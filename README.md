# seo-skills

**Everything an AI agent needs to make a site findable and citable in 2026 — by Google and by AI answer engines — across the whole lifecycle, in one non-conflicting bundle.**

Most SEO skills tell an agent what's wrong with a site that already exists. The more valuable moments come earlier and run wider: deciding **which search terms to target and what content to create**, planning **how to build a site right** so it ranks and gets cited by ChatGPT, Perplexity, and Google AI Overviews, making a brand read as a recognizable **entity**, generating pages **at scale** without a thin-content penalty — and only then auditing, implementing, and measuring.

This bundle covers that whole arc. Thirteen skills divide the work by **role and lifecycle stage** rather than by topic, share one written-down 2026 baseline, and are de-conflicted so they compose into a single toolchain instead of contradicting each other.

Bundle version `b4c9fef88f69324f` · 13 skills · last verified 2026-08-10 · curated by [skillfed.io](https://skillfed.io)

## Install

Installs with the [`skills`](https://www.npmjs.com/package/skills) CLI, which reads this repo's `skills/<slug>/SKILL.md` layout directly from GitHub.

The whole bundle:

```bash
npx skills add skill-federation/seo-skills
```

One skill (repeat `--skill` for more):

```bash
npx skills add skill-federation/seo-skills --skill seo-plan
```

## The thirteen skills

Divided by where they belong in the lifecycle — strategy, then plan, then build, then audit, then implement. Click through for the full document, its **Conditions** (when to use, when not, what breaks first), and its provenance.

| skill | stage | reach for it when |
|---|---|---|
| **[keyword-strategy](skills/keyword-strategy/SKILL.md)** | Strategy | You're choosing which search terms to target — discovery, search-intent, clustering, and prioritization into a topical map. The standalone method (works with just autocomplete + a browser); the tool-driven version rides claude-seo. |
| **[content-strategy](skills/content-strategy/SKILL.md)** | Strategy | You're deciding *what content to create* — pillars, topic clusters, content types, and a prioritized editorial plan. Plans the program; it does not write the copy. |
| **[seo-plan](skills/seo-plan/SKILL.md)** | Build (technical) | You're building or rebuilding a site and want the SEO foundation right from the start — architecture, rendering, HTML semantics, per-page schema, Core Web Vitals budgets, E-E-A-T and trust, content structure. Produces a written build plan; inspects nothing. |
| **[geo-plan](skills/geo-plan/SKILL.md)** | Build (AI-search) | You're deciding what content and structure to create so AI search *cites* you — the 2026 GEO reality, per-engine behavior, what to build and what to skip. Plans; scores nothing. |
| **[entity-seo](skills/entity-seo/SKILL.md)** | Build (authority) | You want your brand, products, and authors to read as recognizable *entities* in search's knowledge systems — entity signals, Organization/Person identity, the Knowledge Graph reality. |
| **[programmatic-seo](skills/programmatic-seo/SKILL.md)** | Build (scale) | You're generating SEO pages at scale from templates + data — the 12 playbooks, unique-value-per-page, and how to avoid the thin-content and doorway-page penalties. |
| **[geo-audit](skills/geo-audit/SKILL.md)** | Audit | You need a fast scored AI-crawler-legibility verdict in ~30 seconds before spending on content. |
| **[geo-technical](skills/geo-technical/SKILL.md)** | Audit | A live site ranks nowhere or AI assistants never cite it — the full 8-category infrastructure inspection, /100. |
| **[seo-validate](skills/seo-validate/SKILL.md)** | Audit | The pages live in a repository, not behind a URL — a framework-aware, read-only, CI-gating check before anything ships. |
| **[ai-bot-log-audit](skills/ai-bot-log-audit/SKILL.md)** | Evidence | A citation-gap theory needs server-log proof of what GPTBot, ClaudeBot, PerplexityBot and peers actually fetched. |
| **[ai-seo](skills/ai-seo/SKILL.md)** | Strategy (per-site) | A *specific live site* needs its tactics adjudicated per engine, against real evidence — pairs with an auditor. |
| **[seo](skills/seo/SKILL.md)** | Implement | You're writing the markup — copy-paste JSON-LD, robots, canonical and hreflang, plus scripted Lighthouse / PageSpeed / Search Console measurement. |
| **[claude-seo](skills/claude-seo/SKILL.md)** | Suite | You want orchestrated, client-grade deliverables and will install its runtime — `/seo` commands, a doctor preflight, parallel audits, hard quality gates. |

## How they fit together

The lifecycle runs top to bottom; stop wherever you have your answer.

1. **keyword-strategy → content-strategy** — before you build anything: decide which terms to target, then what content to create around them.
2. **seo-plan / geo-plan** — before a URL exists: turn "I'm building X" into a concrete, 2026-current build plan (technical foundation, and what earns AI citations).
3. **entity-seo / programmatic-seo** — build techniques layered on the plan: read as a recognizable entity; generate templated pages at scale without a thin-content penalty.
4. **geo-audit → geo-technical** — once it's live: a 30-second scored gate, then the full inspection if the number is low.
5. **ai-seo** — the per-site strategy layer that adjudicates, per engine, which tactics *this* site should adopt (it runs nothing, so pair it with an auditor above).
6. **seo** — the implementation reference to ship the markup and measure it.

Side doors: **seo-validate** when the pages live in your repo and you want a pre-ship check; **ai-bot-log-audit** when you need server-log evidence instead of a theory; **claude-seo** when the deliverable is a client-grade report suite (and for tool-driven keyword/audit work behind an installed runtime).

## What makes these different

Two of the thirteen (**seo-plan**, **geo-plan**) are original skills we authored; the other eleven are upgraded derivatives of the best community skills. Every one, authored or derived, is:

- **Era-verified to 2026** — retired rich-result types, unproven conventions, and undated boost-statistics are ruled out, not recommended.
- **Conditions-stated** — when to use it, when not, and what breaks first.
- **Verify-looped** — every workflow step (or, for the planners and strategists, the plan it produces) ends in a runnable check.
- **De-conflicted as a set** — the thirteen were reviewed together so they route to each other instead of overlapping.
- **Provenance-carrying** — derived skills name their upstream source and record what changed; the two authored skills state that every fact they teach traces to a verified skill in this bundle, in our own words, with nothing invented. Where a derived skill ships a corrected reference file, the upstream original is pinned by hash.

## The shared 2026 baseline

Every skill states these consistently, and each document carries its own dated pins:

- Google retired FAQ rich results for **every** site on **2026-05-07**.
- HowTo rich results have been **deprecated since September 2023**.
- `llms.txt` is a proposed convention at roughly **0.015% adoption** with no vendor confirmation — nothing here scores it or sells it.
- Mass-produced, near-duplicate template pages fall under Google's **scaled-content-abuse** policy, and city-swapped location pages are demoted as **doorway pages** — the strategy and build skills plan around this, they do not chase it.
- `Google-Extended` is the Gemini / AI-training opt-out; its effect on AI Overviews inclusion is **unverified**. Blocking `Googlebot` is what verifiably removes AI Overviews presence.

## Scope

**Covered.** Making a site findable and citable in 2026 across the whole lifecycle: choosing which search terms to target and which content to create; planning a new site's technical foundation and its AI-citation strategy before a URL exists; making a brand, its products, and its authors read as recognizable entities; generating templated pages at scale without a thin-content penalty; implementing markup and running scripted audits; and inspecting a live or pre-ship site from eight angles down to what AI crawlers actually fetched.

**Deliberately not covered.** Writing or rewriting the finished copy — this bundle plans *what* content to create and *how* to structure it, but content production (the actual drafting) lives in a separate collection, precisely because the worst stale-tactic traps concentrate there. The bundle is also not the raw keyword / backlink / rank-tracking **tool** itself: where those are driven, they run on the user's own toolchain and accounts, behind `claude-seo`'s front door, and the tiers that reach a third-party vendor send your domains and keywords with the query — surfaced as an explicit decision, not a silent default. There is no skill promising AI-specific Search Console analytics, because Google ships no such reporting. Two adjacent jobs are queued, not covered: forensic traffic-drop diagnosis and a full site-migration workflow.

## Provenance and licensing

Provenance is a feature of this bundle, not a footnote. Derived skills name their source in frontmatter (`derived_from`) and their **Attribution** section and ship its upstream license in their own directory; the two authored skills carry `synthesized_from` — the verified bundle members whose facts they restate. Every vendored file is pinned by sha256 in [`bundle.json`](bundle.json); a reference we corrected also records the upstream original's hash, so any edit is auditable.

This bundle's documents are generated from a maintained source of truth and re-verified on a cadence; the `verified` date is when each skill's claims were last checked against its sources. A stamp dates a fact — it does not certify it.
