# geo-plan

**Build-time GEO and answer-engine planning, current to 2026: decide what content and site structure to create so AI search (ChatGPT, Perplexity, Google AI Overviews, Claude) cites you — applied before a live site exists to audit. Emits a build plan naming the engine each item targets and a skip list for what is dead or unproven. It plans only: it fetches, renders, scores and audits nothing.**

An original SkillFed skill, authored and era-verified for 2026. It is synthesized from this bundle's already-reviewed members ([`ai-seo`](../ai-seo/SKILL.md), [`geo-technical`](../geo-technical/SKILL.md), [`ai-bot-log-audit`](../ai-bot-log-audit/SKILL.md), [`geo-audit`](../geo-audit/SKILL.md), [`seo`](../seo/SKILL.md)) — every dated fact traces to a verified source, and the prose is our own. It teaches what to build; it inspects and scores nothing.

## Install

```bash
npx skills add skill-federation/seo-skills --skill geo-plan
```

## When to use it

- You are **building or planning** content, a page, or a whole site whose goal is
  to be cited by AI search — ChatGPT, Perplexity, Google AI Overviews, Claude,
  Gemini, Copilot — and there is not yet a live site to inspect.
- You need the 2026 reality settled before you commit effort: which bets pay off,
  which are cosmetic, and which will actively cost you.
- Triggers this skill answers: "how do I get cited by ChatGPT or Perplexity",
  "GEO strategy for a new site", "AI SEO checklist for 2026", "build content that
  AI search cites", "what schema and structure should this new page ship with",
  "how do I get cited on Perplexity vs Claude vs Google".
- You want a written build plan whose every item is scoped to the engine it
  targets and grounded in a dated fact, so a builder can execute it and a
  reviewer can check it.

## When NOT to use it

- **To audit or diagnose a site that already exists.** That question needs
  evidence about *your specific* deployment, and this skill gathers none.
  **geo-plan plans what to build; it inspects and scores nothing.** Route the
  live-site work to the skill that fetches the evidence:
  - a full technical inspection of a deployed site → **geo-technical**;
  - a fast scored read on AI-crawler legibility → **geo-audit**;
  - what AI crawlers actually fetched, skipped, or errored on → **ai-bot-log-audit**
    (it reads your server access logs);
  - which tactics apply to *your* site given that evidence → **ai-seo**.
- **For the traditional and technical SEO build — site architecture, schema
  implementation, Core Web Vitals budgets, the crawlability foundation — that is
  the sibling build-time skill **seo-plan**.** geo-plan owns AI-search and citation
  strategy; seo-plan owns the traditional and technical build; the two are
  build-time siblings that overlap only where structured data serves citation. If
  you landed here to plan a whole new site and want the foundation, start with
  seo-plan and pair this one for the citation layer.
- **The seam with ai-seo, stated plainly.** ai-seo adjudicates which tactics fit
  one specific site given its evidence, and it is built to pair with an executing
  audit that fetches that site. geo-plan is the general, build-time framework you
  apply *before* a site exists to audit — no site, no evidence, no adjudication of
  a particular deployment. When you have a live site and want a per-site call, use
  ai-seo; when you are deciding what to build in the first place, use this.
- For writing the actual JSON-LD, robots rules, or render config once the plan
  says to — that implementation reference is **seo**.
- As proof of anything about a running site. A plan is a set of hypotheses about
  what to build; it becomes fact only after something is built and an executing
  skill measures it.

## Provenance & trust

Synthesized by SkillFed from the seo-skills bundle members: [`ai-seo`](../ai-seo/SKILL.md), [`geo-technical`](../geo-technical/SKILL.md), [`ai-bot-log-audit`](../ai-bot-log-audit/SKILL.md), [`geo-audit`](../geo-audit/SKILL.md), [`seo`](../seo/SKILL.md). MIT · last verified 2026-08-10. Every fact traces to a verified source (no invented claims); full attribution in [SKILL.md](SKILL.md).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
