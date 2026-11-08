---
description: Convert an amount between two currencies at the current rate
argument-hint: [1500 USD to EUR]
allowed-tools: [Read]
---

# Convert an amount

The user asked to convert: $ARGUMENTS

Parse amount, source currency, target currency. Fetch the rate the same way
`/rate` does: the MCP tool `get_exchange_rate`, or, only if the MCP server is
not connected, `https://allratestoday.com/api/open/central-bank/ecb?source=SRC&target=TGT`.
Never convert using a remembered rate.

Show the converted amount rounded to the **target currency's** own precision
(JPY 0 decimals, most currencies 2, KWD/BHD/OMR 3), then the rate used and its
date on a second line. Do the arithmetic explicitly rather than eyeballing it.

If the user is converting for an invoice, a tax filing, or an accounting
period, stop and say so: that needs the official rate published by whichever
authority the rule names, on the relevant date — read the `official-rates`
skill and use `/official-rate` instead.
