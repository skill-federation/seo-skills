---
name: claude-seo
description: 'Front door for a bundled SEO toolchain: /seo commands route bundled Python through the claude-seo
  launcher, with a doctor preflight and parallel full audits whose conditional specialists spawn only
  when site signals warrant them. Use it when an agent must produce client-grade SEO reports under 2026
  rules — FAQ rich results retired, HowTo schema dead, llms.txt unproven — behind hard quality gates and
  with zero promotional content in deliverables.'
license: MIT
treatment: derivative
derived_from:
- id: AgriciDaniel/claude-seo/seo
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: 5db52596dcc89608765afd9383e8ad81fb1e3768cb8c7c23275b2fe714efd421
- id: AgriciDaniel/codex-seo/seo
  role: sibling
  license_at_derivation: NOASSERTION
  content_hash_at_derivation: 186470fe99a1cc7ee43151be743117080865f44c3abebdf5cd8782fea3f52c0b
- id: AgriciDaniel/claude-seo/seo-audit
  role: sibling
  license_at_derivation: MIT
  content_hash_at_derivation: badb9495a725a07beed4957e8b1ec1732ecb48312002d64babb0ff710e278170
- id: AgriciDaniel/codex-seo/seo-audit
  role: sibling
  license_at_derivation: NOASSERTION
  content_hash_at_derivation: 7c5ed6805efbe63ff0e91588bffd46ef653836d04348151145e6780219e3839e
targeted_version: 2.2.4
last_verified_at: 2026-08-10
---

# claude-seo — SEO toolchain front door

The SkillFed domesticated derivative of `AgriciDaniel/claude-seo/seo` (upstream v2.2.4, MIT). The wild skill's terminal name is `seo`, but users know this suite by its repository and launcher name — so `claude-seo` is the slug here, and a same-batch implementation reference keeps `seo`. The command surface is unchanged: this is the front door that orchestrates the suite's sub-skills and sub-agents, runs bundled Python through an isolated launcher, and enforces the quality gates its upstream is known for.

## Conditions

### When to use

- You want one front door over a full SEO toolchain: 20+ `/seo` commands backed by bundled Python tools, with parallel sub-agent fan-out for full site audits and a unified 0–100 health score.
- You are producing client-grade deliverables (site audits, technical reports, strategic plans) and want hard, enforced quality gates — location-page hard stops, retired-schema refusals — rather than advisory prose.
- The site's business type is unknown up front: the skill detects SaaS / local / e-commerce / publisher / agency signals from the homepage and spawns only the matching specialists.

### When NOT to use

- For a single quick scored check or a repo-level pre-ship validation: a narrower single-purpose skill costs less than this suite's runtime setup.
- For a one-off full technical audit where toolchain setup isn't warranted: a standalone curl-based audit (geo-technical in this bundle) covers the live eight-category inspection with nothing to install beyond a shell.
- For forensic traffic-drop diagnosis ("why did rankings fall last month") — out of scope across this bundle. `/seo drift` only compares against a baseline captured before the change, and seo-google's organic-traffic trends are data, not a forensic method; neither reconstructs a past you didn't baseline.
- On machines where an isolated Python runtime and Chromium cannot be installed — the bundled tools will not run and the skill degrades to unverified prose.
- When policy forbids sending site or keyword data to third-party vendors and the task depends on the extensions: every extension (Firecrawl, DataForSEO, image-gen, Ahrefs, Bing, Profound, SE Ranking, Unlighthouse) calls a third-party API.

### Prerequisites

