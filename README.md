# AllRatesToday for Claude Code

Currency exchange rates your coding agent can actually trust — because it
fetches them instead of remembering them.

```
/plugin marketplace add AllRates-Today/claude-code-plugin
/plugin install allratestoday@allratestoday
```

**No API key needed to start.** Both MCP servers run keyless out of the box.

## What you get

**Two skills** that load themselves when the work calls for them:

- `exchange-rates` — live mid-market rates, currency conversion, localized
  pricing, historical series, and the rules for wiring any of it into a
  codebase (cache by pair, money in minor units, explicit failure behaviour).
- `official-rates` — the published rate from a *named* institution, which is
  what invoices, VAT returns, customs valuation and statutory accounting
  actually require. 121 central banks and 3 tax authorities.

**Five slash commands:**

| Command | Does |
|---|---|
| `/rate USD EUR` | Current rate for a pair |
| `/convert 1500 USD to EUR` | Convert an amount, rounded to the target currency's precision |
| `/official-rate ecb USD EUR` | The latest rate a named authority published (past dates need a paid plan) |
| `/fx-history USD EUR 30d` | Historical series for a pair (paid plan) |
| `/add-currency-support` | Reads your project and wires rates in the way that project already does things |

**Two MCP servers**, so the model can fetch rates directly:

- [`@allratestoday/mcp-server`](https://www.npmjs.com/package/@allratestoday/mcp-server)
  — live mid-market rates, 160+ currencies, the Daily Reference Rate (16:00 London fix) and a `request_trial_key` tool that self-issues a 100-call, 7-day key when the keyless tools are not enough
- [`@allratestoday/central-bank-mcp`](https://www.npmjs.com/package/@allratestoday/central-bank-mcp)
  — official published tables, publication calendars, and (paid plan) dated tables and history

The skills also point at the right package when Claude writes the integration:
[`@allratestoday/sdk`](https://www.npmjs.com/package/@allratestoday/sdk) /
[`allratestoday`](https://pypi.org/project/allratestoday/) for mid-market rates,
[`@allratestoday/central-bank`](https://www.npmjs.com/package/@allratestoday/central-bank) /
[`allratestoday-central-bank`](https://pypi.org/project/allratestoday-central-bank/)
for official published ones.

## Keyless vs keyed

Installed with no configuration, the plugin answers from the open, edge-cached
endpoints: the official ECB daily reference rate (~30 major currencies) and the
latest published table of any covered central bank or tax authority. That is
enough for most "what is this in EUR" work and for display-only features.

A **free API key** (<https://allratestoday.com/register> — no card, under a
minute) adds real-time mid-market rates across 160+ currencies, multi-target lookups,
publication calendars, and cross-source comparison. All history and dated rates
— mid-market history, dated official tables and official history — need a paid
plan (free and trial keys get a 403).
Set it once and both servers pick it up:

```bash
export ALLRATES_API_KEY=art_live_...
```

## Why it exists

An LLM asked for an exchange rate will happily produce one from training data.
It will look right. It will be months stale, and in a checkout or an invoice
that is a financial bug, not a rounding error. This plugin makes fetching the
rate the path of least resistance, and makes the mid-market/official
distinction — the one that quietly breaks tax filings — explicit.

## Links

- API docs: <https://allratestoday.com/docs> · for agents: <https://allratestoday.com/llms.txt>
- Central bank coverage: <https://allratestoday.com/central-bank-rates-api/>
- Pricing: <https://allratestoday.com/pricing> · Support: support@allratestoday.com
- [Register (Free)](https://allratestoday.com/register)
- [Dashboard](https://allratestoday.com/profile)
- [Status](https://allratestoday.com/status)
- [GitHub](https://github.com/AllRates-Today/claude-code-plugin)

MIT licensed.
