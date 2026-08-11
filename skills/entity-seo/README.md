# entity-seo

**Entity and topical-authority strategy for SEO, current to 2026: make a brand, its products, and its authors read as distinct, recognizable entities in search engines' knowledge systems. Plan stable-@id Organization and Person identity, cross-touchpoint name/logo/description consistency, and the sameAs and Wikidata signals that strengthen how AI search identifies and cites a brand. Use it to decide entity strategy — not to write JSON-LD (that is the seo reference) or audit a live site.**

An upgraded, era-verified, defect-fixed derivative of [`kostja94/marketing-skills/entity-seo`](https://github.com/kostja94/marketing-skills), checked against platform reality current to 2026 (the kind of dated facts a wild skill silently predates). Conditions are stated, and every workflow step ends in a runnable check.

## Install

```bash
npx skills add skill-federation/seo-skills --skill entity-seo
```

## When to use it

- Deciding the entity strategy for a brand, its products, and its authors: which identity signals to ship so search and AI systems recognize each as one distinct entity.
- Planning stable-@id Organization and Person identity, cross-touchpoint name/logo/description consistency, and the sameAs / Wikidata signals that corroborate an entity.
- Triggers: "entity SEO", "entity optimization", "Knowledge Graph", "Knowledge Panel", "brand entity", "entity signals", "entity linking", "how do I make my brand a recognized entity", "topical authority".

## When NOT to use it

- Writing the actual JSON-LD (Organization, Person, or any other type) — that is the implementation reference seo.
- Mapping which page type carries which schema across a site, or building the E-E-A-T layer — that build work is seo-plan's; entity signals support E-E-A-T but are not the build layer.
- Planning AI-search citation strategy (per-engine selection logic, content blocks, the citation ladder) — that is geo-plan. This document supplies only the entity signals that strengthen citation.
- Auditing a live site or scoring a deployment — this skill plans entity strategy and writes an artifact; it fetches and scores nothing.

## Provenance & trust

Derived from [`kostja94/marketing-skills/entity-seo`](https://github.com/kostja94/marketing-skills) · MIT · last verified 2026-08-10. Attribution is in [SKILL.md](SKILL.md)'s Attribution section; every vendored file is pinned by sha256 in the bundle's [`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