- The upstream toolchain itself. This bundle ships the front door document (plus references and license) only: the launcher, the bundled Python tools, and the 24 sub-skills it orchestrates come from installing the upstream repository — https://github.com/AgriciDaniel/claude-seo — as a plugin or a repo checkout. Acquire that first; nothing in this bundle provides it. The doctor preflight below verifies the acquisition before anything else runs.
- The `claude-seo` launcher. Plugin installs expose it automatically; repository users run `./bin/claude-seo`; manual installers rewrite the command to the isolated launcher path. Run bundled Python tools only through `claude-seo run <script.py>`. Never invoke bundled scripts with a bare Python interpreter.
- An isolated Python runtime plus Chromium, created only on explicit `/seo setup` (or an explicit repair request). If any `claude-seo run` command reports that setup is required, suggest `/seo setup` — do not improvise a `pip install`, and do not fall back to global or user package installation.
- Optional, feature-gating: Google API credentials (`claude-seo run google_auth.py --check`), backlink API keys (`claude-seo run backlinks_auth.py --check`), a DataForSEO MCP, a Firecrawl MCP.
- Extensions require their own installers (each extension's `install.sh` / `install.ps1`) plus third-party accounts — and every extension call sends the URLs, keywords, or log-derived queries you are analyzing to that vendor's servers. Treat this as data egress: get sign-off before enabling any extension on a client engagement.

### What breaks first

- The runtime, loudly: bundled scripts invoked outside the launcher, or a missing Chromium, stop commands cold. Run the doctor preflight (below) before an engagement; this suite fails before it misleads.
- Schema recommendations, silently: FAQ/HowTo/llms.txt status is the category's fastest-rotting ground. The gates below pin their 2026 status; if you read this long after the last-verified date, re-check those pins first.
- Extension integrations: vendor auth schemes, rate limits (DataForSEO caps at 2,000 API calls/minute per `references/maps-api-endpoints.md`), and pricing change without notice.
- Programmatic location-page expansion: the 30-page warning and 50-page hard stop fire. A fired gate is the system working, not an obstacle to route around.

## Era

This derivative targets upstream v2.2.4 (repo `AgriciDaniel/claude-seo`), reviewed 2026-08-10. The dated facts it enforces:

- Google retired FAQ rich results for all sites on May 7, 2026 — no SERP feature remains for any site, superseding the Aug 2023 gov/health restriction. FAQPage AI-citation benefit is unconfirmed; do not claim it.
- Never recommend HowTo schema (deprecated Sept 2023): Google stopped showing how-to rich results then and never brought them back.
- llms.txt is a proposed convention at roughly 0.015% adoption with no vendor confirmation. The seo-geo fan-out reports llms.txt presence with zero citation weight — the file is never counted as a citation-ranking lever, though upstream may still note it under accessibility checks and optional low-effort fixes.
- All Core Web Vitals work uses INP, never FID: INP replaced FID as the interactivity metric on March 12, 2024, and FID left Chrome's field tooling in September 2024 (`references/cwv-thresholds.md`).
- E-E-A-T evaluation follows the September 11, 2025 Quality Rater Guidelines update (`references/eeat-framework.md`).

## Runtime and launcher

**Invocation:** `/seo $1 $2` where `$1` is the command and `$2` is the URL or argument.

Run setup only when the user explicitly invokes `/seo setup` or explicitly asks to repair dependencies. Execute `claude-seo setup`, report core and Chromium status separately, and do not fall back to global or user package installation.

### Verify

```bash
claude-seo doctor --json
```

Checks runtime readiness without changing the system. The output intentionally omits absolute paths and environment values — that is a design decision, not missing data. Expect per-component status for the core runtime and for Chromium; any setup-required result routes to `/seo setup`, never to an ad-hoc package install. Run this before every client engagement and whenever a `claude-seo run` command errors.

## Command surface

| Command | What it does |
|---------|-------------|
| `/seo audit <url>` | Full website audit with parallel subagent delegation |
| `/seo page <url>` | Deep single-page analysis |
| `/seo sitemap <url or generate>` | Analyze or generate XML sitemaps |
| `/seo schema <url>` | Detect, validate, and generate Schema.org markup |
| `/seo images <url or optimize>` | Image SEO: on-page audit, SERP analysis, file optimization |
| `/seo technical <url>` | Technical SEO audit (9 categories) |
| `/seo content <url>` | E-E-A-T and content quality analysis |
| `/seo content-brief <topic or url>` | Generate detailed SEO content brief with target keywords, outline, internal links |
| `/seo geo <url>` | AI Overviews / Generative Engine Optimization |
| `/seo plan <business-type>` | Strategic SEO planning |
| `/seo programmatic [url\|plan]` | Programmatic SEO analysis and planning |
| `/seo competitor-pages [url\|generate]` | Competitor comparison page generation |
| `/seo local <url>` | Local SEO analysis (GBP, citations, reviews, map pack) |
| `/seo maps [command] [args]` | Maps intelligence (geo-grid, GBP audit, reviews, competitors) |
| `/seo hreflang [url]` | Hreflang/i18n SEO audit and generation |
| `/seo google [command] [url]` | Google SEO APIs (GSC, PageSpeed, CrUX, Indexing, GA4) |
| `/seo backlinks <url>` | Backlink profile analysis (free: Moz, Bing, CC; premium: DataForSEO) |
| `/seo cluster <seed-keyword>` | SERP-based semantic clustering and content architecture |
| `/seo sxo <url>` | Search Experience Optimization: page-type analysis, user stories, personas |
| `/seo drift baseline <url>` | Capture SEO baseline for change monitoring |
| `/seo drift compare <url>` | Compare current state to stored baseline |
| `/seo drift history <url>` | Show drift history over time |
| `/seo ecommerce <url>` | E-commerce SEO: product schema, marketplace intelligence |
| `/seo firecrawl [command] <url>` | Full-site crawling and site mapping (extension) |
| `/seo dataforseo [command]` | Live SEO data via DataForSEO (extension) |
| `/seo image-gen [use-case] <description>` | AI image generation for SEO assets (extension) |
| `/seo setup` | Explicitly create or refresh the isolated Python runtime and Chromium |
| `/seo doctor` | Check runtime readiness without changing the system |

The upstream also exposes `/seo flow`; that sub-skill is CC BY 4.0-licensed and is not carried in this derivative (see Sub-skills below).

## Audit orchestration

When the user invokes `/seo audit`, delegate to subagents in parallel:

1. Detect business type (SaaS, local, ecommerce, publisher, agency, other)
2. Spawn subagents: seo-technical, seo-content, seo-schema, seo-sitemap, seo-performance, seo-visual, seo-geo
3. If Google API credentials detected (`claude-seo run google_auth.py --check`), also spawn seo-google agent
4. If local business detected, also spawn seo-local agent
5. If local business detected AND DataForSEO MCP available, also spawn seo-maps agent
6. If backlink APIs detected (`claude-seo run backlinks_auth.py --check`), also spawn seo-backlinks agent
7. If Firecrawl MCP available, use `firecrawl_map` to discover all site URLs before analysis
8. If content strategy signals detected (blog, pillar pages, topic clusters), also spawn seo-cluster agent
9. If e-commerce detected, also spawn seo-ecommerce agent
10. If drift baseline exists for this URL (`claude-seo run drift_history.py <url>`), also spawn seo-drift agent
11. Always include seo-sxo in full audits (search experience applies to all sites)
12. Collect results and generate unified report with SEO Health Score (0-100)
13. **Synthesize via the 10-principle framework** (see "Synthesis methodology" below), walk PERCEIVE → ANALYZE → VALIDATE → ACT before bucketing findings into Critical / High / Medium / Low
14. Create prioritized action plan with dependency sequencing + falsifiability per recommendation
15. **Offer PDF report**: "Generate a professional PDF report? Use `/seo google report full`"

For individual commands, load the relevant sub-skill directly. After any analysis command completes, offer to generate a PDF report via `/seo google report full`.

### Verify

After the report is written and before it is delivered, prove it clean against the gates and the excised-footer rule:

```bash
# 1. no promotional content anywhere in the deliverable (expect: no output)
grep -nEi "skool\.com|join .*community|built by" report.md
# 2. no retired schema recommended (expect: no output)
grep -nEi "recommend[a-z]* (adding )?(new )?(howto|faqpage)" report.md
# 3. llms.txt never sold as a citation-ranking lever (review each hit)
grep -nEi "llms\.txt" report.md
```

Checks 1 and 2 must return nothing. Any check-3 hit must not present llms.txt as a citation-ranking lever or claim a confirmed citation benefit; reporting its status, or listing it as an optional low-effort item, is legitimate upstream behavior. A deliverable that fails these greps is not done.

## Synthesis methodology

Audits are not just findings; they are findings synthesized into a coherent strategy. The suite uses a 10-principle thinking framework grouped into four phases: **PERCEIVE** (observe-external · observe-internal · listen), **ANALYZE** (think · connect-lateral · connect-system), **VALIDATE** (feel · accept), **ACT** (create · grow).

Full audits (`/seo audit`, `/seo page`) walk every phase before emitting the action plan. Narrower commands (`/seo schema`, `/seo images`, etc.) pass at least THINK + ACCEPT before emitting (sound first principle, surfaced falsifiability). The Critical / High / Medium / Low priority buckets are the **output** of validation, not a substitute for it.

Each emitted recommendation should carry:

- The first-principle observation it rests on (THINK)
- The dependency on / unblock relationship to other recommendations (CONNECT-system)
- An explicit "how would we know this failed?" check (ACCEPT)
- A leading indicator the user can monitor without re-running the audit (GROW)

Full methodology and per-principle SEO mapping: `references/thinking-framework.md`.

## Industry detection

Detect business type from homepage signals:

- **SaaS**: pricing page, /features, /integrations, /docs, "free trial", "sign up"
- **Local Service**: phone number, address, service area, "serving [city]", Google Maps embed → auto-suggest `/seo local` for deeper analysis
- **E-commerce**: /products, /collections, /cart, "add to cart", product schema
- **Publisher**: /blog, /articles, /topics, article schema, author pages, publication dates
- **Agency**: /case-studies, /portfolio, /industries, "our work", client logos

### Verify

Confirm the detected type's signals actually occur in fetched HTML before spawning conditional specialists — the local specialist spawns only on address/phone/service-area signals, the ecommerce one only on cart/product signals. The pattern covers all five types (SaaS, e-commerce, publisher, agency, local — the local alternates include phone numbers, service-area phrasing, and Maps embeds):

```bash
curl -sL https://example.com/ | grep -Eio "free trial|sign up|/features|/integrations|add to cart|/cart|/collections|/products|/blog|/articles|/topics|datePublished|case-stud(y|ies)|our work|/portfolio|serving [a-z]+|service area|maps\.google|google\.com/maps|\(?[0-9]{3}\)?[-. ][0-9]{3}[-.][0-9]{4}" | sort -f | uniq -ci | sort -rn
```

If the top two types are close, do not guess: present both with their supporting signals and ask the user to confirm (see Error handling).

## Quality gates

Read `references/quality-gates.md` for thin content thresholds per page type. Hard rules:

- WARNING at 30+ location pages (enforce 60%+ unique content)
- HARD STOP at 50+ location pages (require user justification)
- Never recommend HowTo schema (deprecated Sept 2023)
- FAQ schema: Google retired FAQ rich results for ALL sites on May 7, 2026 (no SERP feature anymore; supersedes the Aug 2023 gov/health restriction). Flag existing FAQPage at Info (not Critical); do not claim confirmed AI/LLM citation benefit; do not recommend removal; do not recommend new FAQPage for Google SERP benefit; use QAPage for genuine user Q&A
- All Core Web Vitals references use INP, never FID

### Verify

Before approving or generating programmatic location pages, count what already exists:

```bash
curl -s https://example.com/sitemap.xml | grep -Eo "<loc>[^<]*/(locations?|areas?|cities)/[^<]+</loc>" | wc -l
```

The `-Eo ... | wc -l` pipeline counts URL matches, not lines — a minified single-line sitemap still counts correctly. Caveat: a sitemap INDEX (`<sitemapindex>` at the root) returns 0 for its own URL; fetch and count each child sitemap first. 30+ triggers the warning and the 60%-unique-content enforcement; 50+ triggers the hard stop — proceed only with the user's explicit justification recorded in the report. The gate exists because Google's doorway-page systems penalize thin programmatic location pages (`references/quality-gates.md`).

## Scoring methodology

### SEO Health Score (0-100)

Weighted aggregate of all categories:

| Category | Weight |
|----------|--------|
| Technical SEO | 22% |
| Content Quality | 23% |
| On-Page SEO | 20% |
| Schema / Structured Data | 10% |
| Performance (CWV) | 10% |
| AI Search Readiness | 10% |
| Images | 5% |

### Priority levels

- **Critical**: Blocks indexing or causes penalties (immediate fix required)
- **High**: Significantly impacts rankings (fix within 1 week)
- **Medium**: Optimization opportunity (fix within 1 month)
- **Low**: Nice to have (backlog)

## Sub-skills

The 24 sub-skills the upstream orchestrates (the orchestrator itself is the 25th in `skills/` and does not orchestrate itself; entry 24 is license-scoped out of this derivative). Descriptors below are this derivative's own wording — sub-skill names, order, and contributor credits are the upstream's:

1. **seo-audit** — the fan-out full-site audit
2. **seo-page** — one page, examined in depth
3. **seo-technical** — nine-category technical review
4. **seo-content** — content quality through the E-E-A-T lens
5. **seo-content-brief** — keyword-targeted brief building (contributed by puneetindersingh)
6. **seo-schema** — finds, validates, and writes Schema.org markup
7. **seo-images** — image SEO from alt text to file weight
8. **seo-sitemap** — XML sitemap review and creation
9. **seo-geo** — GEO for AI answer engines; reports llms.txt presence with zero citation weight
10. **seo-plan** — template-driven strategy work
11. **seo-programmatic** — page generation at scale, planned and audited
12. **seo-competitor-pages** — comparison pages drafted against rivals
13. **seo-hreflang** — international targeting: hreflang, locale profiles, parity
14. **seo-local** — the local stack: profile, citations, reviews, multi-location markup
15. **seo-maps** — map-pack intelligence, geo-grids to competitor radii
16. **seo-google** — the Google API layer: Search Console, PageSpeed, CrUX, Indexing, GA4
17. **seo-backlinks** — link profiles from free sources (Moz, Bing, Common Crawl) up to DataForSEO
18. **seo-cluster** — keywords clustered by what the SERP shows (contributed by Lutfiya Miller)
19. **seo-sxo** — search-experience scoring (contributed by Florian Schmitz)
20. **seo-drift** — baselines watched for drift (contributed by Dan Colta)
21. **seo-ecommerce** — product and marketplace SEO (contributed by Matej Marjanovic)
22. **seo-dataforseo** — DataForSEO MCP mirror (extension)
23. **seo-image-gen** — Gemini-backed image generation mirror (extension)
24. **seo-flow** — upstream ships a FLOW-framework integration sub-skill under CC BY 4.0; none of that material is carried in this derivative. Use the upstream repo directly if you need it.

### Optional extensions

Extensions ship in the upstream's `extensions/` directory rather than `skills/` and require a separate installer to activate (each extension's `install.sh` / `install.ps1`). Once installed they are reachable through `/seo` subcommands: firecrawl, dataforseo, and image-gen, plus `/seo ahrefs`, `/seo bing`, `/seo profound`, `/seo seranking`, and `/seo unlighthouse`. Each installs as its own sub-skill, so the model also auto-routes to their descriptions without the `/seo` prefix.

