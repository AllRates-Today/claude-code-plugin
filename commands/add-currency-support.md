---
description: Wire live or official exchange rates into the current project
argument-hint: [what needs converting]
allowed-tools: [Read, Glob, Grep, Bash, Write, Edit, WebFetch]
---

# Add currency support to this project

The user wants: $ARGUMENTS

Read the `exchange-rates` skill and its `references/integration.md` before
writing code.

Work in this order:

1. **Establish which rate the feature needs** — live mid-market for display and
   checkout, official published rates for invoices, tax, customs or statutory
   accounting. Ask if it is genuinely ambiguous; the answer changes the
   endpoint, the caching, and the audit story.
2. **Read the codebase before adding anything.** Find the language, package
   manager, HTTP conventions, config/secrets pattern, and cache layer already in
   use. Match them. If some currency handling already exists, extend it rather
   than adding a second path.
3. **Grep for hardcoded rates** (`0.85`, `1.08`, `EUR_RATE`, conversion
   constants in fixtures and seeds). Report what you find; replace what is
   genuinely live-data, leave clearly-labelled test fixtures alone.
4. **Implement**: fetch through the SDK for the project's language when one
   exists, otherwise a plain HTTP call. Cache by pair, not by URL or user. Round
   at display to the target currency's precision, and do money arithmetic in
   minor units or a decimal type — never floats.
5. **Handle failure explicitly** — last cached rate with its timestamp, or block
   the operation. Never silently fall back to a constant.
6. **Keys**: read `ALLRATES_API_KEY` from the environment via whatever secrets
   mechanism the project already uses. Never commit one. The keyless
   `/api/open/central-bank/ecb` path is a legitimate zero-config start for
   display-only features; say when you have used it and what its limits are
   (~30 majors, official daily fixing, not real-time).

Finish by telling the user what you added, which endpoint it calls, what the
cache TTL is, and what happens when the API is down.
