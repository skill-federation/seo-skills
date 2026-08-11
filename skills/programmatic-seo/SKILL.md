---
name: programmatic-seo
description: Build SEO pages at scale from a template plus a dataset without earning a thin-content penalty.
  Choose one of twelve page playbooks, anchor each page to a defensible data source and a real unique-value
  rule, pick a subfolder URL pattern, and set indexation so a large templated set survives Google's 2026
  scaled-content and doorway-page enforcement. Use when asked to generate many keyword- or location-variant
  pages (pSEO, directory, comparison, or geo pages) that must genuinely rank.
license: MIT
treatment: derivative
derived_from:
- id: coreyhaines31/marketingskills/programmatic-seo
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: 468af78790daac653dde669968a58773ad06754d25bc31de9b2272632bf58d3a
targeted_version: Google Search spam policies, 2026
last_verified_at: 2026-08-10
---

# Programmatic SEO

Build SEO-optimized pages at scale from a template and a dataset. The one job of
this skill is to produce pages that rank and provide genuine value — never a mass
of near-duplicate pages that a search engine demotes. You produce a written build
plan, `pseo-plan.md`, and each phase ends in a check that greps that plan so the
strategy proves itself before a single page ships.

## Conditions

### When to use

Reach for this skill when someone wants to generate **many similar pages** from
one template driven by rows of data — a repeating keyword pattern such as
`[service] in [city]`, `[X] vs [Y]`, `what is [term]`, or `[category] tools`.
Typical triggers: pSEO, directory pages, location pages, comparison pages,
integration pages, glossary pages, "spin up 500 pages", "data-driven pages".

### When NOT to use

- **Editorial or pillar content planning** (what topics to own, blog roadmap,
  topic clusters) is not this skill — hand that to `content-strategy`, which
  plans the content and hands scaled work back here.
- **A one-off page or a handful of hand-written pages** — the template + data
  machinery is overhead you do not need; write them directly.
- **You have no defensible data and no real search demand.** This is the
  thin-content trap. Swapping a city name into otherwise-identical copy across
  hundreds of URLs is exactly what current spam enforcement targets (see Era).
  If that is your situation, do not do pSEO at all — reach for `content-strategy`
  to build fewer, deeper pages that earn their traffic.

### Prerequisites

pSEO needs **two** real inputs before it can work. If you cannot produce both,
stop — the method has nothing to stand on.

1. **A repeating keyword pattern with real aggregate demand.**
   - *What it is:* a template slot structure (`[variable]` positions) whose
     combinations people actually search for, with meaningful summed volume.
   - *Where it comes from:* keyword tools — Ahrefs / Semrush / Moz for volume and
     difficulty; Google Search Console (Performance → Queries) for demand you
     already capture; Google Keyword Planner (free with a Google Ads account) as
     a floor. Validate the *aggregate* across the pattern, not one head term.
   - *Who cannot produce it:* if the combinations have no measurable demand, the
     pages have no audience. Over-generating pages with no search demand is one
     of the classic mistakes — reach for `content-strategy` instead.

2. **A defensible data source, one per page.**
   - *What it is:* real data that populates each page and makes it non-identical —
     ideally something competitors cannot trivially copy.
   - *Where it comes from:* your product database (usage, pricing, catalog),
     user-generated content (reviews, listings), a licensed feed you have
     exclusive access to, or, weakest, a public dataset anyone can scrape.
   - *Who cannot produce it:* no proprietary, product-derived, user-generated, or
     licensed data **and** no real search demand means every page collapses to
     the same template — the thin-content trap. Do not ship it; use
     `content-strategy` to plan content you *can* differentiate.

### What breaks first

The first thing to fail is almost never the template — it is **per-page
uniqueness at volume**. As the row count climbs, pages drift toward "same copy,
one swapped variable", indexation stalls, and a thin-content or doorway
demotion follows. The numeric guardrail for near-duplicate location pages (a
warning threshold, a hard-stop count, and a minimum unique-content share) is
owned by `seo-plan` — treat it as a build constraint and do not restate the
numbers here.

## Era

