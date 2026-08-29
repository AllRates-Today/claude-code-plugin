---
name: official-rates
description: Use the official exchange rate published by a named institution — a central bank or tax authority — rather than a market rate. Load whenever the task involves invoices, VAT or tax returns, customs valuation, transfer pricing, statutory or month-end accounting, audit evidence, or any rule that names a publisher ("the ECB reference rate", "the HMRC monthly rate", "the RBI reference rate", "the rate in force on the invoice date"). Also load when asked which central banks publish rates, or for a rate on a specific past date.
---

# Official published rates

## Why this is a different thing from a market rate

A live mid-market rate answers "what is this worth right now". Compliance rules
almost never ask that. They name a publisher and a date: *the ECB reference rate
on the invoice date*, *the HMRC monthly rate for the accounting period*, *the
Bank of Japan rate in force*. Those are fixed once published, carry the
institution's own publication date, and are what an auditor will check against.

They also differ from the market — by a percent or more, routinely. Using a
market rate for a tax filing produces numbers nobody can reconcile.

**Ask which publisher the rule names.** If the answer is "whatever's current",
it is a market-rate task: use the `exchange-rates` skill instead.

## Keyless: the latest published table of any source

```bash
curl "https://allratestoday.com/api/open/central-bank/hmrc"
curl "https://allratestoday.com/api/open/central-bank/ecb?source=USD&target=EUR"
```

No key, CORS-open, edge-cached. Returns the newest table the source has
published, with its own `rate_date`. Free to use with a visible attribution link
back to allratestoday.com — the response carries the exact wording in
`attribution`.

With this plugin's MCP servers connected, `list_central_banks` and
`get_official_rates` do the same without shelling out.

## Keyed: dates, history, calendars, cross-source comparison

```bash
AUTH="Authorization: Bearer $ALLRATES_API_KEY"
curl -H "$AUTH" "https://allratestoday.com/api/v1/central-bank/ecb/latest"
curl -H "$AUTH" "https://allratestoday.com/api/v1/central-bank/ecb/2026-01-15"
curl -H "$AUTH" "https://allratestoday.com/api/v1/central-bank/ecb/history?symbol=USD&from=2026-01-01&to=2026-03-31"
curl -H "$AUTH" "https://allratestoday.com/api/v1/central-bank/ecb/availability?year=2026"
curl -H "$AUTH" "https://allratestoday.com/api/v1/central-banks/rates?source=USD&target=EUR"
```

Free key at <https://allratestoday.com/register>. Add `?format=csv|xlsx|xml` to
any table endpoint when the deliverable is a file for someone in finance.

## The rules that bite

1. **Weekends and holidays.** Most sources publish on business days only. A
   request for a non-publication date returns the last table actually
   published — the response's `rate_date` tells you which day you really got.
   Record that date, not the date you asked for; that is the audit trail.
2. **Cadence differs by source.** The Fed's H.10 is weekly, the SNB publishes
   monthly averages, the US Treasury is quarterly, most central banks are daily.
   Check the source before assuming yesterday's rate exists.
3. **Quote direction.** Each source publishes against its own home currency —
   the ECB quotes EUR→x, the Fed quotes some pairs the other way round. Read
   `base` and `quote` from the row rather than assuming.
4. **`derived: true` means we inverted or crossed it**, because the source did
   not publish that pair directly. Legitimate for display; say so if the number
   is going into a filing, because the publisher did not publish it.
5. **Do not derive one institution's rate from another's.** If the rule names
   HMRC, an ECB rate crossed through USD is not an HMRC rate.

## Finding the right source code

`list_central_banks` (MCP) or `GET /api/v1/central-banks` lists every covered
institution with its code, country, home currency and coverage window. Common
ones: `ecb`, `fed`, `boe`, `boj`, `pboc`, `rbi`, `snb`, `rba`, `boc`, `cbr`,
`tcmb`, `bcb`, `sarb`, plus tax authorities `hmrc`, `ustreasury`, `bazg`.

`references/sources.md` has the full bundled catalogue and the per-source npm
packages (`npm i ecb-exchange-rate`, `hmrc-exchange-rate`, …) for pinning a
single institution into a project without the whole API surface.

Hub page: <https://allratestoday.com/central-bank-rates-api/>
