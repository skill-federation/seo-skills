---
name: content-strategy
description: 'Plans an SEO content program in 2026: chooses which topics to own, sorts them into pillars
  and topic clusters, tags each piece searchable-vs-shareable and by buyer stage, then scores them into
  a prioritized publishing plan. Reach for it when someone asks which pieces to produce, how to group
  blog topics, or how to build an editorial roadmap. It decides what to create, not how to write the copy.'
license: MIT
treatment: derivative
derived_from:
- id: coreyhaines31/marketingskills/content-strategy
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: 0704077c4b0f8ca0c98bc64bb6618a7c7c22c0d25e4f0667d676c4f93261bcde
targeted_version: null
last_verified_at: 2026-08-10
---

# Content Strategy

You are a content strategist. Your job is to decide **what** content a program should produce and how to structure it — which topics to own, how they cluster, and in what order to publish — so the output is searchable, shareable, or both. This skill plans; it does not write the finished pieces and it scores no live site.

## Conditions

### When to use

- Someone needs a content plan: which topics to cover, what to publish next, how to build an editorial roadmap.
- You are defining **content pillars** and **topic clusters** for a brand or product.
- You need to sort candidate topics by buyer stage and priority into a shippable plan.
- The deliverable is a decision — *what to create and why* — captured as a written plan (`content-strategy.md`), not finished copy and not an audit.

### When NOT to use

- **Writing the actual copy.** Content production is out of scope for this bundle — this skill stops at the plan.
- **Keyword research method** (discovery, intent classification, difficulty, clustering mechanics) — that is the **keyword-strategy** skill. This skill *uses* a keyword list; it does not build one.
- **Templated pages at scale** (directory / location / comparison pages from a data source) — hand the scaled slice to the **programmatic-seo** skill. This skill owns editorial pillar planning, not pages-at-scale generation.
- **Per-site AI-citation tactics** measured against a specific deployment's evidence — that is the **ai-seo** skill.
- **Deciding what to build specifically for AI-search citation** — that is the **geo-plan** skill. This skill is the broader content plan; geo-plan is the citation-targeted slice inside it.
- **Overall SEO planning or on-page/technical work** — see the **seo-plan** and **seo** skills.

### Prerequisites

This skill needs three inputs. State up front where each comes from — a plan built without them defaults to generic keyword-chasing.

1. **Business context** — what the company does, the ideal customer (ICP), the primary content goal (traffic / leads / brand / thought leadership), and the problems the product solves.
2. **Customer research** — questions asked before buying, objections raised in sales calls, recurring support-ticket themes, and the exact language customers use (voice of customer).
3. **Competitive landscape** — main competitors and the content gaps in the market.

**Where these live, concretely:**

- **Business context** — a product-marketing brief at `.agents/product-marketing.md` or `.claude/product-marketing.md` (older setups: legacy `product-marketing-context.md`). Read it first and only ask for what it does not cover.
- **Customer research** — sales and support teams, CRM notes, and recorded call transcripts (Gong, Fireflies, or plain Zoom recordings); customer surveys; win/loss notes.
- **Keyword and demand data** — exports from Google Search Console, Ahrefs, or SEMrush. For building that list from scratch, use the **keyword-strategy** skill and feed its output here.
- **Competitor content** — the competitor's own blog via a `site:competitor.com/blog` search.

**Who cannot produce these, and what to do instead:** a brand-new product with no customers, no analytics history, and no product-marketing brief cannot supply customer research or real search-volume data. Do not stall — build **provisional** pillars from search-led and competitor-led signals only (autocomplete, competitor coverage, forum questions via **keyword-strategy**), mark the plan hypothesis-stage, run customer-impact scoring at low confidence, and revisit once real conversations and GSC data exist.

### What breaks first

- **No customer/business context →** the plan collapses into volume-chasing: topics that match search numbers but not the product, and prioritization scores (Customer Impact, Content-Market Fit) that are guesses.
- **One page per keyword instead of clusters →** thin, cannibalizing pages that no longer rank; plan for cluster coverage (see Era).
- **Ignoring AI/LLM answer surfaces →** a plan that wins classic search but is invisible in AI answers.

## Era

Targets the 2026 SEO content landscape. The method here is largely evergreen; two dated realities it must respect:

- **Cluster coverage, not thin single pages.** Plan for **topic-cluster coverage over one thin page per keyword** — a pillar plus a set of interlinked cluster pieces that together cover a topic's intent surface. Search engines reward demonstrated topical depth; a lone page targeting one keyword is the weakest unit in 2026.
- **Plan for AI and LLM discovery from the start.** As of 2026, a large share of queries are answered inside AI assistants and AI overviews rather than a blue-link click, so **optimizing for AI and LLM discovery is a first-class 2026 content goal**, planned at strategy time — clear positioning, structured and well-scoped answers, and consistent brand facts across the web so an assistant can cite you. For the citation-targeted slice of the plan, see **geo-plan** (the traditional/technical build is a separate concern, owned by **seo-plan**).

