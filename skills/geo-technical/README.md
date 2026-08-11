# geo-technical

**Score a live site's readiness to be read by machines: fetch raw HTML, hold it against the browser render, and grade eight infrastructure categories out of 100 before any content or GEO work starts. Use when pages rank nowhere, AI assistants never cite the site, or a JavaScript framework may be hiding the copy from crawlers. Era-stamped for 2026 — retired rich-result types and unproven conventions stay out of the score.**

An upgraded, era-verified derivative of [`zubair-trabzada/geo-seo-claude/geo-technical`](https://github.com/zubair-trabzada/geo-seo-claude) —
1 defect fix and 2 excisions, with its guidance checked against platform reality current to 2026 (the kind
of dated facts a wild skill silently predates). Conditions are stated, every workflow step ends
in a runnable check, and what changed from the original is recorded with reasons.

## Install

```bash
npx skills add skill-federation/seo-skills --skill geo-technical
```

## When to use it

- A live, publicly reachable site needs a technical audit before (or alongside) AI-search or content work — this is the infrastructure layer both depend on.
- Pages rank nowhere or are never cited by AI assistants, and you suspect the cause sits below the content: blocked crawlers, client-side rendering, broken canonicals, slow servers.
- You need a scored, evidence-backed report (a 100-point rubric with per-category breakdowns) where every finding traces to a fetch that was actually run.
- No toolchain install is warranted or available: a shell with `curl` suffices here (see Prerequisites), where the orchestrated-suite alternative (claude-seo) needs its own isolated Python runtime and Chromium before it can audit anything.

## When NOT to use it

- The work lives in a repository, not at a URL. This audit inspects a deployed site over HTTP; it cannot read a codebase or catch problems before they ship.
- You need content, keyword, or citation-quality analysis. This document scores infrastructure only and says nothing about what the words should be.
- The site is not fetchable from where you run (auth walls, intranet-only, geo-blocks). Every check here starts from a fetch; an unreachable site produces no score — report that instead of estimating.
- You want evidence of what AI crawlers actually did over time. That lives in server access logs, which this audit does not read.
- You just need a fast scored verdict on AI-crawler legibility, not an eight-category inspection: the bundle's ~30-second scripted check (geo-audit) answers that; return here when its low score needs diagnosis.
- On ordinary business sites, the 9.1 service-discovery result never reaches the report — the header capture itself rides the standard homepage fetch at no cost, so run it either way. The rule (stated in Category 9) scopes the report, not the fetch, and is repeated here so an agent scoping the engagement knows the section is intentionally absent for such sites.

## Provenance & trust

Derived from [`zubair-trabzada/geo-seo-claude/geo-technical`](https://github.com/zubair-trabzada/geo-seo-claude) · MIT · last
verified 2026-08-10. Every source, the full list of changes, and attribution are
in [SKILL.md](SKILL.md); every vendored file is pinned by sha256 in the bundle's
[`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
