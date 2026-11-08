---
description: Look up a current exchange rate for a currency pair
argument-hint: [USD EUR]
allowed-tools: [Read]
---

# Current exchange rate

The user asked for: $ARGUMENTS

Parse the source and target ISO 4217 codes out of that (accept `USD EUR`,
`USD/EUR`, `usd to eur`, or currency names). If only one code is given, use the
other side the user most likely means and say which you assumed. If nothing
parses, ask for the pair — do not guess.

Then fetch it. Never answer from memory.

1. Call the `allratestoday` MCP tool `get_exchange_rate`. With an API key in
   the plugin settings it returns the live mid-market rate; without one, the
   latest ECB official rate.
2. Only if the MCP server is not connected, use the keyless endpoint:
   ```bash
   curl -sS "https://allratestoday.com/api/open/central-bank/ecb?source=SRC&target=TGT"
   ```

Report in two lines: the rate, then what it is — either "live mid-market" or
"ECB official reference rate published on <rate_date>". Flag `derived: true` as
cross-computed. If the keyless call 404s, the pair is outside the ECB table;
say so and point at the free key for full 160-currency coverage.
