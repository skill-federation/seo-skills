# ai-bot-log-audit

**Method for reading Apache and Nginx access-log evidence to establish what GPTBot, ClaudeBot, PerplexityBot and peers actually fetch, skip, or error on, and which fixes each fetch pattern calls for. Reach for it when a citation-gap theory needs log rows behind it and you can export the raw logs. Domesticated 2026-08; the bot roster is carried from the wild source's 2026 table, not independently re-checked.**

An upgraded, era-verified derivative of [`guia-matthieu/clawfu-skills/ai-bot-log-audit`](https://github.com/guia-matthieu/clawfu-skills) —
1 defect fix and 3 excisions, with its guidance checked against platform reality current to 2026 (the kind
of dated facts a wild skill silently predates). Conditions are stated, every workflow step ends
in a runnable check, and what changed from the original is recorded with reasons.

## Install

```bash
npx skills add skill-federation/seo-skills --skill ai-bot-log-audit
```

## When to use it

- You have — or can export — Apache or Nginx access logs, and you want to know what AI crawlers actually fetch, skip, and error on, instead of arguing from theory.
- Your content exists but AI search rarely or never cites it, and the diagnosis should start from crawl evidence rather than from a content rewrite.
- You are scoping GEO work and need to know which pages the bots already prioritize, how often they return, and where crawl budget is being wasted.
- You changed robots.txt, URL structure, or internal linking and want before/after evidence of the effect on AI-bot access.
- Typical operators: SEO professionals adding AI search to their scope, publishers monitoring AI traffic and content extraction, technical SEOs running log-file analysis, content strategists deciding what to optimize for AI visibility.

## When NOT to use it

- Without log access. This document cannot read your logs for you — you bring the log data, this document brings the method. If the logs cannot be produced, stop: no phase below has a theory-only fallback.
- On analytics exports. Web-analytics dashboards are built around human sessions; the fetches this audit studies live in server access logs, and those are the only input the commands below accept.
- For page-quality questions detached from crawl behavior. Only Phase 4 touches on-page structure, and only as placement for retrieval — a content-quality audit is a different job.
- To check citation status. This method cannot query live AI search results — whether ChatGPT, Perplexity, or AI Overviews currently cite you is knowledge you bring from outside; the Phase 2 "fetches but doesn't cite" row consumes that knowledge, it cannot produce it.
- To promise outcomes. Crawl evidence improves the odds of citation; nothing in this method can guarantee that any AI product will cite you.
- As a substitute for a specialist. Per the base's own boundary, this method does not replace technical SEO expertise for complex log analysis — sampled logs, multi-CDN merges, and bot-mitigation layers need one.

## Provenance & trust

Derived from [`guia-matthieu/clawfu-skills/ai-bot-log-audit`](https://github.com/guia-matthieu/clawfu-skills) · MIT · last
verified 2026-08-10. Every source, the full list of changes, and attribution are
in [SKILL.md](SKILL.md); every vendored file is pinned by sha256 in the bundle's
[`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