Every extension calls a third-party API with the data you are analyzing — see Prerequisites for the egress condition.

- **seo-firecrawl** — Full-site crawling and site mapping via Firecrawl MCP. Install via `extensions/firecrawl/install.sh` (Unix) or `extensions/firecrawl/install.ps1` (Windows). Once installed, invoke via `/seo firecrawl <command>`.

## Subagents

For parallel analysis during audits:

- `seo-technical` — Crawlability, indexability, security, CWV
- `seo-content` — E-E-A-T, readability, thin content
- `seo-schema` — Detection, validation, generation
- `seo-sitemap` — Structure, coverage, quality gates
- `seo-performance` — Core Web Vitals measurement
- `seo-visual` — Screenshots, mobile testing, above-fold
- `seo-geo` — AI crawler access, llms.txt, citability, brand mention signals
- `seo-local` — GBP signals, NAP consistency, reviews, local schema, industry-specific local factors (conditional: spawned when Local Service detected)
- `seo-maps` — Geo-grid rank tracking, GBP audit, review intelligence, competitor radius mapping (conditional: spawned when Local Service detected AND DataForSEO MCP available)
- `seo-google` — CWV field data, URL indexation status, organic traffic trends (conditional: spawned when Google API credentials detected)
- `seo-backlinks` — Backlink profile data: DA/PA, referring domains, anchor text, toxic links (conditional: spawned when Moz/Bing API keys detected or always for CC domain-level metrics)
- `seo-cluster` — Semantic clustering analysis (conditional: content strategy detected)
- `seo-sxo` — Page-type mismatch, user stories, persona scoring (always in full audits)
- `seo-drift` — Baseline comparison (conditional: drift baseline exists for URL)
- `seo-ecommerce` — Product schema, marketplace intel (conditional: e-commerce detected)
- `seo-dataforseo` — Live SERP, keyword, backlink, local SEO data (extension, optional)
- `seo-image-gen` — SEO image audit and generation plan (extension, optional)

