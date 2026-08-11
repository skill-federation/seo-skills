# seo-skills

**SEO skills for AI agents — domesticated.** Each skill here is a reviewed, upgraded derivative
of one of the best community SEO skills: era-verified against dated platform reality,
conditions-stated (when to use, when not, what breaks first), verify-looped (every workflow
step ends in a runnable check), defect-fixed, and attribution-carrying. The originals'
mechanics are retained; what changed is recorded in each skill's **Findings** and
**Attribution** sections.

Bundle version `4e9dd6074ced64a1` · 7 skills · last verified 2026-08-10 · curated by [skillfed.io](https://skillfed.io)

## Install

One skill:

```bash
npx skillfed install skill-federation/seo-skills/geo-technical
```

Or the whole bundle with any `skills/`-convention consumer:

```bash
npx skills add skill-federation/seo-skills
```

## The skills

| skill | what it does | derived from | license | verified |
|---|---|---|---|---|
| **[geo-technical](skills/geo-technical/SKILL.md)** | Score a live site's readiness to be read by machines: fetch raw HTML, hold it against the browser render, and grade eight infrastructure categories out of 100 before any content or GEO work starts. Use when pages rank nowhere, AI assistants never cite the site, or a JavaScript framework may be hiding the copy from crawlers. Era-stamped for 2026 — retired rich-result types and unproven conventions stay out of the score. | [zubair-trabzada/geo-seo-claude/geo-technical](https://github.com/zubair-trabzada/geo-seo-claude) | MIT | 2026-08-10 |
| **[ai-seo](skills/ai-seo/SKILL.md)** | The GEO/AEO strategy layer for agents, current to Google's 2026 guidance split: answer features ride core ranking while ChatGPT, Claude, and Perplexity reward extractable structure. Load it when planning how a site earns AI citations, before any page edits. It interviews, adjudicates tactics per engine, and emits an evidence-tagged plan; it executes nothing, so pair it with an audit skill that actually fetches the site. | [coreyhaines31/marketingskills/ai-seo](https://github.com/coreyhaines31/marketingskills) | MIT | 2026-08-10 |
| **[seo-validate](skills/seo-validate/SKILL.md)** | Repo-reading pre-ship SEO audit for source code: detects the framework first, then applies framework-conditioned rules with severity and definitive-vs-heuristic confidence labels; strictly read-only. Reach for it when the pages to check live in a codebase rather than behind a live URL. Era-adjudicated 2026: retired FAQ/HowTo rich-result guidance excised, GEO checks demoted to hypothesis. | [softspark/ai-toolkit/seo-validate](https://github.com/softspark/ai-toolkit) | Apache-2.0 | 2026-08-10 |
| **[ai-bot-log-audit](skills/ai-bot-log-audit/SKILL.md)** | Method for reading Apache and Nginx access-log evidence to establish what GPTBot, ClaudeBot, PerplexityBot and peers actually fetch, skip, or error on, and which fixes each fetch pattern calls for. Reach for it when a citation-gap theory needs log rows behind it and you can export the raw logs. Domesticated 2026-08; the bot roster is carried from the wild source's 2026 table, not independently re-checked. | [guia-matthieu/clawfu-skills/ai-bot-log-audit](https://github.com/guia-matthieu/clawfu-skills) | MIT | 2026-08-10 |
| **[geo-audit](skills/geo-audit/SKILL.md)** | A scored technical audit of whether a live domain is legible to AI-search crawlers, current to 2026: one stdlib Python script, about 30 seconds, five load-bearing checks (robots.txt bot access, pre-JS rendering, sitemap, JSON-LD, internal links) with llms.txt reported as informational only. Reach for it when a site needs a fast numeric verdict on AI-crawler visibility before content spend; it refuses to emit numbers when the script cannot run or the domain will not resolve. | [vellum-ai/vellum-assistant/geo-audit](https://github.com/vellum-ai/vellum-assistant) | MIT | 2026-08-10 |
| **[seo](skills/seo/SKILL.md)** | Era-checked implementation reference and audit workflow for technical SEO and answer-engine (AEO) visibility, current to 2026: copy-paste JSON-LD, robots, canonical and hreflang blocks, vendored Lighthouse, PageSpeed and Search Console scripts, plus a load-bearing llms.txt caution. Reach for it when building or reviewing a site's markup, crawlability, or AI-citation posture; it will not recommend retired rich-result types. | [addyosmani/web-quality-skills/seo](https://github.com/addyosmani/web-quality-skills) | MIT | 2026-08-10 |
| **[claude-seo](skills/claude-seo/SKILL.md)** | Front door for a bundled SEO toolchain: /seo commands route bundled Python through the claude-seo launcher, with a doctor preflight and parallel full audits whose conditional specialists spawn only when site signals warrant them. Use it when an agent must produce client-grade SEO reports under 2026 rules — FAQ rich results retired, HowTo schema dead, llms.txt unproven — behind hard quality gates and with zero promotional content in deliverables. | [AgriciDaniel/claude-seo/seo](https://github.com/AgriciDaniel/claude-seo) | MIT | 2026-08-10 |

## Suggested install order

1. **geo-technical** — the full technical audit (start here for any live site)
2. **ai-seo** — the strategy layer (pair it with an executing audit; its Conditions say so)
3. **seo-validate** — when the SEO lives in your repo (pre-ship, CI-gating)
4. **ai-bot-log-audit** — the moment you need evidence instead of a theory
5. **geo-audit** — the 30-second scored check (escalates to geo-technical)
6. **seo** — the markup implementation reference + scripted Lighthouse/PSI/GSC loop
7. **claude-seo** — the orchestrated multi-specialist suite, when toolchain setup is warranted

## Shared era facts

Every skill in this bundle states these consistently (each document carries its own dated pins):

- Google retired FAQ rich results for every site on **2026-05-07**
- HowTo rich results have been **deprecated since September 2023**
- `llms.txt` is a proposed convention at roughly **0.015% adoption** with no vendor confirmation
- `Google-Extended` is the Gemini/AI-training opt-out; its effect on AI Overviews inclusion is **unverified** — blocking `Googlebot` is what verifiably removes AI Overviews presence

## Coverage note (founder-facing draft)

**What this collection covers.** Seven skills that divide the SEO-for-AI-search job by role
rather than by topic. One strategy layer (ai-seo) decides which tactics belong to which engine
and produces an evidence-tagged plan — it deliberately runs nothing. Three auditors execute
against different ground: geo-audit gives a scored verdict on a live domain in about thirty
seconds, geo-technical inspects a live site across eight infrastructure categories, and
seo-validate reads your repository before anything ships. ai-bot-log-audit replaces theory with
server-log evidence of what AI crawlers actually fetch. seo is the implementation reference —
copy-paste markup, robots and hreflang blocks, and scripted Lighthouse/PageSpeed/Search Console
measurement for sites you control. claude-seo is the front door to a full toolchain when you
want orchestrated, client-grade deliverables and are willing to install its runtime. All seven
share one 2026 baseline, written down rather than assumed: Google retired FAQ rich results in
May 2026, HowTo schema has been dead since 2023, and llms.txt remains an unproven convention
that nothing here scores or sells.

**What it deliberately does not cover.** Writing or rewriting the content itself — this
collection structures, audits, and plans; content production lives in the writing collection,
precisely because the worst stale-tactic traps concentrate there. Keyword research, backlink
analysis, and rank tracking exist only behind the toolchain's front door — backlink analysis and
SERP-based keyword clustering as core suite commands (`/seo backlinks`, with a keyless Common
Crawl tier; `/seo cluster`; `/seo content-brief`), rank tracking via extensions — and the tiers
that reach a third-party vendor send your domains and keywords with the query, a trade the suite
surfaces for an explicit egress decision, not a default. There is no skill promising AI-specific Search Console analytics, because Google ships
no such reporting — anything claiming otherwise would be selling you a dashboard for data that
does not exist. Two adjacent jobs are queued rather than covered today: forensic traffic-drop
diagnosis (why did rankings fall, and when) and a site-migration workflow; until they land, the
auditors here tell you the current state, not the history.

## Provenance and licensing

Every skill names its sources in its frontmatter (`derived_from`) and its **Attribution**
section, ships its upstream license in its own directory, and pins every vendored file by
sha256. Zero-text provenance entries (`superseded`, `sibling`) record family relationships —
no text was taken from them. This bundle's documents are generated from a maintained source
of truth and re-verified on a cadence; the `verified` date on each skill is the date its
claims were last checked against its sources.
