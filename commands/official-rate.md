---
description: Get the official rate published by a central bank or tax authority
argument-hint: [ecb USD EUR]
allowed-tools: [Bash, Read]
---

# Official published rate

The user asked for: $ARGUMENTS

Read the `official-rates` skill first — the rules about publication dates,
weekends, quote direction and derived pairs all apply here.

Work out the source code (`ecb`, `fed`, `boe`, `boj`, `rbi`, `hmrc`,
`ustreasury`, …), the pair, and the date. If the user named an institution but
you are unsure of its code, list the covered sources first — MCP
`list_central_banks`, or `skills/official-rates/references/sources.md`.

- Latest published table, no key needed:
  ```bash
  curl -sS "https://allratestoday.com/api/open/central-bank/BANK?source=SRC&target=TGT"
  ```
- A specific past date (needs `ALLRATES_API_KEY` on a paid plan; free and
  trial keys get `403`, so say so rather than retrying):
  ```bash
  curl -sS -H "Authorization: Bearer $ALLRATES_API_KEY" \
    "https://allratestoday.com/api/v1/central-bank/BANK/YYYY-MM-DD?source=SRC&target=TGT"
  ```

Always report the `rate_date` the response came back with — it may be earlier
than the date requested, because the source did not publish that day, and that
returned date is the one to record. Say plainly when a pair is `derived`.
