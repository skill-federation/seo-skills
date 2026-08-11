---
name: keyword-strategy
description: 'Plan which search terms a site should target in 2026: discover candidate queries, label
  them by search intent, cluster them, screen for winnability, and rank the survivors into a prioritized
  topical map. The standalone strategy layer — no paid API, and it calls none. Use it to choose targets,
  size winnable long-tail, or turn a raw export into a plan. It plans targeting only; it audits no live
  page. For the content plan that consumes the map, see content-strategy.'
license: MIT
treatment: derivative
derived_from:
- id: kostja94/marketing-skills/keyword-research
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: dd186633748cacbd90076bf717102752aa5adf5ae2f3b80a0b8bb0e109dc0933
last_verified_at: 2026-08-10
---

# Keyword Strategy

Plan keyword targeting: discover candidate queries, classify them by search intent, cluster them, screen for winnability, and prioritize the survivors into a topical map. This is the strategy layer — it decides *what to target*; it does not audit pages, score sites, or call any paid API. The one artifact it produces is a `keyword-map.md`.

**On first use**, open with 1–2 sentences on what this skill covers, then produce the map. On subsequent use, or if the user asks to skip, go straight to the output.

## Conditions

### When to use

- The user wants to decide **which search terms to target** — choosing targets, not writing pages.
- They ask for keyword discovery, search-intent classification, keyword clustering, a topical map, or a prioritized keyword plan.
- They have a raw keyword export (Ahrefs/SEMrush/GSC CSV) and need it turned into an intent-labeled, clustered, prioritized plan.
- They want to size **winnable long-tail** for a new or low-authority site.
- They need the keyword layer *before* a content plan or a page build.

### When NOT to use

- **Running tool-driven scans, live SERP/keyword fetches, or a full audit behind an installed runtime** — that is **claude-seo**, whose installed-runtime front door drives it (`/seo cluster`, `/seo content-brief`, GSC data via `/seo google`). keyword-strategy is the *standalone* method you can run with only Google autocomplete and a browser; reach for claude-seo when the user has that toolchain installed and wants it driven.
- **The content plan that consumes the map** — editorial calendar, what to write, pillar pages as *content* — is **content-strategy**. keyword-strategy produces the keyword-to-page map; content-strategy turns it into a content plan. Do not rebuild pillar/cluster *content* planning here.
- **AI-search citation** — getting cited by LLMs, AI Overviews, ChatGPT/Perplexity visibility — is **ai-seo** / **geo-plan**. keyword-strategy is traditional keyword targeting, not answer-engine optimization.
- **On-page, technical, or live-page scoring** — this skill audits nothing and fetches no URL to grade it.
- For an end-to-end SEO roadmap that sequences keyword work with the rest, see **seo-plan**.

### Prerequisites

This skill *benefits from* keyword-tool access but must degrade gracefully to free methods. State up front what you have.

**What it needs:** a seed understanding of the product/audience, plus — ideally — volume and difficulty signal for candidate terms. **Check for project context first:** if `.claude/project-context.md` or `.cursor/project-context.md` exists, read it for product, audience, and positioning.

**Where the signal comes from, by situation:**

| You have | Source of volume/difficulty |
|---|---|
| A paid tool | Ahrefs Keywords Explorer, SEMrush Keyword Overview — volume band + keyword difficulty (KD) |
| A Google Ads account | Google Keyword Planner — bucketed volume ranges (see Era); Google Trends for relative interest |
| A verified site in Search Console | GSC — your own real queries, impressions, and average position (first-party truth) |
| No tool at all | Google autocomplete (alphabet method), People Also Ask, Related Searches, Reddit/Quora/forums — discovery without volumes |

**Who cannot produce the signal, and what to do instead:**

- **No paid tool and no Google Ads account** → you cannot get exact volumes or KD. Use the free discovery methods (autocomplete / People Also Ask / alphabet method) to *find* candidates, then record volume and KD as qualitative estimates (`est. low/med/high`) in the map rather than leaving cells blank. This is a first-class path, not a dead end — the method is designed to run tool-less.
- **Brand-new site with no Search Console history** → no first-party query data yet. Lean on autocomplete/PAA plus competitor SERP inspection; revisit with GSC data once the site has impressions.
- keyword-strategy calls **no paid API** itself; any tool above is the user's own account, used by them, not a dependency of this skill.

