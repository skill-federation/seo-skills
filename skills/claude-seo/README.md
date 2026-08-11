# claude-seo

**Front door for a bundled SEO toolchain: /seo commands route bundled Python through the claude-seo launcher, with a doctor preflight and parallel full audits whose conditional specialists spawn only when site signals warrant them. Use it when an agent must produce client-grade SEO reports under 2026 rules — FAQ rich results retired, HowTo schema dead, llms.txt unproven — behind hard quality gates and with zero promotional content in deliverables.**

An upgraded, era-verified, defect-fixed derivative of [`AgriciDaniel/claude-seo/seo`](https://github.com/AgriciDaniel/claude-seo), checked against platform reality current to 2026 (the kind of dated facts a wild skill silently predates). Conditions are stated, and every workflow step ends in a runnable check.

## Install

```bash
npx skills add skill-federation/seo-skills --skill claude-seo
```

## When to use it

- You want one front door over a full SEO toolchain: 20+ `/seo` commands backed by bundled Python tools, with parallel sub-agent fan-out for full site audits and a unified 0–100 health score.
- You are producing client-grade deliverables (site audits, technical reports, strategic plans) and want hard, enforced quality gates — location-page hard stops, retired-schema refusals — rather than advisory prose.
- The site's business type is unknown up front: the skill detects SaaS / local / e-commerce / publisher / agency signals from the homepage and spawns only the matching specialists.

## When NOT to use it

- For a single quick scored check or a repo-level pre-ship validation: a narrower single-purpose skill costs less than this suite's runtime setup.
- For a one-off full technical audit where toolchain setup isn't warranted: a standalone curl-based audit (geo-technical in this bundle) covers the live eight-category inspection with nothing to install beyond a shell.
- For forensic traffic-drop diagnosis ("why did rankings fall last month") — out of scope across this bundle. `/seo drift` only compares against a baseline captured before the change, and seo-google's organic-traffic trends are data, not a forensic method; neither reconstructs a past you didn't baseline.
- On machines where an isolated Python runtime and Chromium cannot be installed — the bundled tools will not run and the skill degrades to unverified prose.
- When policy forbids sending site or keyword data to third-party vendors and the task depends on the extensions: every extension (Firecrawl, DataForSEO, image-gen, Ahrefs, Bing, Profound, SE Ranking, Unlighthouse) calls a third-party API.

## Provenance & trust

Derived from [`AgriciDaniel/claude-seo/seo`](https://github.com/AgriciDaniel/claude-seo) · MIT · last verified 2026-08-10. Attribution is in [SKILL.md](SKILL.md)'s Attribution section; every vendored file is pinned by sha256 in the bundle's [`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
