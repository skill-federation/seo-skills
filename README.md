# seo-skills

**Everything an AI agent needs to plan, build, and prove out SEO and AI-search — in one non-conflicting bundle, current to 2026.**

Most SEO skills tell an agent what's wrong with a site that already exists. The harder, more valuable moment comes earlier: **how do you build the thing right in the first place** — so it ranks and gets cited by ChatGPT, Perplexity, and Google AI Overviews — without following tactics the platforms quietly retired?

This bundle now starts there. Two build-time planners lead, then seven skills take over once the site is live — nine in all, dividing the work by **role and lifecycle stage** rather than by topic, sharing one written-down 2026 baseline, and de-conflicted so they compose into a single toolchain instead of contradicting each other.

Bundle version `3d5634ce2d5f812b` · 9 skills · last verified 2026-08-10 · curated by [skillfed.io](https://skillfed.io)

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

## The nine skills

Divided by where they belong in the lifecycle — plan, then audit, then strategize and implement. Click through for the full document, its **Conditions** (when to use, when not, what breaks first), and its provenance.

| skill | stage | reach for it when |
|---|---|---|
| **[seo-plan](skills/seo-plan/SKILL.md)** | Build (technical) | You're building or rebuilding a site and want the SEO foundation right from the start — architecture, rendering, HTML semantics, per-page schema, Core Web Vitals budgets, E-E-A-T and trust, content structure. Produces a written build plan; inspects nothing. |
| **[geo-plan](skills/geo-plan/SKILL.md)** | Build (AI-search) | You're deciding what content and structure to create so AI search *cites* you — the 2026 GEO reality, per-engine behavior, what to build and what to skip. Plans; scores nothing. |
| **[geo-technical](skills/geo-technical/SKILL.md)** | Audit | A live site ranks nowhere or AI assistants never cite it — the full 8-category infrastructure inspection, /100. |
| **[geo-audit](skills/geo-audit/SKILL.md)** | Audit | You need a fast scored AI-crawler-legibility verdict in ~30 seconds before spending on content. |
| **[seo-validate](skills/seo-validate/SKILL.md)** | Audit | The pages live in a repository, not behind a URL — a framework-aware, read-only, CI-gating check before anything ships. |
| **[ai-bot-log-audit](skills/ai-bot-log-audit/SKILL.md)** | Evidence | A citation-gap theory needs server-log proof of what GPTBot, ClaudeBot, PerplexityBot and peers actually fetched. |
| **[ai-seo](skills/ai-seo/SKILL.md)** | Strategy | A *specific live site* needs its tactics adjudicated per engine, against real evidence — pairs with an auditor. |
| **[seo](skills/seo/SKILL.md)** | Implement | You're writing the markup — copy-paste JSON-LD, robots, canonical and hreflang, plus scripted Lighthouse / PageSpeed / Search Console measurement. |
| **[claude-seo](skills/claude-seo/SKILL.md)** | Suite | You want orchestrated, client-grade deliverables and will install its runtime — `/seo` commands, a doctor preflight, parallel audits, hard quality gates. |

## How they fit together

The lifecycle runs left to right; stop wherever you have your answer.

1. **seo-plan** / **geo-plan** — before a URL exists: turn "I'm building X" into a concrete, 2026-current build plan (technical foundation, and what earns AI citations).
2. **geo-audit → geo-technical** — once it's live: a 30-second scored gate, then the full inspection if the number is low.
3. **ai-seo** — the strategy layer that adjudicates, per engine, which tactics *this* site should adopt (it runs nothing, so pair it with an auditor above).
4. **seo** — the implementation reference to ship the markup and measure it.

Side doors: **seo-validate** when the pages live in your repo and you want a pre-ship check; **ai-bot-log-audit** when you need server-log evidence instead of a theory; **claude-seo** when the deliverable is a client-grade report suite.

## What makes these different

Two of the nine (**seo-plan**, **geo-plan**) are original skills we authored; the other seven are upgraded derivatives of the best community skills. Every one, authored or derived, is:

- **Era-verified to 2026** — retired rich-result types and unproven conventions are ruled out, not recommended.
- **Conditions-stated** — when to use it, when not, and what breaks first.
- **Verify-looped** — every workflow step (or, for the planners, the plan it produces) ends in a runnable check.
- **De-conflicted as a set** — the nine were reviewed together so they route to each other instead of overlapping.
- **Provenance-carrying** — derived skills name their upstream source and record what changed; the two authored skills state that every fact they teach traces to a verified skill in this bundle, in our own words, with nothing invented.

## The shared 2026 baseline

Every skill states these consistently, and each document carries its own dated pins:

- Google retired FAQ rich results for **every** site on **2026-05-07**.
- HowTo rich results have been **deprecated since September 2023**.
- `llms.txt` is a proposed convention at roughly **0.015% adoption** with no vendor confirmation — nothing here scores it or sells it.
- `Google-Extended` is the Gemini / AI-training opt-out; its effect on AI Overviews inclusion is **unverified**. Blocking `Googlebot` is what verifiably removes AI Overviews presence.

## Scope

**Covered.** The SEO-for-AI-search job across the lifecycle: two build-time planners (technical and AI-search) that plan but execute nothing; four auditors working different ground (a 30-second scored verdict, a deep live inspection, a read-only repo check, and server-log evidence); a per-engine strategy layer for existing sites; an implementation reference; and a front door to a full orchestrated toolchain.

**Deliberately not covered.** Writing or rewriting the content itself — this bundle plans, builds toward, audits, and strategizes; content production lives in a separate collection, precisely because the worst stale-tactic traps concentrate there. Keyword research, backlink analysis, and rank tracking exist only behind the toolchain's front door, and the tiers that reach a third-party vendor send your domains and keywords with the query — surfaced as an explicit decision, not a silent default. There is no skill promising AI-specific Search Console analytics, because Google ships no such reporting. Two adjacent jobs are queued, not covered: forensic traffic-drop diagnosis and a full site-migration workflow — until they land, the members here plan the build and read the current state, not the history.

## Provenance and licensing

Provenance is a feature of this bundle, not a footnote. Derived skills name their source in frontmatter (`derived_from`) and their **Attribution** section and ship its upstream license in their own directory; the two authored skills carry `synthesized_from` — the verified bundle members whose facts they restate. Every vendored file is pinned by sha256 in [`bundle.json`](bundle.json).

This bundle's documents are generated from a maintained source of truth and re-verified on a cadence; the `verified` date is when each skill's claims were last checked against its sources. A stamp dates a fact — it does not certify it.
