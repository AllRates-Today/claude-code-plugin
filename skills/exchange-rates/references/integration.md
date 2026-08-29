# Integration reference

Base URL: `https://allratestoday.com/api`. Auth, where required, is
`Authorization: Bearer art_live_...` (some routes also accept `?api_key=`).
Verify SDK versions against the registry before pinning — never paste a version
number from memory.

## Endpoints

| Endpoint | Key? | Returns |
|---|---|---|
| `GET /open/central-bank/{bank}` | no | Latest published table for one source. `?source=&target=` narrows to one pair. |
| `GET /open/geo` | no | `{ country, currency }` for the caller's IP, from Cloudflare's edge. |
| `GET /v1/symbols` | no | `{ currencies: [{ code, name, symbol }], count }` — 160+ ISO 4217 fiat codes. |
| `GET /rate?source=&target=` | yes | `{ rate, source }` — live mid-market, 1 source = `rate` target. |
| `GET /v1/rates?source=&target=EUR,GBP&time=&group=` | yes | One row per target × bucket. `time` is ISO 8601; `group` ∈ hour/day/week/month. |
| `GET /historical-rates?source=&target=&period=` | yes | `period` ∈ `1d`(hourly) `7d` `30d`(daily) `1y`(weekly), window ends now. |
| `GET /v1/central-banks` | yes | Every covered source with coverage dates. |
| `GET /v1/central-bank/{bank}/latest` \| `/{YYYY-MM-DD}` \| `/history` \| `/availability` | yes | Official published tables. See the `official-rates` skill. |

Table endpoints also take `?format=csv|xml|xlsx` alongside the default JSON.

Errors are `{ "error": "..." }` with a real status code: `400` unknown currency
or bad params, `401` missing/invalid key, `402/403` paid plan required, `404`
unknown bank or unsupported pair, `429` quota exceeded. Handle `429` by backing
off and serving cache — not by retrying in a loop.

## Billing shape (matters for how you write the loop)

- One request = one call, **except** `/historical-rates`, billed one call per
  currency per month of data returned. A 1-year, 3-currency pull is ~36 calls.
- Free tier: 300 requests, lifetime — it does not reset monthly. Fine for
  development; a production integration needs a paid plan.
- So: batch with `target=EUR,GBP,JPY` in one call rather than looping pairs, and
  cache. Never put a rate fetch inside a per-row or per-request path.

## SDKs

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

const { rates } = await client.latest({ base: 'USD', symbols: ['EUR', 'GBP', 'JPY'] });
const result   = await client.convert('USD', 'EUR', 1000);
const past     = await client.convert('USD', 'EUR', 1000, { date: '2026-01-15' });
const series   = await client.timeSeries('2026-01-01', '2026-03-31', { base: 'USD', symbols: ['EUR'] });
const history  = await client.getHistoricalRates('USD', 'EUR', '30d');
const { symbols } = await client.symbols();
```

```python
from allratestoday import AllRatesToday
client = AllRatesToday(api_key=os.environ["ALLRATES_API_KEY"])
rate    = client.get_rate("USD", "EUR")
result  = client.convert("USD", "EUR", 1000)
history = client.get_historical_rates("USD", "EUR", "30d")
```

```php
use AllRatesToday\AllRatesToday;
$client = new AllRatesToday(getenv('ALLRATES_API_KEY'));
$rate = $client->getRate('USD', 'EUR');
```

Per-bank SDKs exist for every covered institution
(`npm i ecb-exchange-rate`, `hmrc-exchange-rate`, …) — see the `official-rates`
skill.

## Showing prices in the visitor's currency (React)

```bash
npm install react-currency-localizer-realtime
```

```jsx
import { LocalizedPrice } from 'react-currency-localizer-realtime';
<LocalizedPrice basePrice={19.99} baseCurrency="USD" />
```

v2 is keyless by default: it detects the visitor's currency from
`GET /api/open/geo` and converts from the open rate table, so it works with no
signup. Pass `apiKey` to switch it to real-time mid-market rates.

Server-rendered pages should do the same work at the edge — read the country
header your platform provides (`CF-IPCountry` on Cloudflare), map to a currency,
convert once per render with a cached rate. Always show the currency code next
to a converted price, and keep the original price available: a converted number
is an estimate, not a charge.

## Caching that actually works

Key the cache on the **pair**, never on the URL or the user. A 60-second TTL on
`USD→EUR` serves every page that needs it; a per-URL cache with a thousand
converter pages multiplies upstream calls by a thousand for identical data.

For official rates, cache until the source's next publication — the table for a
given `rate_date` never changes. `stale-while-revalidate` is the right shape:
serve the last known rate immediately, refresh behind it, and surface the
`rate_date`/timestamp in the UI so a stale number is visibly stale.
