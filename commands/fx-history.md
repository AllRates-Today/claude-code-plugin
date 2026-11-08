---
description: Pull a historical exchange rate series for a pair
argument-hint: [USD EUR 30d]
allowed-tools: [Read]
---

# Historical rate series

The user asked for: $ARGUMENTS

Parse the pair and the window. Fixed windows ending now use the MCP tool
`get_historical_rates` with `period` ∈ `1d` (hourly), `7d`, `30d` (daily),
`1y` (weekly). An explicit date range uses `get_rates_authenticated` with
`time`/`group`; one central bank's official series uses
`get_official_rate_history`.

These calls need an API key on a **paid plan** in the plugin settings: free and trial keys get
`403 historical_requires_paid_plan`. Without a key, or on a 403, say so in a
sentence and point at <https://allratestoday.com/pricing> rather than retrying.
History is billed by volume (`period=1y` costs 12 calls; a single-target
`from`/`to` range costs one call per 31 days, max 366 days per request), so
pull the window the user actually asked for rather than a year "to be safe".

Summarise: start, end, min, max, and the direction of the move. Only write a
file or a chart if the user asked for one; ask where it should go rather than
assuming.
