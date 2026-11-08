---
description: Get the official rate published by a central bank or tax authority
argument-hint: [ecb USD EUR]
allowed-tools: [Read]
---

# Official rate

The user asked for: $ARGUMENTS

Read the `official-rates` skill first — the rules about publication dates,
weekends, quote direction and derived pairs all apply here.

Work out the source code (`ecb`, `fed`, `boe`, `boj`, `rbi`, `hmrc`,
`ustreasury`, …), the pair, and the date. If the user named an institution but
you are unsure of its code, list the covered sources first — MCP
`list_central_banks`, or `skills/official-rates/references/sources.md`.

- Latest official table, no key needed: MCP `get_official_rates` with `bank`,
  `source`, `target`. If the MCP server is not connected:
  ```bash
  curl -sS "https://allratestoday.com/api/open/central-bank/BANK?source=SRC&target=TGT"
  ```
- A specific past date: `get_official_rates` with `date=YYYY-MM-DD`. This needs
  an API key on a paid plan in the plugin settings; free and trial keys get
  `403`, so say so rather than retrying.

Always report the `rate_date` the response came back with — it may be earlier
than the date requested, because the source did not publish that day, and that
returned date is the one to record. Say plainly when a pair is `derived`.
