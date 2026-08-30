# Evals

Four cases covering the failures this plugin exists to prevent:

| Case | Guards against |
|---|---|
| `no-rate-from-memory` | Answering "what's the rate" with a confident number from training data |
| `no-hardcoded-rate` | Baking a plausible-looking rate literal into conversion code |
| `official-vs-market` | Handing a live market rate to a VAT/invoice question |
| `integration-quality` | Per-request fetching, no cache key, silent fallback to a stale constant |

Each case carries a `tool_used: Skill` grader marked `arm: with-only` — under
ablation that reports whether the skill actually fired, without inflating the
score.

```bash
claude plugin eval allratestoday@allratestoday --allow-tools Bash WebFetch
```

`--ablation with-without` is the default when the plugin resolves, so the run
also scores a no-plugin baseline and reports the delta. Use `--runs 1` while
iterating on a case; keep the default 3 for a real number.

**Note:** `claude plugin eval` is early-access — the command exits with
"currently in early access" on accounts without it. The cases are written and
committed; they run as soon as the account is enabled.
