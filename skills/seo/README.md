# seo

**Era-checked implementation reference and audit workflow for technical SEO and answer-engine (AEO) visibility, current to 2026: copy-paste JSON-LD, robots, canonical and hreflang blocks, vendored Lighthouse, PageSpeed and Search Console scripts, plus a load-bearing llms.txt caution. Reach for it when building or reviewing a site's markup, crawlability, or AI-citation posture; it will not recommend retired rich-result types.**

An upgraded, era-verified, defect-fixed derivative of [`addyosmani/web-quality-skills/seo`](https://github.com/addyosmani/web-quality-skills), checked against platform reality current to 2026 (the kind of dated facts a wild skill silently predates). Conditions are stated, and every workflow step ends in a runnable check.

## Install

```bash
npx skills add skill-federation/seo-skills --skill seo
```

## When to use it

- Implementing or reviewing markup you control: JSON-LD, robots, canonicals, sitemaps, hreflang, mobile meta.
- Running the audit loop via the vendored Lighthouse/PageSpeed/Search Console scripts.
- Making pages extractable and citable by answer engines without over-claiming.

## When NOT to use it

- Keyword research, content strategy, backlink campaigns — this reference plans nothing.
- Requests for FAQ or HowTo markup "to win rich results" — see Era; that lever is retired.
- Scored audits of arbitrary domains or repo-level static validation — other skills do that.

## Provenance & trust

Derived from [`addyosmani/web-quality-skills/seo`](https://github.com/addyosmani/web-quality-skills) · MIT · last verified 2026-08-10. Attribution is in [SKILL.md](SKILL.md)'s Attribution section; every vendored file is pinned by sha256 in the bundle's [`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
