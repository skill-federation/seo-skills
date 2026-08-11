# geo-technical

> Score a live site's readiness to be read by machines: fetch raw HTML, hold it against the browser render, and grade eight infrastructure categories out of 100 before any content or GEO work starts. Use when pages rank nowhere, AI assistants never cite the site, or a JavaScript framework may be hiding the copy from crawlers. Era-stamped for 2026 — retired rich-result types and unproven conventions stay out of the score.

**Install**

```bash
npx skillfed install skill-federation/seo-skills/geo-technical
```

## Conditions

### When to use
- A live, publicly reachable site needs a technical audit before (or alongside) AI-search or content work — this is the infrastructure layer both depend on.
- Pages rank nowhere or are never cited by AI assistants, and you suspect the cause sits below the content: blocked crawlers, client-side rendering, broken canonicals, slow servers.
- You need a scored, evidence-backed report (a 100-point rubric with per-category breakdowns) where every finding traces to a fetch that was actually run.
- No toolchain install is warranted or available: a shell with `curl` suffices here (see Prerequisites), where the orchestrated-suite alternative (claude-seo) needs its own isolated Python runtime and Chromium before it can audit anything.

### When NOT to use
- The work lives in a repository, not at a URL. This audit inspects a deployed site over HTTP; it cannot read a codebase or catch problems before they ship.
- You need content, keyword, or citation-quality analysis. This document scores infrastructure only and says nothing about what the words should be.
- The site is not fetchable from where you run (auth walls, intranet-only, geo-blocks). Every check here starts from a fetch; an unreachable site produces no score — report that instead of estimating.
- You want evidence of what AI crawlers actually did over time. That lives in server access logs, which this audit does not read.
- You just need a fast scored verdict on AI-crawler legibility, not an eight-category inspection: the bundle's ~30-second scripted check (geo-audit) answers that; return here when its low score needs diagnosis.
- On ordinary business sites, the 9.1 service-discovery result never reaches the report — the header capture itself rides the standard homepage fetch at no cost, so run it either way. The rule (stated in Category 9) scopes the report, not the fetch, and is repeated here so an agent scoping the engagement knows the section is intentionally absent for such sites.

### Prerequisites
- The target homepage URL plus 2-3 representative inner pages (an article, a product page, a category page).
- A shell with `curl` — every Verify block below uses it — plus an HTTP-fetch capability for full page retrieval.
- A way to see the browser-rendered DOM for the Category 7 comparison: a headless browser, browser devtools, or a rendering fetch tool.
- Write access to the working directory for the generated `GEO-TECHNICAL-AUDIT.md`. No credentials or third-party API keys are required.

### What breaks first
- The era facts. Schema-type status and emerging conventions (llms.txt, markdown content negotiation) rot faster than anything else in this category — the ## Era section pins their state as of this document's review date.
- The AI crawler roster in 1.2. New bots appear and user-agent strings change; treat the table as a snapshot to extend, not a complete census.
- Core Web Vitals metric definitions. The metric set has changed before (INP for FID in 2024) and can change again, taking Category 6's thresholds with it.
- The markdown content-negotiation check in 9.2 is currently Cloudflare-specific; the check outlives the vendor detail, but the remediation advice may not.

## Era

Targets: web and AI-crawler behavior as of 2026-08 · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [zubair-trabzada/geo-seo-claude/geo-technical](https://github.com/zubair-trabzada/geo-seo-claude) (MIT)
- **License**: MIT (this directory's LICENSE)
- **What domestication changed**: 1 defect(s) fixed, 2 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