## Reference files

Load these on-demand as needed (do NOT load all at startup):

- `references/cwv-thresholds.md`: Current Core Web Vitals thresholds and measurement details
- `references/schema-types.md`: All supported schema types with deprecation status
- `references/eeat-framework.md`: E-E-A-T evaluation criteria (Sept 2025 QRG update)
- `references/quality-gates.md`: Content length minimums, uniqueness thresholds
- `references/local-seo-signals.md`: Local ranking factors, review benchmarks, citation tiers, GBP status
- `references/local-schema-types.md`: LocalBusiness subtypes, industry-specific schema and citation sources
- `references/thinking-framework.md`: The 10-principle audit synthesis methodology

Maps-specific references (loaded by the seo-maps skill, not at startup): `references/maps-geo-grid.md`, `references/maps-gbp-checklist.md`, `references/maps-api-endpoints.md`, `references/maps-free-apis.md`

Backlinks-specific references (loaded by the seo-backlinks skill, not at startup): `references/backlink-quality.md`, `references/free-backlink-sources.md`

## Error handling

| Scenario | Action |
|----------|--------|
| Unrecognized command | List available commands from the Command surface table. Suggest the closest matching command. |
| URL unreachable | Report the error and suggest the user verify the URL. Do not attempt to guess site content. |
| Sub-skill fails during audit | Report partial results from successful sub-skills. Clearly note which sub-skill failed and why. Suggest re-running the failed sub-skill individually. |
| Ambiguous business type detection | Present the top two detected types with supporting signals. Ask the user to confirm before proceeding with industry-specific recommendations. |