**Targets Google Search spam-policy reality as of 2026.** The base skill said
"avoid Google penalties / no doorway pages / no thin content" without pinning it
to a policy; here is the current framing the rest of this bundle also teaches:

- **Scaled content abuse.** As of 2026, mass-produced template pages that add no per-page value fall under Google's scaled content abuse spam policy — the same policy family the bundle's AI-SEO guidance cites for content spun up "for AI". Volume without value is the trigger, whether a human or a script wrote it.
- **Doorway-page demotion.** near-duplicate location pages are treated as doorway pages and demoted, which is why "unique value per page" is a hard requirement here and why `seo-plan` enforces a numeric cap on location-page fan-out.
- **URL structure still holds.** In 2026, subfolders still consolidate domain
  authority while subdomains split it — the subfolder rule below is unchanged.
- **Deprecated markup.** Do not lean on HowTo or FAQ rich results to pad
  programmatic pages for a SERP feature; that markup no longer earns one. For
  what schema still helps, hand markup work to the `seo` skill rather than
  guessing here.

## The 12 Playbooks

Every pSEO build is one (or a layered combination) of these proven patterns.

| Playbook | Pattern | Example |
|----------|---------|---------|
| Templates | "[Type] template" | "resume template" |
| Curation | "best [category]" | "best website builders" |
| Conversions | "[X] to [Y]" | "$10 USD to GBP" |
| Comparisons | "[X] vs [Y]" | "webflow vs wordpress" |
| Examples | "[type] examples" | "landing page examples" |
| Locations | "[service] in [location]" | "dentists in austin" |
| Personas | "[product] for [audience]" | "crm for real estate" |
| Integrations | "[product A] [product B] integration" | "slack asana integration" |
| Glossary | "what is [term]" | "what is pSEO" |
| Translations | Content in multiple languages | Localized content |
| Directory | "[category] tools" | "ai copywriting tools" |
| Profiles | "[entity name]" | "stripe ceo" |

**Detailed per-playbook implementation** (value requirements + URL structure per
pattern): see [references/playbooks.md](references/playbooks.md).

## Phase 1 — Scope and playbook selection

Establish business context (product, audience, conversion goal for these pages),
size the opportunity (how many combinations, volume distribution head vs. long
tail, trend), and judge the competitive landscape (who ranks now, can you
realistically compete). Then choose the playbook that matches your assets:

| If you have... | Consider... |
|----------------|-------------|
| Proprietary data | Directory, Profiles |
| Product with integrations | Integrations |
| Design/creative product | Templates, Examples |
| Multi-segment audience | Personas |
| Local presence | Locations |
| Tool or utility product | Conversions |
| Content/expertise | Glossary, Curation |
| Competitor landscape | Comparisons |

You can layer playbooks (e.g. "best coworking spaces in San Diego" = Curation +
Locations). Record the choice in `pseo-plan.md` as a `Playbook:` line.

### Verify

```bash
grep -Eiq '^Playbook:[[:space:]]*[A-Za-z]' pseo-plan.md \
  && echo "PASS: a playbook is chosen" \
  || echo "FAIL: pseo-plan.md has no 'Playbook:' line"
```

## Phase 2 — Data source and defensibility

Every page must be populated by real data, and the strength of the build is the
strength of that data. Rank your source on the defensibility hierarchy (strongest
first):

1. **Proprietary** — you created it (strongest, hardest to copy)
2. **Product-derived** — from your users' activity
3. **User-generated** — from your community
4. **Licensed** — exclusive access you pay for
5. **Public** — anyone can use it (weakest)

If your only source is public data with no added analysis, expect to compete on
depth of insight per page, not on the data itself. Record the source and its tier
in `pseo-plan.md` as `Data source:` and `Defensibility tier:` lines (tier value
one of: Proprietary, Product-derived, User-generated, Licensed, Public).

### Verify

```bash
grep -Eiq '^Data source:[[:space:]]*[A-Za-z]' pseo-plan.md \
  && grep -Eiq '^Defensibility tier:[[:space:]]*(proprietary|product-derived|user-generated|licensed|public)' pseo-plan.md \
  && echo "PASS: data source and defensibility tier recorded" \
  || echo "FAIL: add a 'Data source:' and a valid 'Defensibility tier:' line"
```