### What breaks first

- **Invented terms nobody searches.** The single biggest failure. Every keyword must be one real users actually type — validate against autocomplete or tool data; never brainstorm targets in a vacuum.
- **Sorting on a single volume number.** Tools now report ranges, not counts (see Era). A plan that ranks purely on one "monthly searches" figure breaks; rank on volume *band* + intent + winnability instead.
- **Head-term obsession.** Zero-click and AI answers eat head-term clicks (see Era); a plan aimed only at broad heads loses the click even when it ranks. Intent-matched long-tail is where winnable traffic and conversions live.
- **Translating a list instead of re-researching in-language.** In multilingual work, a translated keyword list breaks — demand differs by language. Re-research each target language natively.

## Era

Targets **2026** keyword tooling and SERP behavior. Two shifts change how a keyword strategy is built today:

- **Volumes are ranges, not counts.** As of 2026, Google Keyword Planner reports search volume as bucketed ranges, not exact monthly counts (e.g. "1K–10K"), and third-party tools model volume rather than measure it. Treat any single volume figure as an estimate; rank on band + intent, and store a range in the map's Volume column.
- **Head-term clicks are shrinking.** In 2026, zero-click SERPs and AI Overviews absorb a growing share of head-term clicks, so search intent and long-tail specificity carry more of a keyword's real value than raw volume does. Screen for intent match and winnable long-tail before chasing broad heads.

Most keywords are low-volume, and long-tail queries dominate aggregate search traffic — so a strategy built on many specific, intent-matched terms usually beats one built on a handful of high-volume heads. (These are directional realities of search demand, stated without a precise percentage; the exact split varies by market and is not a stable published figure.)

## The keyword map (keyword-map.md)

Every phase writes into one artifact, `keyword-map.md`. Build it with these ASCII section headers so the checks below can verify it:

```
# Keyword map: <project>

## Executive summary
Top 3 priorities.

## Keyword list
| Keyword | Volume | KD | Intent | Cluster | Priority | Target page |
|---------|--------|----|--------|---------|----------|-------------|
| best seo tool for startups | 1K–10K | 34 | Commercial | tool-comparison | High | /compare |

## Clusters
### tool-comparison
- best seo tool for startups
- seo tool vs ...

## Pillar / cluster / page map
- Pillar: SEO tools (hub) -> Cluster: tool-comparison -> Page: /compare

## Content gaps
- keyword a competitor ranks for that this site does not
```

Volume accepts a range or a qualitative estimate; no cell should be left blank or `TBD` once a phase is done.

## Phase 1 — Scope the target

Identify, before discovery:

1. **Product / service** — what is offered.
2. **Audience** — who searches for it, and in what words (customer language from project context).
3. **Goal** — traffic, conversions, or brand.
4. **Tool access** — which row of the Prerequisites table applies (this sets whether volumes are exact, bucketed, or estimated).

Write the project name and the top-3 goal priorities into the map's `## Executive summary`.

## Phase 2 — Discover candidate keywords

Cast wide before filtering. Combine sources; do not rely on one.

| Method | What it yields |
|---|---|
| **User perspective** | Pain points and the words the audience would search; customer language from project context |
| **Tool expansion** | Related keywords, questions, and suggestions from your keyword tool |
| **Competitor reverse** | Read competitor titles, H1s, and URLs; the pages where they rank #4–10 are your opportunities (gaps to take) |
| **People Also Ask** | People Also Ask and Related Searches — high-value signals from real user behavior |
| **Extract from an article** | Auditing existing content: pull seed terms from title, H1, H2s, and the first 100 words, then expand each seed |

**Google autocomplete (long-tail discovery).** Autocomplete only surfaces queries with real traffic, so it is the primary tool-less source and often finds long-tail that paid tools filter out.

