# geo-audit

**A scored technical audit of whether a live domain is legible to AI-search crawlers, current to 2026: one stdlib Python script, about 30 seconds, five load-bearing checks (robots.txt bot access, pre-JS rendering, sitemap, JSON-LD, internal links) with llms.txt reported as informational only. Reach for it when a site needs a fast numeric verdict on AI-crawler visibility before content spend; it refuses to emit numbers when the script cannot run or the domain will not resolve.**

An upgraded, era-verified derivative of [`vellum-ai/vellum-assistant/geo-audit`](https://github.com/vellum-ai/vellum-assistant) —
4 defect fixes and 2 excisions, with its guidance checked against platform reality current to 2026 (the kind
of dated facts a wild skill silently predates). Conditions are stated, every workflow step ends
in a runnable check, and what changed from the original is recorded with reasons.

## Install

```bash
npx skills add skill-federation/seo-skills --skill geo-audit
```

## When to use it

- A live, publicly reachable domain needs a fast scored read on AI-crawler legibility — before a content program, during triage, or when someone asks why ChatGPT, Perplexity, Gemini or Claude never surfaces the site.
- The user says "run a GEO audit on <url>", "audit <url> for GEO", "how AI-ready is my site" or a close variant: extract the domain and run the script immediately, no clarifying questions.
- You want a keepable artifact: the script writes an HTML report alongside the streamed terminal scorecard.

## When NOT to use it

- The site only exists in a repository or on localhost — this skill fetches public URLs; use a repository-reading validator for pre-ship checks.
- Content writing, comparison pages, or GEO strategy and cadence work — this is an audit; it produces no prose and no plan.
- Auth-walled or staging hosts the public internet cannot fetch, and domains behind a WAF that challenges plain scripted user agents — the score would measure the wall, not the site.
- Anything needing a deep multi-page crawl: the script reads the homepage plus a handful of well-known root paths, nothing more.

## Provenance & trust

Derived from [`vellum-ai/vellum-assistant/geo-audit`](https://github.com/vellum-ai/vellum-assistant) · MIT · last
verified 2026-08-10. Every source, the full list of changes, and attribution are
in [SKILL.md](SKILL.md); every vendored file is pinned by sha256 in the bundle's
[`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
