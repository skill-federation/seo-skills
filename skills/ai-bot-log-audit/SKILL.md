---
name: ai-bot-log-audit
description: Method for reading Apache and Nginx access-log evidence to establish what GPTBot, ClaudeBot,
  PerplexityBot and peers actually fetch, skip, or error on, and which fixes each fetch pattern calls
  for. Reach for it when a citation-gap theory needs log rows behind it and you can export the raw logs.
  Domesticated 2026-08; the bot roster is carried from the wild source's 2026 table, not independently
  re-checked.
license: MIT
treatment: derivative
derived_from:
- id: guia-matthieu/clawfu-skills/ai-bot-log-audit
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: 8dfc675b2b1824bf3b82388da4c81c4bc598bbf0b27f05d73a02d38004ec1dfd
targeted_version: wild-2026 AI-crawler user-agent table, domesticated 2026-08
last_verified_at: 2026-08-10
---

# AI Bot Log Audit

> Analyze server logs to understand how AI crawlers retrieve your content, then optimize placement and structure for maximum citation probability. Based on Metehan Yeşilyurt's log file analysis framework.

## Conditions

### When to use

- You have — or can export — Apache or Nginx access logs, and you want to know what AI crawlers actually fetch, skip, and error on, instead of arguing from theory.
- Your content exists but AI search rarely or never cites it, and the diagnosis should start from crawl evidence rather than from a content rewrite.
- You are scoping GEO work and need to know which pages the bots already prioritize, how often they return, and where crawl budget is being wasted.
- You changed robots.txt, URL structure, or internal linking and want before/after evidence of the effect on AI-bot access.
- Typical operators: SEO professionals adding AI search to their scope, publishers monitoring AI traffic and content extraction, technical SEOs running log-file analysis, content strategists deciding what to optimize for AI visibility.

### When NOT to use

- Without log access. This document cannot read your logs for you — you bring the log data, this document brings the method. If the logs cannot be produced, stop: no phase below has a theory-only fallback.
- On analytics exports. Web-analytics dashboards are built around human sessions; the fetches this audit studies live in server access logs, and those are the only input the commands below accept.
- For page-quality questions detached from crawl behavior. Only Phase 4 touches on-page structure, and only as placement for retrieval — a content-quality audit is a different job.
- To check citation status. This method cannot query live AI search results — whether ChatGPT, Perplexity, or AI Overviews currently cite you is knowledge you bring from outside; the Phase 2 "fetches but doesn't cite" row consumes that knowledge, it cannot produce it.
- To promise outcomes. Crawl evidence improves the odds of citation; nothing in this method can guarantee that any AI product will cite you.
- As a substitute for a specialist. Per the base's own boundary, this method does not replace technical SEO expertise for complex log analysis — sampled logs, multi-CDN merges, and bot-mitigation layers need one.

### Prerequisites

- Apache or Nginx access logs in combined log format, covering a window long enough to show frequency patterns (weeks, not hours). The commands below index fields by that format: user agent is field 6 when splitting on double quotes, request path is field 7, timestamp is field 4, status is field 9.
- A shell with grep, awk, sort, uniq, and wc; curl for the Phase 4 placement check.
- Knowledge of where your logs actually originate (origin server vs CDN). CDN log exports use their own layouts — map their fields to the combined-format positions before running anything.

### What breaks first

- No logs → no evidence → the audit stops. Do not fall back to theory: a scored report written without log rows is exactly the confident-but-unverified artifact this method exists to displace.
- A custom LogFormat silently shifts the awk field positions and produces plausible-looking garbage (paths tallied as user agents, status codes as paths). The field sanity check in Phase 1's Verify catches this — run it before trusting any count.
- The bot roster goes stale as vendors add crawlers — and the roster here is the wild source's 2026 table, not independently re-checked (see Era). The Phase 2 reconciliation flags hits that the tally pattern no longer covers.
- User-agent strings in logs are self-declared and can be spoofed by scrapers borrowing a well-known bot name. Treat UA-only identification as provisional, and check the operator documentation listed under References before reading a surprising spike as genuine vendor traffic.

