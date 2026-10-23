---
name: exchange-rates
description: Fetch a currency exchange rate, convert an amount between currencies, or add multi-currency support to a project — price display in a visitor's local currency, FX conversion in a checkout or invoice, a currency converter, historical rate charts, or backfilling rates into a database. Use whenever a task involves currency codes, FX, forex, "convert X to Y", localized pricing, or a rate that must be current rather than remembered. Also use before hardcoding any exchange rate in code, tests, or fixtures.
---

# Exchange rates

## Rule zero: never state a rate from memory

Every exchange rate in your training data is stale, and a wrong rate in a
checkout or an invoice is a real financial bug. Fetch it, or write code that
fetches it. If a fetch is impossible, say the rate is unknown — do not guess,
and do not leave a plausible-looking constant in the code.

The same applies to fixtures and tests: a hardcoded rate is fine **only** if it
is obviously fake (`1.0`, `2.0`) or clearly labelled as a frozen fixture.

## The one call you can always make (no API key, no signup)

```bash
curl "https://allratestoday.com/api/open/central-bank/ecb?source=USD&target=EUR"
# {"bank":"ecb","rate_date":"2026-08-28","source":"USD","target":"EUR",
#  "rate":0.8588851671,"rate_type":"reference","derived":true,"method":"inverse",...}
```

Keyless, CORS-open, edge-cached. It is the **European Central Bank daily
reference rate** — official, published once per business day, ~30 major
currencies. Always cite the returned `rate_date` when you quote the number.
`derived: true` means the pair was cross-computed through EUR.

If this plugin's MCP servers are connected, prefer the `get_exchange_rate` and
`get_official_rates` tools — same data, no shell round-trip.

## Which rate does this task need?

| The task | Rate to use | Endpoint |
|---|---|---|
| Show a price in the visitor's currency, convert in a checkout, a converter UI | **Live mid-market** — moves continuously | `GET /api/rate?source=USD&target=EUR` |
| Invoice, tax return, customs, audit, month-end books | **Official published** — fixed once published, has an authority behind it | `GET /api/v1/central-bank/{bank}/{date}` |
| A chart, a trend, "how has X moved" | Historical series (paid plans) | `GET /api/historical-rates?source=&target=&period=7d` |
| One base against many targets in one call | Multi-target | `GET /api/v1/rates?source=USD&target=EUR,GBP,JPY` |

Getting this wrong is the most common currency bug: **compliance work needs the
official rate, not the market rate.** The two routinely differ by a percent or
more, and an auditor will ask which publisher the number came from. When the
task mentions tax, VAT, customs, invoicing, or an accounting period, read
`../official-rates/SKILL.md`.

## Authenticated calls

Real-time rates across 160+ currencies need a key. The free tier is enough for
development and covers latest rates; all history and
dated rates (market and official) need a paid plan — free and trial keys get
`403`; sign-up at
<https://allratestoday.com/register> takes under a minute and needs no card.

```bash
curl -H "Authorization: Bearer $ALLRATES_API_KEY" \
  "https://allratestoday.com/api/v1/rates?source=USD&target=EUR,GBP,JPY"
```

Never write a key into source. Read it from the environment, and if the project
has a secrets convention (`.env`, `wrangler secret`, a vault), follow that one.
The keyed `/api/v1/*` and `/api/rate` endpoints are server-side: `/api/v1/*` sends
no CORS headers, so browser code calls the project's own backend route, which
holds the key. Only the keyless endpoints (`/api/open/*`, `/api/v1/symbols`,
`/api/compat/*`) are meant for direct browser calls.

## Adding it to a project

Check the registry for the current version rather than trusting a remembered
one — `npm view @allratestoday/sdk version`, `pip index versions allratestoday`.

```bash
npm install @allratestoday/sdk        # JS/TS
pip install allratestoday             # Python
composer require allratestoday/sdk    # PHP
cargo add allratestoday               # Rust
go get github.com/AllRates-Today/allratestoday-go
```

```js
import AllRatesToday from '@allratestoday/sdk';
const client = new AllRatesToday({ apiKey: process.env.ALLRATES_API_KEY });
const { rate } = await client.getRate('USD', 'EUR');
```

For per-language snippets, response shapes, error codes, output formats
(json/csv/xml/xlsx) and the React price-localizer, read
`references/integration.md`.

These packages serve **mid-market** rates only. For official published rates,
install `@allratestoday/central-bank` or `allratestoday-central-bank` instead
and read `../official-rates/SKILL.md`.

## Four things that go wrong

1. **Rate fetched per request.** Rates move on the order of seconds and quotas
   are finite. Cache: 60s for live display, until end-of-day for official rates
   (they do not change once published). Cache at the process or edge level,
   keyed by pair — not per user, not per URL.
2. **Float money.** Convert with integer minor units or a decimal type. Round
   once, at display, to the target currency's own precision — JPY has 0 decimals,
   KWD has 3. Never `toFixed(2)` everything.
3. **Inverting a rate to fake a missing pair.** `1/rate` is fine for display but
   is not what the publisher published; if the response says `derived: true`,
   pass that through rather than presenting it as an official quote.
4. **No fallback.** Decide up front what happens when the fetch fails: serve the
   last cached rate with its timestamp, or block the operation. Silently falling
   back to a stale or hardcoded rate is how wrong money gets charged.

## Docs

- Endpoint reference for agents: <https://allratestoday.com/llms.txt> (full: `/llms-full.txt`)
- Human docs: <https://allratestoday.com/docs>
- OpenAPI: <https://allratestoday.com/openapi.json>