- **Alphabet method** (seed + space + each letter): type `keyword a`, `keyword b`, … `keyword z`; record relevant suggestions; repeat with digits `0–9`. Example: `seo a` → "seo audit", "seo agency"; `seo b` → "seo basics", "seo best practices".
- **Position variants**: prefix (`a keyword`), suffix (`keyword a`, the alphabet method above), and middle (`how to keyword a`, `best keyword for`).
- **Question and intent modifiers**: `how to`, `what is`, `why`, `when`, `vs`, `for beginners`, `for small business`, `without`.

**Incremental sources**: support tickets, community, reviews, and NPS (high-frequency questions = unmet demand); and multi-platform search (Reddit, Quora, X, Hacker News) for real phrasing.

Write every candidate as a row in `## Keyword list` (Intent, KD, Cluster can stay empty for now).

### Verify

```bash
# Real candidates exist under the Keyword list (rows beyond header + divider)
awk '/^## Keyword list/{f=1;next} /^## /{f=0} f&&/^\|/{n++} END{print (n>2)?"PASS: "n-2" candidate rows":"FAIL: no candidates captured"}' keyword-map.md
```

## Phase 3 — Classify search intent

Label every candidate with one intent. Intent, not volume, decides whether a ranking earns a click in 2026.

| Intent | Content type | Example |
|---|---|---|
| **Informational** | Blog, guide, FAQ | "how to optimize sitemap" |
| **Navigational** | Brand page | "acme login" |
| **Commercial** | Comparison, review | "seo tools comparison" |
| **Transactional** | Product, pricing | "best seo tool pricing" |

**Modifier signals** (fast first pass): informational — "how", "what", "why", "guide", "tutorial"; commercial — "best", "compare", "vs", "review", "top"; transactional — "buy", "price", "cheap", "coupon"; local — place names.

**SERP check** (authoritative): search the term and read the result page. Knowledge cards/Wikipedia → informational; product lists and reviews → commercial; brand sites → navigational. Broad terms often show a mixed SERP — split them by the dominant intent. Note where SERP features (a featured snippet, People Also Ask, an AI answer) may satisfy the query with no click; that lowers the term's real traffic value.

Fill the **Intent** column for every row.

### Verify

```bash
# Every row carries a recognized intent; no placeholders remain
grep -Eqi 'informational|commercial|transactional|navigational' keyword-map.md \
  && ! grep -qi 'TBD' keyword-map.md \
  && echo "PASS: intents filled" || echo "FAIL: unresolved intent labels"
```

## Phase 4 — Cluster into a topical map

Group the labeled keywords, then map the groups to a page structure.

| Clustering method | Use |
|---|---|
| **SERP overlap** | Keywords whose top-ranking pages overlap → same cluster (strongest signal) |
| **Semantic** | Group by meaning and related concepts |
| **Intent-based** | Group by intent; split a cluster into separate pages when intent differs inside it |

**Pillar → cluster → page.** A pillar (hub) is a broad topic page; clusters (spokes) are focused subtopics that link back to it. Target the long-tail spokes first, then the pillar; interlink spokes within a topic. Record each mapping in `## Pillar / cluster / page map` as `Pillar: <hub> -> Cluster: <spoke> -> Page: <url>`.

Stop at the keyword-to-page map. Turning that map into an editorial plan — what to write, in what order, at what depth — is **content-strategy**'s job; do not rebuild content planning here.

### Verify

```bash
# Clusters exist and the pillar/cluster/page mapping is present
grep -q '^## Clusters' keyword-map.md \
  && grep -q '^## Pillar / cluster / page map' keyword-map.md \
  && echo "PASS: clusters + pillar/cluster/page map" || echo "FAIL: topical map incomplete"
```

## Phase 5 — Evaluate, screen, and prioritize

Score each surviving keyword, then rank.

| Factor | Consider |
|---|---|
| **Volume band** | Monthly-search range; a niche can relax the floor. Treat the number as an estimate (see Era) |
| **Keyword difficulty (KD)** | New / low-authority sites target lower KD first |
| **CPC** | A higher CPC often signals stronger commercial intent |
| **SERP features** | A featured snippet, People Also Ask, or an AI answer can satisfy intent with no click — discount the term's real traffic accordingly |

**Screening order:** 1) remove irrelevant terms; 2) filter terms too low-volume even for a niche; 3) assess achievability against your KD ceiling; 4) prioritize commercial and transactional intent for conversion-led goals.

