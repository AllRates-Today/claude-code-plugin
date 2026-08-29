---
description: Look up a current exchange rate for a currency pair
argument-hint: [USD EUR]
allowed-tools: [Bash, Read]
---

# Current exchange rate

The user asked for: $ARGUMENTS

Parse the source and target ISO 4217 codes out of that (accept `USD EUR`,
`USD/EUR`, `usd to eur`, or currency names). If only one code is given, use the
other side the user most likely means and say which you assumed. If nothing
parses, ask for the pair — do not guess.

Then fetch it. Never answer from memory.

1. If the `allratestoday` MCP server is connected, call `get_exchange_rate`.
2. Otherwise:
   ```bash
   curl -sS "https://allratestoday.com/api/open/central-bank/ecb?source=SRC&target=TGT"
   ```
   and if `ALLRATES_API_KEY` is set in the environment, prefer the live
   mid-market rate instead:
   ```bash
   curl -sS -H "Authorization: Bearer $ALLRATES_API_KEY" \
     "https://allratestoday.com/api/rate?source=SRC&target=TGT"
   ```

Report in two lines: the rate, then what it is — either "live mid-market" or
"ECB official reference rate published on <rate_date>". Flag `derived: true` as
cross-computed. If the keyless call 404s, the pair is outside the ECB table;
say so and point at the free key for full 160-currency coverage.
