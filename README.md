# seo-skills

**Everything an AI agent needs to make a site legible to AI search — in one non-conflicting bundle, current to 2026.**

The community has published dozens of overlapping SEO and GEO skills. Their quality is uneven, and many still ship tactics that Google has since retired — FAQ rich results, HowTo schema, `llms.txt` treated as a ranking factor — so an agent that grabs the wrong one can quietly follow stale advice. Picking well means reading all of them.

We did that. We pulled every available SEO/GEO skill from the federation catalog, clustered them by the job they actually do, reviewed the cluster, and kept the single best skill in each role. Then we upgraded each one — verified against 2026 platform reality, stated its conditions, ended every workflow step in a runnable check, fixed defects, and carried its attribution — and de-conflicted the set so the seven compose into one toolchain instead of contradicting each other.

The result is **7 skills that divide the work by role, share one written-down 2026 baseline, and don't step on each other.**

Bundle version `4e9dd6074ced64a1` · last verified 2026-08-10 · curated by [skillfed.io](https://skillfed.io)

## Install

Installs with the [`skills`](https://www.npmjs.com/package/skills) CLI, which reads this repo's `skills/<slug>/SKILL.md` layout directly from GitHub.

The whole bundle:

```bash
npx skills add skill-federation/seo-skills
```

One skill (repeat `--skill` for more):

```bash
npx skills add skill-federation/seo-skills --skill geo-technical
```

## The seven skills

Each divides the job by role, not by topic. Click through for the full document, its **Conditions** (when to use, when not, what breaks first), and its **Findings** and **Attribution**.

| skill | role | reach for it when | source | license |
|---|---|---|---|---|
| **[geo-audit](skills/geo-audit/SKILL.md)** | Fast scored verdict | You need a numeric AI-crawler-visibility read in ~30s before spending on content — one stdlib Python script, five load-bearing checks. Escalates to geo-technical. | [vellum-ai/vellum-assistant](https://github.com/vellum-ai/vellum-assistant) | MIT |
| **[geo-technical](skills/geo-technical/SKILL.md)** | Deep live-site audit | Pages rank nowhere or AI assistants never cite the site — grades 8 infrastructure categories out of 100, holding raw HTML against the rendered DOM. | [zubair-trabzada/geo-seo-claude](https://github.com/zubair-trabzada/geo-seo-claude) | MIT |
| **[seo-validate](skills/seo-validate/SKILL.md)** | Repo pre-ship audit | The pages live in a codebase, not behind a URL — framework-aware, read-only, with severity and definitive-vs-heuristic confidence labels. | [softspark/ai-toolkit](https://github.com/softspark/ai-toolkit) | Apache-2.0 |
| **[ai-bot-log-audit](skills/ai-bot-log-audit/SKILL.md)** | Server-log evidence | A citation-gap theory needs data — reads access logs to show what GPTBot, ClaudeBot, PerplexityBot and peers actually fetch, skip, or error on. | [guia-matthieu/clawfu-skills](https://github.com/guia-matthieu/clawfu-skills) | MIT |
| **[ai-seo](skills/ai-seo/SKILL.md)** | Strategy layer | Planning how a site earns AI citations, before any edits — adjudicates tactics per engine and emits an evidence-tagged plan. Executes nothing; pair with an auditor. | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills) | MIT |
| **[seo](skills/seo/SKILL.md)** | Implementation reference | Building or reviewing markup — copy-paste JSON-LD, robots, canonical and hreflang blocks, plus scripted Lighthouse / PageSpeed / Search Console measurement. | [addyosmani/web-quality-skills](https://github.com/addyosmani/web-quality-skills) | MIT |
| **[claude-seo](skills/claude-seo/SKILL.md)** | Full toolchain front door | You want orchestrated, client-grade reports and will install its runtime — `/seo` commands, a doctor preflight, parallel audits, hard quality gates. | [AgriciDaniel/claude-seo](https://github.com/AgriciDaniel/claude-seo) | MIT |

## How they fit together

A typical live-site engagement moves down this path; stop wherever you have your answer.

1. **geo-audit** — 30-second scored gate. Is this site even legible to AI crawlers?
2. **geo-technical** — when the gate fails or the number is low: the full 8-category diagnosis.
3. **ai-seo** — the strategy layer that turns findings into a per-engine, evidence-tagged plan (it runs nothing, so pair it with one of the auditors above).
4. **seo** — the implementation reference to actually ship the markup and measure it.

Two side doors:

- **seo-validate** when the pages live in your repo and you want a read-only, framework-aware check before anything ships (CI-friendly).
- **ai-bot-log-audit** the moment you need server-log evidence instead of a theory about what the crawlers do.
- **claude-seo** when the deliverable is a client-grade report suite and the toolchain setup is warranted.

## What "upgraded" means

Every skill here is one wild skill made trustworthy — never a topic blend. Against its source, each was:

- **Era-verified to 2026** — retired rich-result types and unproven conventions are scored out, not recommended.
- **Conditions-stated** — when to use it, when not, and what breaks first.
- **Verify-looped** — every workflow step ends in a runnable check.
- **Defect-fixed** — bugs in the original mechanics corrected; the mechanics themselves retained.
- **Attribution-carrying** — every change is recorded, with its reason, in the skill's own **Findings** and **Attribution** sections.

## The shared 2026 baseline

Every skill states these consistently, and each document carries its own dated pins:

- Google retired FAQ rich results for **every** site on **2026-05-07**.
- HowTo rich results have been **deprecated since September 2023**.
- `llms.txt` is a proposed convention at roughly **0.015% adoption** with no vendor confirmation — nothing here scores it or sells it.
- `Google-Extended` is the Gemini / AI-training opt-out; its effect on AI Overviews inclusion is **unverified**. Blocking `Googlebot` is what verifiably removes AI Overviews presence.

## Scope

**Covered.** The SEO-for-AI-search job split by role: one strategy layer that plans but executes nothing; three auditors working different ground (a 30-second scored verdict, a deep live-site inspection, and a read-only repo check); a server-log evidence method; an implementation reference for sites you control; and a front door to a full orchestrated toolchain.

**Deliberately not covered.** Writing or rewriting the content itself — this bundle structures, audits, and plans; content production lives in a separate collection, precisely because the worst stale-tactic traps concentrate there. Keyword research, backlink analysis, and rank tracking exist only behind the toolchain's front door (`/seo backlinks`, `/seo cluster`, `/seo content-brief`, rank tracking via extensions) — and the tiers that reach a third-party vendor send your domains and keywords with the query, surfaced as an explicit egress decision rather than a silent default. There is no skill promising AI-specific Search Console analytics, because Google ships no such reporting; anything claiming otherwise would sell you a dashboard for data that does not exist. Two adjacent jobs are queued, not covered: forensic traffic-drop diagnosis and a site-migration workflow. Until they land, the auditors here report the current state, not the history.

## Provenance and licensing

Provenance is a feature of this bundle, not a footnote. Every skill names its sources in its frontmatter (`derived_from`) and its **Attribution** section, ships its upstream license in its own directory, and pins every vendored file by sha256. Zero-text provenance entries (`superseded`, `sibling`) record family relationships only — no text was taken from them.

This bundle's documents are generated from a maintained source of truth and re-verified on a cadence; the `verified` date is the date each skill's claims were last checked against its sources. A stamp dates a fact — it does not certify it.
