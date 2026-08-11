# geo-audit

> A scored technical audit of whether a live domain is legible to AI-search crawlers, current to 2026: one stdlib Python script, about 30 seconds, five load-bearing checks (robots.txt bot access, pre-JS rendering, sitemap, JSON-LD, internal links) with llms.txt reported as informational only. Reach for it when a site needs a fast numeric verdict on AI-crawler visibility before content spend; it refuses to emit numbers when the script cannot run or the domain will not resolve.

**Install** (the [`skills`](https://www.npmjs.com/package/skills) CLI reads this repo's layout directly from GitHub)

```bash
npx skills add skill-federation/seo-skills --skill geo-audit
```

## Conditions

### When to use

- A live, publicly reachable domain needs a fast scored read on AI-crawler legibility — before a content program, during triage, or when someone asks why ChatGPT, Perplexity, Gemini or Claude never surfaces the site.
- The user says "run a GEO audit on <url>", "audit <url> for GEO", "how AI-ready is my site" or a close variant: extract the domain and run the script immediately, no clarifying questions.
- You want a keepable artifact: the script writes an HTML report alongside the streamed terminal scorecard.

### When NOT to use

- The site only exists in a repository or on localhost — this skill fetches public URLs; use a repository-reading validator for pre-ship checks.
- Content writing, comparison pages, or GEO strategy and cadence work — this is an audit; it produces no prose and no plan.
- Auth-walled or staging hosts the public internet cannot fetch, and domains behind a WAF that challenges plain scripted user agents — the score would measure the wall, not the site.
- Anything needing a deep multi-page crawl: the script reads the homepage plus a handful of well-known root paths, nothing more.

### Prerequisites

- `python3` on PATH; the script uses only the standard library (no pip installs).
- Outbound HTTPS from the session to the target domain — the script performs about a dozen GET requests.
- The vendored script at `{baseDir}/scripts/audit.py` (sha256 pinned in the frontmatter).

### What breaks first

- DNS failure does not abort the run: the script still prints a scorecard (its robots.txt check hands 18 partial-credit points to a domain that does not exist). The tripwire is the finding "Homepage did not return 200 (0)" — status 0 means the fetch itself errored. Treat that run as failed and produce no score.
- Bot-challenging CDNs: a 403 or 503 to the script's user agent zeroes the rendering and link checks regardless of what real AI crawlers see. Report the block; do not score through it.
- Slow origins: the per-request timeout defaults to 10 seconds; heavy sites can trip it. Re-run with a higher `--timeout` before concluding anything.

## Era

Targets: audit.py 1.0 (upstream HEAD, fetched 2026-08-10) · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [vellum-ai/vellum-assistant/geo-audit](https://github.com/vellum-ai/vellum-assistant) (MIT)
- **License**: MIT (this directory's LICENSE)
- **What domestication changed**: 4 defect(s) fixed, 2 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