## Phase 3 — URL structure and per-page uniqueness

**Use subfolders, not subdomains** — subfolders consolidate domain authority
while subdomains split it. Write the pattern as a leading-slash path:

- Good (subfolder): `example.com/compare/notion-vs-coda/`
- Bad (subdomain): `compare.example.com/notion-vs-coda/`

Then commit to the rule that keeps the set out of thin-content territory: **each
page must carry value specific to that page** — original analysis, conditional
sections driven by the data, or genuinely local detail — not just a swapped
variable. Record a `URL pattern:` line (leading slash) and a `Unique-value rule:`
line stating concretely what makes each page non-duplicative.

### Verify

```bash
grep -Eiq '^URL pattern:[[:space:]]*/[A-Za-z0-9]' pseo-plan.md \
  && grep -Eiq '^Unique-value rule:[[:space:]]*[A-Za-z]' pseo-plan.md \
  && echo "PASS: subfolder URL pattern and unique-value rule recorded" \
  || echo "FAIL: need a leading-slash 'URL pattern:' and a 'Unique-value rule:' line"
```

## Phase 4 — Indexation, sitemaps, and internal linking

Wire the pages into the site and control what gets indexed:

- **hub-and-spoke** internal linking: a hub category page links to the individual
  programmatic (spoke) pages, with cross-links between related spokes. No orphan
  pages — every page reachable from the main site, with breadcrumbs.
- **Sitemaps and indexation:** put pages in an XML sitemap, separate sitemaps by
  page type, prioritize high-volume patterns, `noindex` very thin variations, and
  manage crawl budget deliberately rather than dumping every combination at once.

Record an `Indexation:` line naming the sitemap and thin-page (`noindex`) strategy.

### Verify

```bash
grep -Eiq '^Indexation:[[:space:]]*[A-Za-z]' pseo-plan.md \
  && grep -Eiq 'sitemap' pseo-plan.md \
  && echo "PASS: indexation and sitemap strategy recorded" \
  || echo "FAIL: add an 'Indexation:' line covering sitemaps and thin-page handling"
```

## Phase 5 — Quality gate and handoff

Before building, the plan must be complete on all five load-bearing fields.
After building, hand off — this skill plans the pages-at-scale method; it does not
own markup or post-launch auditing.

- **Structured data / schema markup:** hand to the `seo` skill.
- **Location-page fan-out cap** (the numeric doorway guardrail): honor `seo-plan`.
- **Pre-ship validation** of the generated pages while they are still in the
  repo, before you deploy: `seo-validate` (a read-only, CI-gating repo check —
  it refuses live URLs, so it belongs here, not post-launch).
- **Post-launch auditing** of the shipped pages (thin content, indexation,
  AI-readiness): hand to the live auditors — `geo-audit`, `geo-technical`.
- **Upstream content planning:** `content-strategy` decides what to build and
  routes scaled work here.

### Verify

```bash
missing=0
for field in "Playbook:" "Data source:" "Defensibility tier:" "URL pattern:" "Unique-value rule:" "Indexation:"; do
  grep -Eiq "^${field}" pseo-plan.md || { echo "MISSING: ${field}"; missing=1; }
done
[ "$missing" -eq 0 ] && echo "PASS: pseo-plan.md is complete — ready to build" \
  || echo "FAIL: complete the missing fields before building"
```

## Common mistakes

- **Thin content:** just swapping city names in otherwise identical copy.
- **Keyword cannibalization:** multiple pages targeting the same keyword.
- **Over-generation:** creating pages for combinations with no search demand.
- **Poor data quality:** outdated or incorrect information at scale.
- **Ignoring UX:** pages built for Google, not for the person who lands on them.

## Attribution

Derived from **programmatic-seo** in `coreyhaines31/marketingskills`
(https://github.com/coreyhaines31/marketingskills), licensed MIT. This derivative
is likewise MIT. The vendored `references/playbooks.md` originates from the same
MIT source; it was edited to remove a dangling cross-reference to a non-bundle
skill and a stray non-playbook table entry (its upstream original is pinned by
`original_sha256` in this document's frontmatter).
