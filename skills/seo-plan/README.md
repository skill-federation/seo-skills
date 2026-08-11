# seo-plan

**Build-time SEO planning for 2026: turns a new site or product into a written build plan — architecture, server-rendering, semantics, per-page schema, Core Web Vitals budgets, E-E-A-T, content structure — before any live URL exists. Use it to structure a site for search from the start, not audit a running one. Encodes the 2026 baseline (FAQ retired, HowTo dead, INP not FID, crawlers that skip JavaScript) and verifies the plan it writes. Pair with geo-plan for AI-search citation.**

An original SkillFed skill, authored and era-verified for 2026. It is synthesized from this bundle's already-reviewed members ([`seo`](../seo/SKILL.md), [`geo-technical`](../geo-technical/SKILL.md), [`seo-validate`](../seo-validate/SKILL.md), [`claude-seo`](../claude-seo/SKILL.md), [`ai-seo`](../ai-seo/SKILL.md)) — every dated fact traces to a verified source, and the prose is our own. It teaches what to build; it inspects and scores nothing.

## Install

```bash
npx skills add skill-federation/seo-skills --skill seo-plan
```

## When to use it

- You are designing a site's SEO foundation before there is a deployed URL to inspect: choosing the URL scheme and hierarchy, deciding what renders on the server, mapping page types to schema, setting performance budgets, and settling the semantics, trust, and content rules that ship correctly the first time rather than being retrofitted after an audit finds them missing.
- Triggers: "SEO plan for a new site", "how should I structure this site for SEO", "technical SEO checklist 2026", "site architecture for SEO", "what schema should each page type carry", "what Core Web Vitals budget should we build to", "how do I set up E-E-A-T from the start".
- You want the plan itself to be checkable — a document where every page type has a rendering mode, a schema mapping, and a performance budget stated, so a reviewer (or a later audit) can hold the build to it.

## When NOT to use it

This skill plans what to build; it inspects and scores nothing. Route elsewhere when:

- There is already a live site to diagnose. For a scored, evidence-backed inspection of a deployed site, use geo-technical (the full eight-category live check) or geo-audit (the fast scored verdict); for a repository pre-ship validation, use seo-validate; for what AI crawlers actually did over time in server logs, use ai-bot-log-audit. seo-plan reads no site and emits no score.
- You need one tactic adjudicated against a specific site's evidence. ai-seo interviews a real site and pairs with an executing auditor to decide, per engine, which tactics that site should adopt. seo-plan is the general build-time framework that applies before a site exists, so there is no evidence to adjudicate against yet.
- The goal is AI-search / generative-engine citation — getting cited by ChatGPT, Perplexity, or Google AI Overviews. That is the job of the sibling skill geo-plan. seo-plan owns the traditional and technical SEO build (architecture, rendering, semantics, schema implementation, Core Web Vitals, crawlability, E-E-A-T); geo-plan owns AI-search citation strategy. The two meet only at structured data: seo-plan decides HOW each page type implements schema; geo-plan decides what to do with it for citation.

## Provenance & trust

Synthesized by SkillFed from the seo-skills bundle members: [`seo`](../seo/SKILL.md), [`geo-technical`](../geo-technical/SKILL.md), [`seo-validate`](../seo-validate/SKILL.md), [`claude-seo`](../claude-seo/SKILL.md), [`ai-seo`](../ai-seo/SKILL.md). MIT · last verified 2026-08-10. Every fact traces to a verified source (no invented claims); full attribution in [SKILL.md](SKILL.md).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