**Product-fit screen (optional).** Before committing, test whether the offering is even keyword-targetable: a clear function word (`generator`, `converter`, `checker`, `calculator`, `tool`, …) or an input→output shape ("image to video", "text to speech") signals searchable intent. Pure "agent"/"copilot" products are hard to grow via search — users rarely search "agent"; target adjacent feature terms first, then funnel.

Fill **KD**, **Volume**, and **Priority** for every row.

### Verify

```bash
# No scored cell was left as a placeholder
grep -nE '\|[[:space:]]*(\?|TBD|n/?a)[[:space:]]*\|' keyword-map.md \
  && echo "FAIL: unscored volume/KD cells remain" || echo "PASS: all rows scored"
```

## Phase 6 — Assemble the keyword map

Produce the final `keyword-map.md`. Required contents:

- **Keyword list** — each term with volume band, KD, intent, cluster, priority, and target page.
- **Clusters** — each cluster and its member keywords.
- **Pillar / cluster / page map** — the hub→spoke→page mapping.
- **Content gaps** — keywords competitors rank for that this site does not.
- **Executive summary** — top-3 priorities.

Optional report scaffolding, if the user wants a formal deliverable:

| Section | Content |
|---|---|
| Executive Summary | Top-3 priorities |
| Keyword Overview | Total keywords, primary intent, avg KD, content-gap count |
| Keyword List | Keyword, volume, KD, intent, priority, target page |
| Keyword Mapping | Page/URL, target keywords, status |
| Content Gaps | Keywords competitors rank for that you do not |
| Action Plan | Priority, action, impact, effort |

### Verify

```bash
# All required sections present and at least one content gap listed
for s in "## Keyword list" "## Clusters" "## Pillar / cluster / page map" "## Content gaps"; do
  grep -qF "$s" keyword-map.md || echo "MISSING: $s"
done
awk '/^## Content gaps/{f=1;next} /^## /{f=0} f&&/^[-*] /{n++} END{exit !(n>0)}' keyword-map.md \
  && echo "PASS: content gaps listed" || echo "FAIL: no content gaps listed"
```

## Optional: SEO–PPC keyword synergy

A real strategic angle, but optional — skip it if the user has no paid search. One keyword map can serve both organic and paid search; aligning them avoids duplication, cannibalization, and wasted spend.

| Data flow | Use |
|---|---|
| keyword map → paid search (Google Ads) | Keyword list, clusters, intent; support terms (login, forum, pricing) become negative keywords for paid |
| paid search → keyword map | The Search Terms report and PPC conversion rate flag which terms are worth ranking for organically |
| keyword map → landing pages | Clusters → one landing page per intent; PAA questions → FAQ sections |
| GSC organic rank ≤ 4 | Where you already rank well organically, consider trimming paid spend on those terms to avoid cannibalization |

Use PPC conversion data to validate organic priorities: `SEO ROI ≈ (Organic clicks × PPC conversion rate × Customer value) − SEO cost`.

## Data sources

| Source | Use |
|---|---|
| **Ahrefs** | Keywords Explorer, Site Explorer |
| **SEMrush** | Keyword Overview, Organic Research |
| **GSC** | Search queries, impressions, clicks (first-party) |
| **GA** | Traffic by landing page |
| **PostHog** | Feature / on-site search usage |

## Related skills

- **content-strategy** — the content plan that consumes this keyword map (what to write, editorial calendar).
- **claude-seo** — tool-driven clustering, content briefs, and GSC data behind an installed runtime (`/seo cluster`, `/seo content-brief`, `/seo google`).
- **ai-seo** / **geo-plan** — AI-search citation and answer-engine visibility (a different game from keyword targeting).
- **seo-plan** — the end-to-end SEO roadmap that sequences keyword work with everything else.

## Attribution

Derived from **`kostja94/marketing-skills/keyword-research`** (MIT license), an SEO keyword-research skill by kostja94. This is an upgraded, era-verified derivative: restructured to the domesticated canon (Conditions / Era / verify-looped workflow), re-scoped to keyword *strategy*, with the two undated statistics corrected and cross-references re-pointed to real bundle members. Output license: MIT.
