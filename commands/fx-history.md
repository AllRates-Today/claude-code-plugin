---
description: Pull a historical exchange rate series for a pair
argument-hint: [USD EUR 30d]
allowed-tools: [Bash, Read, Write]
---

# Historical rate series

The user asked for: $ARGUMENTS

Parse the pair and the window. Fixed windows ending now use
`/api/historical-rates` with `period` ∈ `1d` (hourly), `7d`, `30d` (daily),
`1y` (weekly). An explicit date range uses the SDK's time-series call or
`/api/v1/rates` with `time`/`group`.

```bash
curl -sS -H "Authorization: Bearer $ALLRATES_API_KEY" \
  "https://allratestoday.com/api/historical-rates?source=SRC&target=TGT&period=30d"
```

This route needs a key: without one, say so in a sentence and point at
<https://allratestoday.com/register> (free, no card). Note that history is
billed one call per currency per month of data returned, so pull the window the
user actually asked for rather than a year "to be safe".

Summarise: start, end, min, max, and the direction of the move. Only write a
file or a chart if the user asked for one; ask where it should go rather than
assuming.
