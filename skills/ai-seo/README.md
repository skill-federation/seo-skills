# ai-seo

> The GEO/AEO strategy layer for agents, current to Google's 2026 guidance split: answer features ride core ranking while ChatGPT, Claude, and Perplexity reward extractable structure. Load it when planning how a site earns AI citations, before any page edits. It interviews, adjudicates tactics per engine, and emits an evidence-tagged plan; it executes nothing, so pair it with an audit skill that actually fetches the site.

**Install**

```bash
npx skillfed install skill-federation/seo-skills/ai-seo
```

## Conditions

### When to use

- Planning how a site earns citations in AI-generated answers (Google AI Overviews / AI Mode, ChatGPT, Perplexity, Claude, Gemini, Copilot) — before any page is edited.
- Adjudicating tactic-to-engine fit: what Google's stated position permits versus what the other engines reward. This separation is the document's core value.
- Producing the strategy artifact (`ai-seo-plan.md`, defined below) that an executing audit or implementation skill then works from.
- Reviewing someone else's GEO/AEO proposal for era-stale or engine-misattributed tactics.

### When NOT to use

- **As evidence about a live site's current state.** This is the strategy layer: it asks questions and produces a plan; it runs nothing. It never fetches a page, reads a robots.txt, renders JavaScript, or scores anything. Any claim about what a site *currently* does must come from a paired executing audit skill — one that declares Bash/WebFetch-class tools and actually inspects the site — never from this document. In this bundle that executing role is filled by geo-technical (the full eight-category live inspection), geo-audit (the fast scored ~30-second check), or claude-seo (the suite audit behind its own runtime). A plan produced here that states site facts nobody fetched is the exact confident-report failure this collection exists to prevent.
- For traditional technical and on-page SEO audits (crawlability, indexation, Core Web Vitals) — different job, different tooling.
- For implementing structured data. This document says which schema types matter for AI extraction and why; writing the JSON-LD belongs to a schema-focused skill or your build pipeline.

### Prerequisites

- The business context this skill interviews for: key queries, content types, competitors, goals. If `.agents/product-marketing.md` exists (or `.claude/product-marketing.md`, or the legacy `product-marketing-context.md` filename in older setups), read it before asking questions and only ask for what it does not cover.
- A place to write the plan artifact — this document standardizes on `ai-seo-plan.md` and `ai-seo-monitoring.md` in the working directory.
- For Verify steps marked *post-implementation*: shell access (an executing agent or a human) to run the fenced commands against the produced artifacts and, later, the deployed site.

### What breaks first

- **Platform behavior claims.** The engine-landscape table, the citation-share percentages, and the monitoring-tool list are the fastest-rotting parts of this document — vendors change retrieval backends and features without notice.
- **Vendor stances.** Google's published position, quoted in the Era section, can be superseded by newer guidance; when anything here conflicts with a newer dated statement from the vendor, the newer statement wins and this document needs re-verification.
- **OKF.** The Open Knowledge Format is v0.1; breaking changes are possible below 1.0.
- **The same-name fork trap this derivative exists to fix:** copies of this skill circulate frozen at older versions behind near-identical descriptions. Check the version stamp in Era before trusting any copy found in the wild.

## Era

Targets: 2.2.0 · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [coreyhaines31/marketingskills/ai-seo](https://github.com/coreyhaines31/marketingskills) (MIT)
- **Superseded** (zero text taken): b1rdmania/ghostclaw/ai-seo
- **License**: MIT (this directory's LICENSE)
- **What domestication changed**: 9 defect(s) fixed, 6 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