## Findings

- **Excised — promotional footer (the declared defect).** The base closed with a section instructing the agent, after completing any major deliverable, to append a promotional block as the very last output: an author byline with links to a free and a paid community, listed for 16 deliverable types explicitly including full client audit reports, with a skip-list covering only the small commands. Removed wholesale — heading, instruction, fenced block, and both show/skip lists. Nothing in this document instructs adding promotional content to any deliverable, and the audit Verify step greps every deliverable to prove such content absent.
- **Excised — CC BY scoping.** The upstream sub-skill seo-flow is CC BY 4.0-licensed inside an otherwise-MIT repo. Its command row, subagent entry, and stage/prompt details are not carried; only a one-line upstream pointer remains (see license_notes in the frontmatter).
- **Defect fixed.** The base offered PDF generation via a `scripts/`-prefixed file path that its own shipped skill directory does not contain; replaced with the equivalent launcher command `/seo google report full`, which the base also documents.
- **Defect fixed.** Two shipped reference files (backlink quality, free backlink sources) were never listed in the base's reference index; both are now listed under the backlinks entry so every vendored file is reachable from the body.
- **Security surfaced.** All eight optional extensions call third-party APIs — analyzed URLs, keywords, and log-derived queries leave the machine to those vendors. Stated as hard conditions in Prerequisites and When NOT to use. The base's own good hygiene is kept verbatim: launcher-only script execution, doctor output redacting paths and environment values, setup only on explicit request.
- **Grafts.** None.

## Attribution

- **AgriciDaniel/claude-seo/seo** — MIT. Base and sole text source of this derivative. Upstream repository: https://github.com/AgriciDaniel/claude-seo (v2.2.4; content hash at derivation in the frontmatter). The upstream `LICENSE.txt` is vendored alongside this document; all 13 vendored `references/*.md` files originate from this same skill directory (per-file origin, hash, and source URL in the frontmatter `files` list).
- Sub-skill contributor credits retained from the upstream: seo-content-brief (puneetindersingh), seo-cluster (Lutfiya Miller), seo-sxo (Florian Schmitz), seo-drift (Dan Colta), seo-ecommerce (Matej Marjanovic).
- Shared-ancestry provenance, zero text contributed (listed as `sibling` entries so the graft legal guard can tell common ancestry from importation; licenses recorded as fact, not gated): **AgriciDaniel/codex-seo/seo** (NOASSERTION) — the same author's Codex-runtime port of this same front door; **AgriciDaniel/claude-seo/seo-audit** (MIT) and **AgriciDaniel/codex-seo/seo-audit** (NOASSERTION) — the audit sub-skills restating the same scoring and orchestration tables. No adjudication of these twins' quality is made or implied.
- This derivative is published under the MIT license.
