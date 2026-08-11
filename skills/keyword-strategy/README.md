# keyword-strategy

**Plan which search terms a site should target in 2026: discover candidate queries, label them by search intent, cluster them, screen for winnability, and rank the survivors into a prioritized topical map. The standalone strategy layer — no paid API, and it calls none. Use it to choose targets, size winnable long-tail, or turn a raw export into a plan. It plans targeting only; it audits no live page. For the content plan that consumes the map, see content-strategy.**

An upgraded, era-verified, defect-fixed derivative of [`kostja94/marketing-skills/keyword-research`](https://github.com/kostja94/marketing-skills), checked against platform reality current to 2026 (the kind of dated facts a wild skill silently predates). Conditions are stated, and every workflow step ends in a runnable check.

## Install

```bash
npx skills add skill-federation/seo-skills --skill keyword-strategy
```

## When to use it

- The user wants to decide **which search terms to target** — choosing targets, not writing pages.
- They ask for keyword discovery, search-intent classification, keyword clustering, a topical map, or a prioritized keyword plan.
- They have a raw keyword export (Ahrefs/SEMrush/GSC CSV) and need it turned into an intent-labeled, clustered, prioritized plan.
- They want to size **winnable long-tail** for a new or low-authority site.
- They need the keyword layer *before* a content plan or a page build.

## When NOT to use it

- **Running tool-driven scans, live SERP/keyword fetches, or a full audit behind an installed runtime** — that is **claude-seo**, whose installed-runtime front door drives it (`/seo cluster`, `/seo content-brief`, GSC data via `/seo google`). keyword-strategy is the *standalone* method you can run with only Google autocomplete and a browser; reach for claude-seo when the user has that toolchain installed and wants it driven.
- **The content plan that consumes the map** — editorial calendar, what to write, pillar pages as *content* — is **content-strategy**. keyword-strategy produces the keyword-to-page map; content-strategy turns it into a content plan. Do not rebuild pillar/cluster *content* planning here.
- **AI-search citation** — getting cited by LLMs, AI Overviews, ChatGPT/Perplexity visibility — is **ai-seo** / **geo-plan**. keyword-strategy is traditional keyword targeting, not answer-engine optimization.
- **On-page, technical, or live-page scoring** — this skill audits nothing and fetches no URL to grade it.
- For an end-to-end SEO roadmap that sequences keyword work with the rest, see **seo-plan**.

## Provenance & trust

Derived from [`kostja94/marketing-skills/keyword-research`](https://github.com/kostja94/marketing-skills) · MIT · last verified 2026-08-10. Attribution is in [SKILL.md](SKILL.md)'s Attribution section; every vendored file is pinned by sha256 in the bundle's [`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
