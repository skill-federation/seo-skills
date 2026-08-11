# seo

> Era-checked implementation reference and audit workflow for technical SEO and answer-engine (AEO) visibility, current to 2026: copy-paste JSON-LD, robots, canonical and hreflang blocks, vendored Lighthouse, PageSpeed and Search Console scripts, plus a load-bearing llms.txt caution. Reach for it when building or reviewing a site's markup, crawlability, or AI-citation posture; it will not recommend retired rich-result types.

**Install** (the [`skills`](https://www.npmjs.com/package/skills) CLI reads this repo's layout directly from GitHub)

```bash
npx skills add skill-federation/seo-skills --skill seo
```

## Conditions

### When to use
- Implementing or reviewing markup you control: JSON-LD, robots, canonicals, sitemaps, hreflang, mobile meta.
- Running the audit loop via the vendored Lighthouse/PageSpeed/Search Console scripts.
- Making pages extractable and citable by answer engines without over-claiming.

### When NOT to use
- Keyword research, content strategy, backlink campaigns — this reference plans nothing.
- Requests for FAQ or HowTo markup "to win rich results" — see Era; that lever is retired.
- Scored audits of arbitrary domains or repo-level static validation — other skills do that.

### Prerequisites
- `bash` + `curl`; Node 18+ (`search-console-export.mjs`); Lighthouse CLI (`npm i -g lighthouse`); `python3` (`pagespeed.sh` URL-encoding).
- `PAGESPEED_API_KEY`; `GSC_ACCESS_TOKEN` OAuth token, `webmasters.readonly` scope.
- Deploy access to the site's HTML and headers.

### What breaks first
- Schema-type status: templates keep validating after the result type retires (FAQ 2026-05-07, HowTo September 2023).
- AI-crawler user-agent names churn; re-check before editing robots.txt.
- API surfaces: PageSpeed v5, Search Console v1 (25,000-row cap), Lighthouse CLI flags.
- Adoption stats (llms.txt ~0.015%) age fastest.

## Era

Targets: Google Search / answer-engine guidance as of 2026-08 · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [addyosmani/web-quality-skills/seo](https://github.com/addyosmani/web-quality-skills) (MIT)
- **Grafted from**: [warpdotdev/oz-skills/seo-aeo-audit](https://github.com/warpdotdev/oz-skills)
- **Sibling** (zero text taken): tech-leads-club/agent-skills/seo
- **Sibling** (zero text taken): manojbajaj95/claude-gtm-plugin/seo-and-aeo-strategy
- **License**: MIT (this directory's LICENSE)
- **What domestication changed**: 3 defect(s) fixed, 4 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