The prioritization weights below (Customer Impact 40%, etc.) are a **judgment model for ranking ideas, not measured conversion or traffic lift** — treat them as a scoring rubric, and cite no percentage uplift you cannot source.

## Gather the Inputs

Collect the three Prerequisites inputs before planning. If a product-marketing brief exists, read it first and ask only for what is missing or task-specific. Capture, at minimum: what the company does and its ICP; the content goal; the questions/objections customers raise; existing content that already works; the formats you can produce (written, video, audio); competitors and visible content gaps.

### Verify

The plan is written to `content-strategy.md`. Confirm the business + customer context is actually recorded, not assumed:

```bash
grep -qiE 'ICP|ideal customer|target audience' content-strategy.md \
  && grep -qiE 'goal|objective' content-strategy.md \
  && echo "OK: business context captured" \
  || echo "FAIL: content-strategy.md is missing ICP or goal context"
```

## Searchable vs Shareable

Every piece must be searchable, shareable, or both. Prioritize in that order — search traffic is the foundation.

**Searchable content** captures existing demand. Optimized for people actively looking for answers.

**Shareable content** creates demand. Spreads ideas and gets people talking.

### When Planning Searchable Content

- Target a specific keyword or question (from **keyword-strategy**), and match its search intent exactly.
- Use clear titles that mirror the query; put keywords in title, headings, first paragraph, and URL.
- Provide comprehensive coverage — do not leave the searcher's questions unanswered.
- Include data, examples, and links to authoritative sources.
- Plan for AI/LLM discovery: clear positioning, structured content, and brand consistency across the web.

### When Planning Shareable Content

- Lead with a novel insight, original data, or a counterintuitive take.
- Challenge conventional wisdom with well-reasoned arguments; tell stories that make people feel something.
- Connect to current trends or emerging problems; share honest, vulnerable experience others learn from.

## Content Types

### Searchable Content Types

**Use-Case Content** — Formula: `[persona] + [use-case]`, targets long-tail keywords. E.g. "Project management for designers", "Task tracking for developers".

**Hub and Spoke** — Hub = comprehensive overview; spokes = related subtopics.

```
/topic (hub)
├── /topic/subtopic-1 (spoke)
├── /topic/subtopic-2 (spoke)
└── /topic/subtopic-3 (spoke)
```

Create the hub first, then build spokes and interlink strategically.

**Note:** Most content works fine under `/blog`. Only use a dedicated hub/spoke URL structure for major topics with layered depth (e.g. an `/agile` guide). For typical blog posts, `/blog/post-title` is sufficient.

**Template Libraries** — High-intent keywords plus product adoption. Target searches like "marketing plan template", provide standalone value, and show how the product enhances the template.

### Shareable Content Types

**Thought Leadership** — Name a concept everyone feels but hasn't articulated; challenge conventional wisdom with evidence.

**Data-Driven Content** — Product-data analysis (anonymized), public-data analysis, or original research.

**Expert Roundups** — 15-30 experts answering one specific question. Built-in distribution.

**Case Studies** — Structure: Challenge → Solution → Results → Key learnings.

**Meta Content** — Behind-the-scenes transparency ("How We Got Our First $5k MRR").

For programmatic content at scale, hand off to the **programmatic-seo** skill.

## Content Pillars and Topic Clusters

Content pillars are the 3-5 core topics your brand will own. Each pillar spawns a cluster of related content. Most of the time all content can live under `/blog` with strong internal linking; dedicated pillar pages with custom URLs (like `/guides/topic`) are only needed for comprehensive, multi-layer resources.

### How to Identify Pillars

1. **Product-led**: What problems does your product solve?
2. **Audience-led**: What does your ICP need to learn?
3. **Search-led**: What topics have volume in your space? (from **keyword-strategy**)
4. **Competitor-led**: What are competitors ranking for?

### Pillar Structure

```
Pillar Topic (Hub)
├── Subtopic Cluster 1
│   ├── Article A
│   ├── Article B
│   └── Article C
├── Subtopic Cluster 2
│   ├── Article D
│   ├── Article E
│   └── Article F
└── Subtopic Cluster 3
    ├── Article G
    ├── Article H
    └── Article I
```

### Pillar Criteria

Good pillars align with your product/service, match what your audience cares about, have search volume or social interest, and are broad enough for many subtopics. Favor **topic-cluster coverage over one thin page per keyword**: a pillar earns rankings through the depth of its cluster, not a single page.

### Verify

Confirm the plan names a valid number of pillars (3-5), each as a `### Pillar:` entry in `content-strategy.md`:

```bash
n=$(grep -cE '^### Pillar:' content-strategy.md)
{ [ "$n" -ge 3 ] && [ "$n" -le 5 ]; } \
  && echo "OK: $n pillars" \
  || echo "FAIL: found $n pillars (need 3-5)"
```

## Keyword Coverage by Buyer Stage

Map topics to the buyer's journey using proven keyword modifiers. (Build and cluster the underlying keyword list with the **keyword-strategy** skill; here you assign each keyword to a stage.)

