# ai-bot-log-audit

> Method for reading Apache and Nginx access-log evidence to establish what GPTBot, ClaudeBot, PerplexityBot and peers actually fetch, skip, or error on, and which fixes each fetch pattern calls for. Reach for it when a citation-gap theory needs log rows behind it and you can export the raw logs. Domesticated 2026-08; the bot roster is carried from the wild source's 2026 table, not independently re-checked.

**Install** (the [`skills`](https://www.npmjs.com/package/skills) CLI reads this repo's layout directly from GitHub)

```bash
npx skills add skill-federation/seo-skills --skill ai-bot-log-audit
```

## Conditions

### When to use

- You have — or can export — Apache or Nginx access logs, and you want to know what AI crawlers actually fetch, skip, and error on, instead of arguing from theory.
- Your content exists but AI search rarely or never cites it, and the diagnosis should start from crawl evidence rather than from a content rewrite.
- You are scoping GEO work and need to know which pages the bots already prioritize, how often they return, and where crawl budget is being wasted.
- You changed robots.txt, URL structure, or internal linking and want before/after evidence of the effect on AI-bot access.
- Typical operators: SEO professionals adding AI search to their scope, publishers monitoring AI traffic and content extraction, technical SEOs running log-file analysis, content strategists deciding what to optimize for AI visibility.

### When NOT to use

- Without log access. This document cannot read your logs for you — you bring the log data, this document brings the method. If the logs cannot be produced, stop: no phase below has a theory-only fallback.
- On analytics exports. Web-analytics dashboards are built around human sessions; the fetches this audit studies live in server access logs, and those are the only input the commands below accept.
- For page-quality questions detached from crawl behavior. Only Phase 4 touches on-page structure, and only as placement for retrieval — a content-quality audit is a different job.
- To check citation status. This method cannot query live AI search results — whether ChatGPT, Perplexity, or AI Overviews currently cite you is knowledge you bring from outside; the Phase 2 "fetches but doesn't cite" row consumes that knowledge, it cannot produce it.
- To promise outcomes. Crawl evidence improves the odds of citation; nothing in this method can guarantee that any AI product will cite you.
- As a substitute for a specialist. Per the base's own boundary, this method does not replace technical SEO expertise for complex log analysis — sampled logs, multi-CDN merges, and bot-mitigation layers need one.

### Prerequisites

- Apache or Nginx access logs in combined log format, covering a window long enough to show frequency patterns (weeks, not hours). The commands below index fields by that format: user agent is field 6 when splitting on double quotes, request path is field 7, timestamp is field 4, status is field 9.
- A shell with grep, awk, sort, uniq, and wc; curl for the Phase 4 placement check.
- Knowledge of where your logs actually originate (origin server vs CDN). CDN log exports use their own layouts — map their fields to the combined-format positions before running anything.

### What breaks first

- No logs → no evidence → the audit stops. Do not fall back to theory: a scored report written without log rows is exactly the confident-but-unverified artifact this method exists to displace.
- A custom LogFormat silently shifts the awk field positions and produces plausible-looking garbage (paths tallied as user agents, status codes as paths). The field sanity check in Phase 1's Verify catches this — run it before trusting any count.
- The bot roster goes stale as vendors add crawlers — and the roster here is the wild source's 2026 table, not independently re-checked (see Era). The Phase 2 reconciliation flags hits that the tally pattern no longer covers.
- User-agent strings in logs are self-declared and can be spoofed by scrapers borrowing a well-known bot name. Treat UA-only identification as provisional, and check the operator documentation listed under References before reading a surprising spike as genuine vendor traffic.

## Era

Targets: wild-2026 AI-crawler user-agent table, domesticated 2026-08 · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [guia-matthieu/clawfu-skills/ai-bot-log-audit](https://github.com/guia-matthieu/clawfu-skills) (MIT)
- **License**: MIT (this directory's LICENSE)
- **What domestication changed**: 1 defect(s) fixed, 3 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