## Era

- The user-agent roster in Phase 1 is carried unchanged from the wild source's 2026 table; as of 2026-08 it has not been independently checked against operator documentation. The stamp dates the roster — it does not certify it. Read the rows as the wild author's claims, including the parenthetical that Google-Extended is deprecated and folded into Googlebot and the robots.txt-compliance column, and let your own logs arbitrate which of these names actually appear in your traffic (Phase 1's count puts evidence behind exactly that question). One row is not just unverified but disputed within this bundle: the Google-Extended deprecation parenthetical contradicts the bundle's Stage 2.5 adjudication, under which the four members that instruct robots.txt policy treat Google-Extended as a live opt-out token whose effect on AI Overviews inclusion is unverified — do not conclude from this table that the token is inert.
- Google retired FAQ rich results for every site on 2026-05-07. The FAQ advice in Phase 4 and in the checklist survives that retirement because it is about LLM attention at document edges, not about Google display features — do not convert it into FAQPage structured data in expectation of a rich result; that channel is closed.
- Per the 2026-07-30 editorial this derivative comes from, llms.txt is a proposed convention at roughly 0.015% adoption with no vendor confirmation that any major AI system reads it. If it comes up during an audit, settle it from your own logs (see the evidence check in Phase 2) rather than from advocacy in either direction; it earns no place among the report's recommendations without log rows behind it.

## Methodology Foundation

**Source Expert:** Metehan Yeşilyurt (SEO Consultant, speaker at BrightonSEO, The Search Session)

**Core Thesis:** Log file analysis reveals the real mechanics of AI search retrieval. Different AI products (AI Overviews, AI Mode, Perplexity) use fundamentally different retrieval pipelines, so optimizing for "AI search" requires understanding each product's specific crawl and retrieval behavior.

> "AI Overviews, AI Mode, and Web Guide are three completely different products with different retrieval behaviors. You can't optimize for 'AI search' as if it's one thing." — Metehan Yeşilyurt, The Search Session

**Key Insight:** The shift from traditional SEO to AI search optimization is from chasing clicks in deterministic SERPs to chasing citations in machine-generated text. Log files reveal the mechanics behind citation selection.

## What Claude Does vs What You Decide

| Claude Does | You Decide |
|-------------|------------|
| Guides log analysis methodology | Which log data to provide |
| Identifies patterns in crawl behavior | Strategic priority of AI products |
| Recommends content placement optimizations | Content creation/modification scope |
| Maps retrieval behavior to optimization actions | Resource allocation for changes |
| Creates audit templates and checklists | Which recommendations to implement |

## What This Skill Does

When invoked, I will guide you through:

1. **Log Collection** — Identify and extract AI bot activity from server logs
2. **Bot Identification** — Map user agents to AI products
3. **Crawl Pattern Analysis** — Understand what AI bots fetch and ignore
4. **Retrieval Mechanics** — Learn how each AI product processes your content
5. **Optimization Actions** — Specific changes to improve AI citation probability

## Phase 1: AI Bot Identification

#### Known AI Crawlers (2026 roster per the wild source — see Era)

| Bot User Agent | Operator | Purpose | Respects robots.txt? |
|---------------|----------|---------|---------------------|
| **GPTBot** | OpenAI | Training data + ChatGPT Browse | Yes |
| **ChatGPT-User** | OpenAI | Real-time browsing in ChatGPT | Yes |
| **OAI-SearchBot** | OpenAI | SearchGPT / ChatGPT Search | Yes |
| **ClaudeBot** | Anthropic | Training data collection | Yes |
| **PerplexityBot** | Perplexity | Real-time search + answer generation | Yes (mostly) |
| **Google-Extended** | Google | Gemini/AI training (deprecated — now part of Googlebot: the wild author's claim, disputed — see Era; the bundle's other members treat this as a live opt-out token whose AI Overviews effect is unverified) | N/A (same disputed claim) |
| **Googlebot** | Google | Traditional crawl + AI Overviews + AI Mode | Yes |
| **Bytespider** | ByteDance | Training for TikTok AI features | Yes |
| **CCBot** | Common Crawl | Open dataset used by many AI models | Yes |
| **Applebot-Extended** | Apple | Apple Intelligence features | Yes |

#### Log Extraction Commands

```bash
# Extract all AI bot hits from Apache/Nginx access logs
grep -iE "(GPTBot|ChatGPT-User|OAI-SearchBot|ClaudeBot|PerplexityBot|Bytespider|CCBot|Applebot-Extended)" access.log > ai_bots.log

# Count hits by bot
awk -F'"' '{print $6}' ai_bots.log | grep -oE "(GPTBot|ChatGPT-User|OAI-SearchBot|ClaudeBot|PerplexityBot|Bytespider|CCBot|Applebot-Extended)" | sort | uniq -c | sort -rn

# Top pages crawled by AI bots
awk '{print $7}' ai_bots.log | sort | uniq -c | sort -rn | head -50

# Crawl frequency by day
awk '{print $4}' ai_bots.log | cut -d: -f1 | tr -d '[' | sort | uniq -c

# Response codes for AI bots (are they getting 200s or errors?)
awk '{print $9}' ai_bots.log | sort | uniq -c | sort -rn
```

### Verify — extraction produced rows and the fields line up

```bash
# Guard: rows must exist before any analysis proceeds
wc -l < ai_bots.log    # 0 means either no AI-bot traffic in this window or the wrong file/format - stop and determine which

# Field sanity: field 6 must print user-agent strings, not paths or status codes
awk -F'"' '{print $6}' ai_bots.log | head -5
```

An empty `ai_bots.log` is itself a finding (no AI-bot access at all) only after you have confirmed the log file and its format are right — the two failure modes look identical until you check. If the field sanity check prints paths or numbers instead of user agents, your LogFormat is not the combined format this document assumes; fix the field mapping before any tally.

## Phase 2: Crawl Pattern Analysis

#### What to Look For

| Pattern | What It Means | Action |
|---------|--------------|--------|
| **Bot fetches page frequently** | Page is in retrieval index, content matters | Optimize this page first |
| **Bot fetches page once then stops** | Page was evaluated and deprioritized | Improve content quality/freshness |
| **Bot never fetches a page** | Page not discovered or blocked | Check internal linking, sitemap, robots.txt |
| **Bot gets 404/500** | Technical issue blocking retrieval | Fix immediately |
| **Bot fetches but doesn't cite** | Content retrieved but not selected for answers | Improve structure, uniqueness, authority |

Where the action rows exit this document: structure, uniqueness, and markup changes are implemented with the bundle's implementation reference (seo), and which engine deserves that work is the strategy layer's call (ai-seo) — this audit supplies the log evidence both act on.

#### Crawl Budget Analysis

AI bots have crawl budgets like traditional bots. If your site is large:

```
QUESTIONS TO ANSWER:
1. What % of pages are being crawled by AI bots?
2. Are high-value pages being fetched?
3. Are AI bots wasting time on low-value pages (tag pages, pagination)?
4. What's the crawl frequency — daily? weekly? sporadic?
5. Do different AI bots prioritize different pages?
```

#### Comparative Bot Behavior

Map how each bot interacts with your site differently:

```
ANALYSIS TEMPLATE:

GPTBot:
  Pages fetched: ___
  Top pages: ___
  Crawl frequency: ___
  Response codes: ___

PerplexityBot:
  Pages fetched: ___
  Top pages: ___
  Crawl frequency: ___
  Response codes: ___

ClaudeBot:
  Pages fetched: ___
  Top pages: ___
  Crawl frequency: ___
  Response codes: ___
```

Evidence beats convention debates. Questions like "should we ship llms.txt" are settled by your own logs, not by advocacy (see Era):

```bash
# Has any AI bot ever fetched it? Two counts: AI bots specifically, then all traffic
grep -c "llms.txt" ai_bots.log
grep -c "llms.txt" access.log
```

### Verify — the per-bot tally accounts for every extracted line

```bash
total=$(wc -l < ai_bots.log)
tallied=$(awk -F'"' '{print $6}' ai_bots.log | grep -cE "GPTBot|ChatGPT-User|OAI-SearchBot|ClaudeBot|PerplexityBot|Bytespider|CCBot|Applebot-Extended")
echo "extracted=$total tallied=$tallied"

# When the numbers differ, look at the unmatched user agents themselves before touching anything
awk -F'"' '{print $6}' ai_bots.log | grep -vE "GPTBot|ChatGPT-User|OAI-SearchBot|ClaudeBot|PerplexityBot|Bytespider|CCBot|Applebot-Extended" | sort | uniq -c | sort -rn
```

The two numbers must match. A shortfall has three known causes, and only one of them is a roster gap: (1) a bot name the extraction caught that the tally alternation does not list — the defect class this derivative fixed once already (see Findings); extend both patterns together. (2) Case — the extraction is `grep -iE` but the tally is case-sensitive, so a lowercase `claudebot` extracts without tallying; re-run the tally with `-i` to test. (3) A false extraction — the extraction greps the whole log line, so a bot name inside a request path (an ordinary browser fetching /blog/what-is-gptbot) lands in ai_bots.log without being a bot visit at all. The unmatched-agents listing above distinguishes the three. Extend the roster only after ruling out (2) and (3).

## Phase 3: Understanding Retrieval Mechanics

Each AI product uses a different retrieval pipeline. Optimizing requires understanding the mechanics.

#### Perplexity: Embedding Similarity + Source Diversification

Perplexity uses high embedding similarity to match content to queries, then actively diversifies sources.

**What this means for you:**
- Semantic match matters more than keyword match
- Being the single best source isn't enough — Perplexity diversifies
- Your content needs to be retrievable AND complementary to other sources
- Structured, extractable content wins (tables, definitions, clear claims)

#### Google AI Overviews: Search Index + LLM Layer

AI Overviews sit on top of existing Google Search rankings. Your traditional SEO signals matter.

**What this means for you:**
- If you don't rank on page 1 for traditional search, you're unlikely to appear in AI Overviews
- The AI layer selects from already-ranked pages and synthesizes
- E-E-A-T signals are inherited from search ranking

#### Google AI Mode: Multi-Step Query Fan-Out

AI Mode decomposes complex questions into sub-queries, retrieves for each, then synthesizes.

**What this means for you:**
- Content that answers sub-questions gets included
- Comprehensive topical coverage across your site matters
- Internal linking between related topics helps AI Mode stitch answers together

### Verify — optimize only for pipelines that actually touch this site

```bash
# Separate answer-time fetching from index building and training collection
grep -c "ChatGPT-User" ai_bots.log     # real-time browsing fetches
grep -c "OAI-SearchBot" ai_bots.log    # search-index fetches
grep -c "GPTBot" ai_bots.log           # training-data fetches
```

If a product family shows zero fetches across a meaningful window, its optimization advice in this phase is not yet actionable for this site — fix discovery and access first (the Phase 2 pattern table) before investing in placement.

## Phase 4: LLM Vulnerability Awareness

Understanding known LLM processing weaknesses helps you position content for maximum retrieval.

#### 4 Key LLM Vulnerabilities

| Vulnerability | Description | Optimization |
|--------------|-------------|-------------|
| **Recency bias** | LLMs weight recent information higher, even when older info is more accurate | Date your content clearly. Update regularly. Recent timestamps = retrieval advantage |
| **Lost-in-the-middle** | LLMs process beginnings and endings of context better than middles | Place key claims, definitions, and statistics at the START and END of pages/sections |
| **Data poisoning susceptibility** | LLMs can be influenced by coordinated content patterns | Not actionable for you, but be aware: competitors can game AI answers |
| **Prompt injection** | LLMs can be manipulated via hidden instructions | Not actionable for SEO, but relevant for security audits |

#### Lost-in-the-Middle: Practical Content Placement

This is the most actionable vulnerability for SEO:

```
PAGE STRUCTURE FOR LLM RETRIEVAL:

TOP (HIGH ATTENTION):
├── Key definition / direct answer
├── Critical statistics with context
└── Main claim / thesis

MIDDLE (LOW ATTENTION):
├── Supporting details
├── Tables and structured data (LLMs handle these well regardless of position)
├── Examples and elaboration
└── Supporting evidence

BOTTOM (HIGH ATTENTION):
├── Summary of key points
├── FAQ with direct answers
├── Conclusion with standalone claims
└── Updated date
```

> "FAQs at the end of the page, tables in the middle — that's the lost-in-the-middle fix. LLMs handle structured data well regardless of position, but flowing text in the middle gets deprioritized." — Metehan Yeşilyurt

### Verify — the served HTML carries claims at the edges

```bash
# Crawlers read served HTML, not the rendered viewport: check edge placement in what the server returns
URL="https://example.com/page"; CLAIM="the page's key claim phrase"; SUMMARY="a phrase from the closing summary"
curl -s "$URL" > /tmp/page.html    # fetched once into /tmp/page.html so both edge checks measure the same bytes
total=$(wc -c < /tmp/page.html)
head -c $((total / 5)) /tmp/page.html | grep -Fci "$CLAIM"      # expect >= 1
tail -c $((total / 5)) /tmp/page.html | grep -Fci "$SUMMARY"    # expect >= 1
```

Run this after restructuring a page: both greps returning at least 1 confirms the key claim sits in the leading fifth of the served document and the summary in the trailing fifth — the placement this phase argues for. The greps treat the phrases as literal fixed strings (`-F`), so pick short plain fragments: a phrase broken across a line break, or rewritten by HTML entity encoding (an apostrophe becoming `&#39;`), returns a false zero. A zero therefore means: check the phrase choice first, then whether the edit shipped at all or lives only in a client-side render.

## Phase 5: Audit Report Template

#### AI Bot Log Audit Report

```markdown
# AI Bot Log Audit: [Site Name]
**Date:** [Date]
**Period analyzed:** [Date range]
**Log source:** [Apache/Nginx/CDN]

## Executive Summary
[Two or three sentences: what the logs showed]

## Bot Activity Overview

| Bot | Total Hits | Unique Pages | Avg Daily Hits | Status |
|-----|-----------|-------------|----------------|--------|
| GPTBot | ___ | ___ | ___ | Active/Inactive |
| PerplexityBot | ___ | ___ | ___ | Active/Inactive |
| ClaudeBot | ___ | ___ | ___ | Active/Inactive |
| ChatGPT-User | ___ | ___ | ___ | Active/Inactive |

## Top Pages by AI Bot Activity
1. [URL] — [hits] hits — [which bots]
2. [URL] — [hits] hits — [which bots]
3. [URL] — [hits] hits — [which bots]

## Pages Not Crawled (Expected High-Value)
- [URL] — Likely cause: [blocked/not linked/low authority]
- [URL] — Likely cause: [___]

## Technical Issues
- [N] pages returning 404 to AI bots
- [N] pages returning 500 to AI bots
- robots.txt blocking: [yes/no — which bots?]

## Content Optimization Recommendations

### Priority 1: Fix Technical Issues
- [ ] [Specific fix]

### Priority 2: Optimize High-Traffic AI Pages
- [ ] Apply lost-in-the-middle structure to [page]
- [ ] Add entity schema to [page]
- [ ] Update freshness signals on [page]

### Priority 3: Improve Discoverability
- [ ] Internal link to [uncrawled page] from [crawled hub]
- [ ] Add to sitemap: [page]
- [ ] Create content for [gap topic]

## robots.txt Recommendations
[Current AI bot directives and recommended changes]
```

### Verify — the report is finished and every number is real

```bash
# A finished report contains no unfilled ___ blanks
grep -c "___" ai_bot_audit_report.md    # the passing output is 0

# The template's bracket placeholders should be gone too
grep -cE "\[(Site Name|Date range|Date|URL|N|hits|which bots|gap topic|Specific fix|page|blocked/not linked/low authority)\]" ai_bot_audit_report.md    # the passing output is 0
```

These two greps cover the template's own placeholders — the ___ blanks and the bracket placeholders it ships with. They cannot catch a placeholder you introduced yourself, so read the report once with human eyes before it leaves you. Every figure in the report must trace to the output of a command in Phases 1–3 run against this site's logs. A number that cannot be traced is an estimate — remove it. An audit with three verified findings outranks one with twelve plausible ones.

Hand-offs from a finished report: the recommended structure and markup changes route to the bundle's implementation reference (seo); whether each is worth doing, and for which engine, is adjudicated by the strategy layer (ai-seo).

## Examples

### Example 1: Publisher Losing AI Traffic

**Context:** News publisher noticed declining traffic from AI referrals. Log audit reveals:

**Findings:**
- GPTBot hits dropped 60% after robots.txt change (accidentally blocked)
- PerplexityBot only crawling homepage and top 5 articles
- Most content pages have zero AI bot visits
- AI bots hitting 404s on URL structure that changed 3 months ago

**Actions:**
1. Fix robots.txt — allow GPTBot and PerplexityBot
2. Add 301 redirects for old URL structure
3. Improve internal linking from high-crawl pages to deep content
4. Add article schema with datePublished and dateModified
5. Restructure top articles with lost-in-the-middle optimization

### Example 2: SaaS Blog Not Getting AI Citations

**Context:** SaaS company publishes weekly blog but never appears in ChatGPT or Perplexity answers.

**Findings:**
- ClaudeBot and GPTBot crawl regularly (technical access is fine)
- Content is generic ("10 Tips for..." format) — interchangeable with competitors
- No original data, case studies, or unique insights
- Author pages have no Person schema
- Brand search volume: 100/month (competitors: 3,000+)

**Actions:**
1. Content strategy shift: original research > generic guides
2. Add Person schema for all authors with credentials
3. Place unique data/claims at start and end of articles (lost-in-the-middle)
4. Build entity authority for 2 key authors (podcast appearances, guest posts)
5. Create comparison content where their product is one of the compared options

## Checklists & Templates

### Quick Audit Checklist

```
ACCESS CHECK
[ ] AI bots not blocked in robots.txt (check each bot separately)
[ ] AI bots getting 200 responses (not 403/404/500)
[ ] Sitemap accessible and up to date
[ ] Key pages present in sitemap

CRAWL PATTERNS
[ ] High-value pages are being crawled by AI bots
[ ] Crawl frequency is consistent (not declining)
[ ] AI bots not wasting budget on low-value pages
[ ] Multiple AI bots active (not just one)

CONTENT OPTIMIZATION
[ ] Key claims at beginning and end of pages (not buried in middle)
[ ] Tables and structured data for comparisons
[ ] FAQ sections at bottom of major pages
[ ] Content is updated with recent dates
[ ] Unique data or original insights present

ENTITY SIGNALS
[ ] Author/organization schema on relevant pages
[ ] Entity mentioned consistently across the site
[ ] Cross-platform entity presence established
```

## References

**Primary Sources:**
- Metehan Yeşilyurt — "Log Files, AI Bots, and the Real Mechanics of AI Search" (The Search Session, Advanced Web Ranking)
- Mark Williams-Cook — Signal decay thesis and query fan-out analysis
- Lily Ray — Entity-first framework and cross-platform authority

**Tools Referenced:**
- Screaming Frog Log File Analyzer
- GoAccess (open-source log analyzer)
- queryfan.com (query fan-out analysis)

**Technical References:**
- OpenAI GPTBot documentation
- Anthropic ClaudeBot documentation
- Google Search Central — Googlebot and AI features

## Attribution

- Base: `guia-matthieu/clawfu-skills/ai-bot-log-audit` — MIT. The wild document credits its methodology to Metehan Yeşilyurt's log-file analysis framework (The Search Session); that credit is preserved in Methodology Foundation and References above.
- This derivative: MIT. No graft sources; no vendored files.