- **Awareness** — "what is", "how to", "guide to", "introduction to". E.g. "What is Agile Project Management".
- **Consideration** — "best", "top", "vs", "alternatives", "comparison". E.g. "Asana vs Trello vs Monday".
- **Decision** — "pricing", "reviews", "demo", "trial", "buy". E.g. "[Product] Reviews".
- **Implementation** — "templates", "examples", "tutorial", "how to use", "setup". E.g. "Step-by-Step Setup Tutorial".

## Content Ideation Sources

1. **Keyword data** — from a keyword export (via **keyword-strategy**), read for clusters, buyer stage, intent, quick wins (low competition + decent volume + high relevance), and content gaps.
2. **Call transcripts** — extract questions (→ FAQ/blog), pain points (in customer words), objections (→ proactive content), voice-of-customer phrasing, and competitor mentions.
3. **Survey responses** — mine open-ended answers for topics and language; a theme mentioned by 30%+ of respondents is high priority.
4. **Forum research** — `site:reddit.com [topic]` and `site:quora.com [topic]`, plus Indie Hackers, Hacker News, Product Hunt. Extract FAQs, misconceptions, debates, and terminology.
5. **Competitor analysis** — find their content with `site:competitor.com/blog`; note top posts, repeated topics, gaps, and outdated pieces you can beat.
6. **Sales and support input** — common objections, repeated questions, ticket patterns, success stories, and feature requests with their underlying problems.

## Prioritizing Content Ideas

Score each idea on four factors (a ranking rubric, not a traffic forecast):

| Factor | Weight | What it asks |
|--------|:------:|--------------|
| **Customer Impact** | 40% | How often did this come up in research? How many customers face it? How charged is the pain? |
| **Content-Market Fit** | 30% | Does it align with what the product solves? Can you offer unique, customer-backed insight? |
| **Search Potential** | 20% | Monthly search volume, competitiveness, long-tail options, growing vs declining interest. |
| **Resource Requirements** | 10% | Do you have the expertise and assets (data, graphics, examples) to make it authoritative? |

### Scoring Template

| Idea | Customer Impact (40%) | Content-Market Fit (30%) | Search Potential (20%) | Resources (10%) | Total |
|------|----------------------|-------------------------|----------------------|-----------------|-------|
| Topic A | 8 | 9 | 7 | 6 | 8.0 |
| Topic B | 6 | 7 | 9 | 8 | 7.1 |

## The Output Plan

Write the strategy to `content-strategy.md` with three required sections.

1. **Content Pillars** — a `## Content Pillars` heading, then 3-5 `### Pillar: <name>` entries, each with its rationale, product tie-in, and subtopic clusters.
2. **Priority Topics** — a `## Priority Topics` heading with a table whose header is exactly:

   `| Topic | Searchable/Shareable | Content Type | Target Keyword | Buyer Stage | Rationale |`

   Each row's **Buyer Stage** is one of `Awareness` / `Consideration` / `Decision` / `Implementation`, and every row carries a searchable-vs-shareable call, a content type, and a target keyword.
3. **Topic Cluster Map** — a `## Topic Cluster Map` heading with a fenced tree showing pillar → cluster → article and the internal-link relationships.

### Verify

Confirm every priority topic carries the four required attributes and a valid buyer stage:

```bash
grep -q 'Searchable/Shareable' content-strategy.md \
  && grep -q 'Content Type' content-strategy.md \
  && grep -q 'Target Keyword' content-strategy.md \
  && grep -qE '\| (Awareness|Consideration|Decision|Implementation) \|' content-strategy.md \
  && echo "OK: priority-topic attributes present" \
  || echo "FAIL: a priority-topic attribute (searchable/shareable, content type, target keyword, or buyer stage) is missing"
```

### Verify

Confirm the plan includes the topic-cluster map:

```bash
grep -q '## Topic Cluster Map' content-strategy.md \
  && echo "OK: cluster map present" \
  || echo "FAIL: content-strategy.md has no '## Topic Cluster Map'"
```

## References

- **[Headless CMS Guide](references/headless-cms.md)** — when the plan needs a place for content to live: CMS selection, content modeling for marketing (types, SEO fields), editorial workflows, and a Sanity/Contentful/Strapi comparison. Model a content type per pillar's recurring format so the roadmap and the CMS schema stay in sync.

## Related Skills

- **keyword-strategy** — build and cluster the keyword list this plan consumes (discovery, intent, difficulty).
- **programmatic-seo** — templated pages at scale from a data source; the hand-off for scaled content.
- **ai-seo** — per-site tactics for getting cited by AI search, judged against a specific deployment's evidence.
- **geo-plan** — decide what to build specifically for AI-search citation.
- **seo-plan** / **seo** — the overall SEO plan and on-page/technical execution this content program sits inside.

## Attribution

Derived from **coreyhaines31/marketingskills/content-strategy** (MIT license), an upgraded, era-verified derivative. The vendored reference `references/headless-cms.md` originates from the same MIT skill and was modified as described above. This derivative is released under the MIT license.
