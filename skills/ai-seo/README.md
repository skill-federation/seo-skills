# ai-seo

**The GEO/AEO strategy layer for agents, current to Google's 2026 guidance split: answer features ride core ranking while ChatGPT, Claude, and Perplexity reward extractable structure. Load it when planning how a site earns AI citations, before any page edits. It interviews, adjudicates tactics per engine, and emits an evidence-tagged plan; it executes nothing, so pair it with an audit skill that actually fetches the site.**

An upgraded, era-verified derivative of [`coreyhaines31/marketingskills/ai-seo`](https://github.com/coreyhaines31/marketingskills) —
3 defect fixes and 3 excisions, with its guidance checked against platform reality current to 2026 (the kind
of dated facts a wild skill silently predates). Conditions are stated, every workflow step ends
in a runnable check, and what changed from the original is recorded with reasons.

## Install

```bash
npx skills add skill-federation/seo-skills --skill ai-seo
```

## When to use it

- Planning how a site earns citations in AI-generated answers (Google AI Overviews / AI Mode, ChatGPT, Perplexity, Claude, Gemini, Copilot) — before any page is edited.
- Adjudicating tactic-to-engine fit: what Google's stated position permits versus what the other engines reward. This separation is the document's core value.
- Producing the strategy artifact (`ai-seo-plan.md`, defined below) that an executing audit or implementation skill then works from.
- Reviewing someone else's GEO/AEO proposal for era-stale or engine-misattributed tactics.

## When NOT to use it

- **As evidence about a live site's current state.** This is the strategy layer: it asks questions and produces a plan; it runs nothing. It never fetches a page, reads a robots.txt, renders JavaScript, or scores anything. Any claim about what a site *currently* does must come from a paired executing audit skill — one that declares Bash/WebFetch-class tools and actually inspects the site — never from this document. In this bundle that executing role is filled by geo-technical (the full eight-category live inspection), geo-audit (the fast scored ~30-second check), or claude-seo (the suite audit behind its own runtime). A plan produced here that states site facts nobody fetched is the exact confident-report failure this collection exists to prevent.
- For traditional technical and on-page SEO audits (crawlability, indexation, Core Web Vitals) — different job, different tooling.
- For implementing structured data. This document says which schema types matter for AI extraction and why; writing the JSON-LD belongs to a schema-focused skill or your build pipeline.

## Provenance & trust

Derived from [`coreyhaines31/marketingskills/ai-seo`](https://github.com/coreyhaines31/marketingskills) · MIT · last
verified 2026-08-10. Every source, the full list of changes, and attribution are
in [SKILL.md](SKILL.md); every vendored file is pinned by sha256 in the bundle's
[`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
