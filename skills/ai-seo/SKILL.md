---
name: ai-seo
description: 'The GEO/AEO strategy layer for agents, current to Google''s 2026 guidance split: answer
  features ride core ranking while ChatGPT, Claude, and Perplexity reward extractable structure. Load
  it when planning how a site earns AI citations, before any page edits. It interviews, adjudicates tactics
  per engine, and emits an evidence-tagged plan; it executes nothing, so pair it with an audit skill that
  actually fetches the site.'
license: MIT
treatment: derivative
derived_from:
- id: coreyhaines31/marketingskills/ai-seo
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: cb70d0b5daf4cfe3cad30ca897007347bb3dc150c9384497334dbd9122c0143c
- id: b1rdmania/ghostclaw/ai-seo
  role: superseded
  license_at_derivation: MIT
  content_hash_at_derivation: 7ef9eac488baafde07c816f6c24c1b250995bef730882cc05e4dfe32978d93eb
targeted_version: 2.2.0
last_verified_at: 2026-08-10
---

# AI SEO — the strategy layer

Domesticated derivative of the coreyhaines31/marketingskills `ai-seo` skill: the briefing an agent loads before it plans or edits anything for AI-search visibility. You are an expert in AI search optimization — the practice of making content discoverable, extractable, and citable by AI systems including Google AI Overviews, ChatGPT, Perplexity, Claude, Gemini, and Copilot. Your goal is to help users get their content cited as a source in AI-generated answers — via a plan whose every claim names its evidence, not via anything this document runs itself.

## Conditions

### When to use

- Planning how a site earns citations in AI-generated answers (Google AI Overviews / AI Mode, ChatGPT, Perplexity, Claude, Gemini, Copilot) — before any page is edited.
- Adjudicating tactic-to-engine fit: what Google's stated position permits versus what the other engines reward. This separation is the document's core value.
- Producing the strategy artifact (`ai-seo-plan.md`, defined below) that an executing audit or implementation skill then works from.
- Reviewing someone else's GEO/AEO proposal for era-stale or engine-misattributed tactics.

### When NOT to use

- **As evidence about a live site's current state.** This is the strategy layer: it asks questions and produces a plan; it runs nothing. It never fetches a page, reads a robots.txt, renders JavaScript, or scores anything. Any claim about what a site *currently* does must come from a paired executing audit skill — one that declares Bash/WebFetch-class tools and actually inspects the site — never from this document. In this bundle that executing role is filled by geo-technical (the full eight-category live inspection), geo-audit (the fast scored ~30-second check), or claude-seo (the suite audit behind its own runtime). A plan produced here that states site facts nobody fetched is the exact confident-report failure this collection exists to prevent.
- For traditional technical and on-page SEO audits (crawlability, indexation, Core Web Vitals) — different job, different tooling.
- For implementing structured data. This document says which schema types matter for AI extraction and why; writing the JSON-LD belongs to a schema-focused skill or your build pipeline.

### Prerequisites

- The business context this skill interviews for: key queries, content types, competitors, goals. If `.agents/product-marketing.md` exists (or `.claude/product-marketing.md`, or the legacy `product-marketing-context.md` filename in older setups), read it before asking questions and only ask for what it does not cover.
- A place to write the plan artifact — this document standardizes on `ai-seo-plan.md` and `ai-seo-monitoring.md` in the working directory.
- For Verify steps marked *post-implementation*: shell access (an executing agent or a human) to run the fenced commands against the produced artifacts and, later, the deployed site.

### What breaks first

- **Platform behavior claims.** The engine-landscape table, the citation-share percentages, and the monitoring-tool list are the fastest-rotting parts of this document — vendors change retrieval backends and features without notice.
- **Vendor stances.** Google's published position, quoted in the Era section, can be superseded by newer guidance; when anything here conflicts with a newer dated statement from the vendor, the newer statement wins and this document needs re-verification.
- **OKF.** The Open Knowledge Format is v0.1; breaking changes are possible below 1.0.
- **The same-name fork trap this derivative exists to fix:** copies of this skill circulate frozen at older versions behind near-identical descriptions. Check the version stamp in Era before trusting any copy found in the wild.

## Era

**Version stamp.** This derivative targets the 2.2.0 line of coreyhaines31/marketingskills/ai-seo; the same-name fork b1rdmania/ghostclaw/ai-seo is frozen at 1.1.0 and is missing the Google-stance section and the query fan-out material — behind a description that reads almost identically (the newer line adds a handful of trigger phrases and nothing else on the surface). Both bodies were read and compared for this derivative on 2026-08-10. Nothing in either wild listing warns an installer of the gap; this stamp is the warning.

Dated facts this document encodes, each dated where its source dates it:

- **Google's stated position** (from Google's AI-features optimization guide as quoted in the base at v2.2.0; verified present in the base body on 2026-08-10 — no one in this pipeline fetched the live guide): Google's generative AI features on Search are rooted in its core Search ranking and quality systems — nothing has to be added to a page for them. No special markup, no AI files, no separate AI variant of the content. Going further: producing an AI-targeted variant of your content falls under Google's scaled-content spam policy — the base carries the policy name as Google's words ("scaled content abuse"); the categorical "falls under" form is the batch editorial's reading (2026-07-30).
- **The Princeton GEO method ranking:** the Princeton GEO study (KDD 2024) ranks citing sources at the top of its nine-method list at roughly +40% visibility, while keyword stuffing at the bottom actively costs roughly 10%. Note this is a ranking of *optimization methods*, not of positions on a page.
- **Open Knowledge Format:** introduced by Google in June 2026 (2026-06-12 per the vendored reference), v0.1, built for data-team catalog metadata; no confirmed AI-search ranking signal exists for it today.
- **From the batch-940 editorial review (published 2026-07-30):** Google retired FAQ rich results for every site on May 7, 2026; HowTo rich results have been deprecated since Sept 2023; and no major AI vendor has confirmed that it reads `llms.txt`. These three dates gate several recommendations below.

## The Plan Artifact

Everything this skill produces goes into `ai-seo-plan.md`, in this shape — the Verify steps below grep it, so the shape is load-bearing:

```markdown
# AI SEO Plan — [site]

## Context
- Q: [intake question] — A: [answer or "unknown"]

## Visibility Audit
[the query table and bot-access evidence from the audit section]

## Recommendations
### R1. [title]
Engines: [Google AI Overviews | ChatGPT | Perplexity | Claude | Copilot | all-non-Google]
Evidence: [the section of this skill, the reference file, or the audit finding that justifies it]
[the recommendation]

## Monitoring
[cadence and metric choices; the running log lives in ai-seo-monitoring.md]
```

Two hard rules for the artifact: every recommendation carries an `Engines:` line (tactics are engine-scoped in this document — an unscoped tactic is an adjudication skipped), and every recommendation carries an `Evidence:` line. A recommendation that cannot name its evidence is dropped, not softened.

## Before Starting

Gather this context (ask if not provided, after checking the product-marketing file named in Prerequisites):

### 1. Current AI Visibility
- Do you know if your brand appears in AI-generated answers today?
- Have you checked ChatGPT, Perplexity, or Google AI Overviews for your key queries?
- What queries matter most to your business?

### 2. Content & Domain
- What type of content do you produce? (Blog, docs, comparisons, product pages)
- What's your domain authority / traditional SEO strength?
- Do you have existing structured data (schema markup)?

### 3. Goals
- Get cited as a source in AI answers?
- Appear in Google AI Overviews for specific queries?
- Compete with specific brands already getting cited?
- Optimize existing content or create new AI-optimized content?

### 4. Competitive Landscape
- Who are your top competitors in AI search results?
- Are they being cited where you're not?

### Verify

The intake is recorded, and unknowns are marked rather than guessed:

```bash
grep -q "^## Context" ai-seo-plan.md || echo "FAIL: no Context section"
n_q=$(grep -c "^- Q:" ai-seo-plan.md)
n_a=$(grep -c "— A: " ai-seo-plan.md)
echo "questions=$n_q answered=$n_a (must be equal; 'unknown' is a valid answer, a missing '— A:' segment is not)"
```

## How AI Search Works

### The AI Search Landscape

| Platform | How It Works | Source Selection |
|----------|-------------|----------------|
| **Google AI Overviews** | Summarizes top-ranking pages | Strong correlation with traditional rankings |
| **ChatGPT (with search)** | Searches web, cites sources | Draws from wider range, not just top-ranked |
| **Perplexity** | Always cites sources with links | Favors authoritative, recent, well-structured content |
| **Gemini** | Google's AI assistant | Pulls from Google index + Knowledge Graph |
| **Copilot** | Bing-powered AI search | Bing index + authoritative sources |
| **Claude** | Brave Search (when enabled) | Training data + Brave search results |

For a deep dive on how each platform selects sources and what to optimize per platform, see [references/platform-ranking-factors.md](references/platform-ranking-factors.md). **Dated caveat (2026-08-10):** that file is vendored exactly as fetched and predates the rich-results retirements dated in Era — its Google AI Overviews section still recommends FAQPage/HowTo schema as a Google-side lever with a "30-40% visibility boost" claim, and its closing actions list repeats it. Where that file conflicts with § Schema Markup for AI below, the Schema section wins.

### Key Difference from Traditional SEO

Traditional SEO gets you ranked. AI SEO gets you **cited**.

In traditional search, you need to rank on page 1. In AI search, a well-structured page can get cited even if it ranks on page 2 or 3 — AI systems select sources based on content quality, structure, and relevance, not just rank position.

**Stats the base carries (its figures, undated in the source — treat as order-of-magnitude, not gospel):**
- AI Overviews appear in ~45% of Google searches
- AI Overviews reduce clicks to websites by up to 58%
- Brands are 6.5x more likely to be cited via third-party sources than their own domains
- Optimized content gets cited 3x more often than non-optimized
- Statistics and citations boost visibility by 40%+ across queries

### Google's Official Stance vs. Multi-Platform Reality

This is the section the frozen 1.1.0 fork is missing, and it is the one to read before doing anything else — it decides which tactics you may honestly attach to which engine.

**Google's position** ([AI features optimization guide](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)):
> "The best practices for SEO continue to be relevant because our generative AI features on Google Search are rooted in our core Search ranking and quality systems."

Google explicitly says:
- **No special markup or files are required** for AI Overviews or AI Mode
- **Don't chunk content for AI** — write for people, organize with normal headings and paragraphs
- **Don't write separate content for AI** — that risks "scaled content abuse" spam policy
- **Helpful, reliable, people-first content** wins — same E-E-A-T standards as regular Search
- **No AI-specific Search Console reporting** — use standard SEO metrics

**Other AI engines (ChatGPT, Claude, Perplexity, Copilot) behave differently:**
- They actively reward extractable structure — passages, FAQs, comparison tables, definition blocks
- They cite third-party sources (Reddit, Wikipedia, review sites) more heavily than top-ranked pages
- Machine-readable files (`llms.txt`, structured pricing pages) are commonly recommended for them — but as of the 2026-07-30 editorial review, no major AI vendor has confirmed that it reads `llms.txt`; treat such files as cheap and speculative, never load-bearing

**What this means for the work:**
- The structural patterns in this skill (40–60 word answer blocks, FAQ schema, comparison tables) help **non-Google AI engines** materially. They also don't hurt Google — they're just normal good content organization.
- For Google AI Overviews / AI Mode specifically: optimize for people and core Search, full stop. Strong E-E-A-T, original information, semantic HTML, clean indexability.
- For ChatGPT/Claude/Perplexity: layer on the extractable structure and, if you like cheap speculative bets, the machine-readable files.
- The one-line resolution: use the structural patterns because they are good organization anyway — never sold to a client as a Google lever.

When in doubt, default to "write for people, organize for clarity" — that satisfies both camps.

### Query Fan-Out (Google AI Search)

Also missing from the 1.1.0 fork. Google's AI features don't just answer the one query a user typed — they generate **concurrent, related queries** under the hood and retrieve results for each.

Google's own example: a user asking "how to fix lawns" triggers fan-out queries about herbicides, chemical-free removal, weed prevention, etc. The AI synthesizes across all of them.

**Implications:**
- Single-page-per-keyword targeting is less effective. Cover the **full topical cluster** so you're retrievable for the fan-out variants too.
- Long-tail intent matters less than topical authority — Google's AI systems understand synonyms and semantic equivalence.
- A page that comprehensively answers a parent topic (with sub-questions covered) will be retrieved more often than narrow per-query pages.

**Action**: when planning content, brainstorm the 5–10 related queries the AI is likely to fan out to and make sure your content (or your site as a whole) covers them.

## AI Visibility Audit

Before optimizing, assess the current AI search presence. Reminder from Conditions: the steps below *prescribe* checks — running them (fetching answers, reading robots.txt) is the paired executing skill's or the operator's job, and the results are recorded as evidence in `ai-seo-plan.md`. This document supplies the method and the table shapes.

### Step 1: Check AI Answers for Your Key Queries

Test 10-20 of your most important queries across platforms:

| Query | Google AI Overview | ChatGPT | Perplexity | You Cited? | Competitors Cited? |
|-------|:-----------------:|:-------:|:----------:|:----------:|:-----------------:|
| [query 1] | Yes/No | Yes/No | Yes/No | Yes/No | [who] |
| [query 2] | Yes/No | Yes/No | Yes/No | Yes/No | [who] |

**Query types to test:**
- "What is [your product category]?"
- "Best [product category] for [use case]"
- "[Your brand] vs [competitor]"
- "How to [problem your product solves]"
- "[Your product category] pricing"

### Step 2: Analyze Citation Patterns

When your competitors get cited and you don't, examine:
- **Content structure** — Is their content more extractable?
- **Authority signals** — Do they have more citations, stats, expert quotes?
- **Freshness** — Is their content more recently updated?
- **Schema markup** — Do they have structured data you're missing?
- **Third-party presence** — Are they cited via Wikipedia, Reddit, review sites?

### Step 3: Content Extractability Check

For each priority page, verify:

| Check | Pass/Fail |
|-------|-----------|
| Clear definition in first paragraph? | |
| Self-contained answer blocks (work without surrounding context)? | |
| Statistics with sources cited? | |
| Comparison tables for "[X] vs [Y]" queries? | |
| FAQ section with natural-language questions? | |
| Schema markup (FAQ, HowTo, Article, Product — see the rich-results dating under Schema Markup for AI)? | |
| Expert attribution (author name, credentials)? | |
| Recently updated (within 6 months)? | |
| Heading structure matches query patterns? | |
| AI bots allowed in robots.txt? | |

### Step 4: AI Bot Access Check

Verify your robots.txt allows AI crawlers. Each AI platform has its own bot, and blocking it means that platform can't cite you:

- **GPTBot** and **ChatGPT-User** — OpenAI (ChatGPT)
- **PerplexityBot** — Perplexity
- **ClaudeBot** and **anthropic-ai** — Anthropic (Claude)
- **Google-Extended** — Google's opt-out control for Gemini/AI use of your content. Hedged the same way `llms.txt` is: whether blocking it affects AI Overviews inclusion is unverified by any input here (2026-08-10), and the claim sits in tension with the Era pin that Google's AI features ride core Search ranking — verify Google's current crawler guidance before treating it as an AI Overviews switch
- **Bingbot** — Microsoft Copilot (via Bing)

Check your robots.txt for `Disallow` rules targeting any of these. If you find them blocked, you have a business decision to make: blocking prevents AI training on your content but also prevents citation. One middle ground is blocking training-only crawlers (like **CCBot** from Common Crawl) while allowing the search bots listed above.

See [references/platform-ranking-factors.md](references/platform-ranking-factors.md) for the full robots.txt configuration — read it for the bot list and the robots.txt block, not for its Google-side schema claims (see the dated caveat under The AI Search Landscape). Its robots.txt block's `Google-Extended` comment also carries the unhedged AI Overviews claim addressed in the bot list above.

### Verify

The audit section of the plan holds evidence, not template residue or assumptions:

```bash
# Template placeholders still present means rows were never actually filled by a real check
grep -n "Yes/No" ai-seo-plan.md && echo "FAIL: unfilled audit rows"
# Every bot's access status is recorded from OBSERVED robots.txt lines (pasted into the plan),
# not asserted from memory
for bot in GPTBot ChatGPT-User PerplexityBot ClaudeBot Google-Extended Bingbot; do
  grep -q "$bot" ai-seo-plan.md || echo "MISSING evidence line for: $bot"
done
```

## Optimization Strategy

### The Three Pillars

```
1. Structure (make it extractable)
2. Authority (make it citable)
3. Presence (be where AI looks)
```

### Pillar 1: Structure — Make Content Extractable

AI systems extract passages, not pages. Every key claim should work as a standalone statement.

**Content block patterns:**
- **Definition blocks** for "What is X?" queries
- **Step-by-step blocks** for "How to X" queries
- **Comparison tables** for "X vs Y" queries
- **Pros/cons blocks** for evaluation queries
- **FAQ blocks** for common questions
- **Statistic blocks** with cited sources

For detailed templates for each block type, see [references/content-patterns.md](references/content-patterns.md).

**Structural rules:**
- Lead every section with a direct answer (don't bury it)
- Keep key answer passages to 40-60 words (optimal for snippet extraction)
- Use H2/H3 headings that match how people phrase queries
- Tables beat prose for comparison content
- Numbered lists beat paragraphs for process content
- Each paragraph should convey one clear idea

### Pillar 2: Authority — Make Content Citable

AI systems prefer sources they can trust. Build citation-worthiness.

**The Princeton GEO research** (KDD 2024, studied across Perplexity.ai) ranked 9 optimization methods:

| Method | Visibility Boost | How to Apply |
|--------|:---------------:|--------------|
| **Cite sources** | +40% | Add authoritative references with links |
| **Add statistics** | +37% | Include specific numbers with sources |
| **Add quotations** | +30% | Expert quotes with name and title |
| **Authoritative tone** | +25% | Write with demonstrated expertise |
| **Improve clarity** | +20% | Simplify complex concepts |
| **Technical terms** | +18% | Use domain-specific terminology |
| **Unique vocabulary** | +15% | Increase word diversity |
| **Fluency optimization** | +15-30% | Improve readability and flow |
| ~~Keyword stuffing~~ | **-10%** | **Actively hurts AI visibility** |

**Best combination:** Fluency + Statistics = maximum boost. Low-ranking sites benefit even more — up to 115% visibility increase with citations.

**Statistics and data** (+37-40% citation boost)
- Include specific numbers with sources
- Cite original research, not summaries of research
- Add dates to all statistics
- Original data beats aggregated data

**Expert attribution** (+25-30% citation boost)
- Named authors with credentials
- Expert quotes with titles and organizations
- "According to [Source]" framing for claims
- Author bios with relevant expertise

**Freshness signals**
- "Last updated: [date]" prominently displayed
- Regular content refreshes (quarterly minimum for competitive topics)
- Current year references and recent statistics
- Remove or update outdated information

**E-E-A-T alignment**
- First-hand experience demonstrated
- Specific, detailed information (not generic)
- Transparent sourcing and methodology
- Clear author expertise for the topic

### Pillar 3: Presence — Be Where AI Looks

AI systems don't just cite your website — they cite where you appear.

**Third-party sources matter more than your own site:**
- Wikipedia mentions (7.8% of all ChatGPT citations)
- Reddit discussions (1.8% of ChatGPT citations)
- Industry publications and guest posts
- Review sites (G2, Capterra, TrustRadius for B2B SaaS)
- YouTube (frequently cited by Google AI Overviews)
- Quora answers

**Actions:**
- Ensure your Wikipedia page is accurate and current
- Participate authentically in Reddit communities
- Get featured in industry roundups and comparison articles
- Maintain updated profiles on relevant review platforms
- Create YouTube content for key how-to queries
- Answer relevant Quora questions with depth

### Verify

Every recommendation the strategy produced is engine-scoped and evidence-tagged, per The Plan Artifact:

```bash
recs=$(grep -c "^### R" ai-seo-plan.md)
eng=$(grep -c "^Engines:" ai-seo-plan.md)
ev=$(grep -c "^Evidence:" ai-seo-plan.md)
echo "recommendations=$recs engines=$eng evidence=$ev (all three must be equal and > 0)"
# The Google-stance guard: no recommendation may sell an AI-specific artifact as a Google lever
grep -niE "(llms\.txt|pricing\.md|okf|answer block|faq schema).{0,80}(google (ranking|boost|lever)|boost.{0,20}ai overview)" ai-seo-plan.md \
  && echo "FAIL: a tactic is being sold as a Google lever - re-scope its Engines line"
```

## Machine-Readable Files for AI Agents

> **Google's stance**: not required for AI Overviews or AI Mode. Their guide explicitly says you don't need new markup, AI files, or markdown to appear in generative AI search.
>
> **Why consider them anyway**: non-Google AI engines and autonomous buying agents reward extractable structure, and these files are cheap. Vendor-confirmation status varies per file and is stated per file below — none of them harms Google.

AI agents aren't just answering questions — they're becoming buyers. When an AI agent evaluates tools on behalf of a user, it needs structured, parseable information. If your pricing is locked in a JavaScript-rendered page or a "contact sales" wall, agents will skip you and recommend competitors whose information they can actually read.

Add these machine-readable files to your site root:

**`/pricing.md` or `/pricing.txt`** — Structured pricing data for AI agents

```markdown
# Pricing — [Your Product Name]

## Free
- Price: $0/month
- Limits: 100 emails/month, 1 user
- Features: Basic templates, API access

## Pro
- Price: $29/month (billed annually) | $35/month (billed monthly)
- Limits: 10,000 emails/month, 5 users
- Features: Custom domains, analytics, priority support

## Enterprise
- Price: Custom — contact sales@example.com
- Limits: Unlimited emails, unlimited users
- Features: SSO, SLA, dedicated account manager
```

**Why this matters now:**
- AI agents increasingly compare products programmatically before a human ever visits your site
- Opaque pricing gets filtered out of AI-mediated buying journeys
- A simple markdown file is trivially parseable by any LLM — no rendering, no JavaScript, no login walls
- Same principle as `robots.txt` (for crawlers) — a well-known path with predictable structure

**Best practices:**
- Use consistent units (monthly vs. annual, per-seat vs. flat)
- Include specific limits and thresholds, not just feature names
- List what's included at each tier, not just what's different
- Keep it updated — stale pricing is worse than no file
- Link to it from your sitemap and main pricing page

**`/llms.txt`** — Context file for AI systems (see [llmstxt.org](https://llmstxt.org))

A proposed convention: a root file giving AI systems a quick overview of what your product does, who it's for, and links to key pages. Status, dated: as of the 2026-07-30 editorial review, no major AI vendor has confirmed that it reads `llms.txt`. It costs minutes and cannot hurt, so shipping one is a reasonable speculative bet — but it never appears in a plan as a load-bearing fix, and never as a Google tactic.

**`/okf/` — Open Knowledge Format bundle (Google-backed, v0.1)**

Google [introduced OKF](https://cloud.google.com/blog/products/data-analytics/how-the-open-knowledge-format-can-improve-data-sharing) in June 2026 — a markdown spec for representing site content as a directory of cross-linked files with YAML frontmatter, agent-readable without scraping. Built primarily for data-team catalog metadata; the site-readable-by-agents repurposing was popularized by Suganthan Mohanadasan. No confirmed AI-search ranking signal today — treat it as protocol-layer registration like early schema.org. **For the full breakdown, implementation paths (free generator, WordPress plugin, by-hand), hosting guidance, and when to skip, see [references/okf.md](references/okf.md).**

### Verify

*Post-implementation.* Once the paired implementation ships the files the plan called for, confirm they are actually served as plain parseable text:

```bash
# pricing.md serves as markdown, not an HTML shell or a redirect to a rendered page
curl -sf https://yoursite.com/pricing.md | head -5
curl -sf https://yoursite.com/pricing.md | grep -qi "<html" && echo "FAIL: pricing.md is HTML"
# llms.txt (if the plan chose to ship one) resolves
curl -s -o /dev/null -w "llms.txt HTTP %{http_code}\n" https://yoursite.com/llms.txt
```

## Schema Markup for AI

Structured data helps AI systems understand your content. Key schemas:

| Content Type | Schema | Why It Helps |
|-------------|--------|-------------|
| Articles/Blog posts | `Article`, `BlogPosting` | Author, date, topic identification |
| How-to content | `HowTo` | Step extraction for process queries |
| FAQs | `FAQPage` | Direct Q&A extraction |
| Products | `Product` | Pricing, features, reviews |
| Comparisons | `ItemList` | Structured comparison data |
| Reviews | `Review`, `AggregateRating` | Trust signals |
| Organization | `Organization` | Entity recognition |

Content with proper schema shows 30-40% higher AI visibility on non-Google AI engines. **Google's note**: structured data is "not required for generative AI search" but is recommended for overall SEO strategy.

**Rich-results dating (do not let a plan blur this):** Google retired FAQ rich results for every site on May 7, 2026, and HowTo rich results have been deprecated since Sept 2023. `FAQPage` and `HowTo` markup therefore earn **no Google SERP display** — their remaining value is extraction context for non-Google engines (Perplexity's FAQ-schema preference is documented in [references/platform-ranking-factors.md](references/platform-ranking-factors.md)). A plan may keep existing FAQPage/HowTo markup and may add FAQPage for non-Google engines — existing HowTo may stay; never add HowTo — but must never promise Google rich results from either.

## Agentic Experiences

Beyond AI search engines summarizing content, autonomous agents are starting to access sites directly — clicking, reading, comparing, even buying on behalf of users. Google's guide flags this as an emerging category to plan for.

**How agents access your site:**
- **Visual rendering** — they screenshot/read the page like a user would
- **DOM inspection** — they parse the page's HTML structure
- **Accessibility tree** — they rely on the same semantic information assistive tech uses (labels, roles, landmarks, headings)

**What to do:**
- **Render meaningful content without heavy JS gymnastics** — if the page is blank until 4 frameworks finish loading, agents see blank
- **Semantic HTML** — use `<main>`, `<nav>`, `<article>`, `<button>`, proper heading hierarchy, `alt` text on images
- **Clean accessibility tree** — every interactive element labelled; ARIA used correctly (or not at all when native HTML suffices)
- **Stable selectors / predictable layouts** — agents struggle with sites that re-render every interaction
- **Visible pricing, specs, contact info** — anything an agent would need to make a buying recommendation should be on a public, indexable page (this is where `/pricing.md` and similar files help)

**Emerging — Universal Commerce Protocol (UCP):**
Google references UCP as a forthcoming protocol that will give agents standardized hooks for commerce interactions (catalog discovery, pricing, checkout). Watch for adoption; for now, the structural recommendations above are the precursor.

For ecom and local business specifically, Google highlights:
- **Merchant Center feeds** + **Google Business Profile** for product/service visibility in AI Search
- **Business Agent** for conversational customer engagement (where applicable)

## Content Types That Get Cited Most

Not all content is equally citable. Prioritize these formats:

| Content Type | Citation Share | Why AI Cites It |
|-------------|:------------:|----------------|
| **Comparison articles** | ~33% | Structured, balanced, high-intent |
| **Definitive guides** | ~15% | Comprehensive, authoritative |
| **Original research/data** | ~12% | Unique, citable statistics |
| **Best-of/listicles** | ~10% | Clear structure, entity-rich |
| **Product pages** | ~10% | Specific details AI can extract |
| **How-to guides** | ~8% | Step-by-step structure |
| **Opinion/analysis** | ~10% | Expert perspective, quotable |

**Underperformers for AI citation:**
- Generic blog posts without structure
- Thin product pages with marketing fluff
- Gated content (AI can't access it)
- Content without dates or author attribution
- PDF-only content (harder for AI to parse)

**Citation ≠ recommendation.** Getting cited means your content was useful to consult; getting *recommended* — onto the buyer's actual shortlist — is governed by web-wide consensus (reviews, forums, analysts, press) and is largely independent of your own content. Self-promotional "best [category]" listicles can even backfire for emerging brands: in one 100-query B2B study, 69% of the AI Overview citations that self-promotional listicles earned came in answers that recommended competitors instead of the publishing brand. See [references/citations-vs-recommendations.md](references/citations-vs-recommendations.md) for the visibility ladder (retrieved → cited → mentioned → recommended), stage-dependent buyer's-guide strategy, what earns recommendations, and the attribution blind spot.

## AI SEO by Content Type

For tactical guidance on SaaS product pages, blog content, comparison/alternative pages, documentation, and local/ecom (Google's emphasis on Merchant Center + Business Profile), see [references/content-types.md](references/content-types.md).

## Monitoring AI Visibility

### What to Track

| Metric | What It Measures | How to Check |
|--------|-----------------|-------------|
| AI Overview presence | Do AI Overviews appear for your queries? | Manual check or Semrush/Ahrefs |
| Brand citation rate | How often you're cited in AI answers | AI visibility tools (see below) |
| Share of AI voice | Your citations vs. competitors | Peec AI, Otterly, ZipTie |
| Citation sentiment | How AI describes your brand | Manual review + monitoring tools |
| Recommendation rate | Whether you're on the shortlist, not just cited (see [references/citations-vs-recommendations.md](references/citations-vs-recommendations.md)) | Prompt tracking + mention framing |
| Source attribution | Which of your pages get cited | Track referral traffic from AI sources |

### AI Visibility Monitoring Tools

| Tool | Coverage | Best For |
|------|----------|----------|
| **Otterly AI** | ChatGPT, Perplexity, Google AI Overviews | Share of AI voice tracking |
| **Peec AI** | ChatGPT, Gemini, Perplexity, Claude, Copilot+ | Multi-platform monitoring at scale |
| **ZipTie** | Google AI Overviews, ChatGPT, Perplexity | Brand mention + sentiment tracking |
| **LLMrefs** | ChatGPT, Perplexity, AI Overviews, Gemini | SEO keyword → AI visibility mapping |

(Tool coverage rots fast — see What breaks first. Re-verify a tool's platform list before a plan commits to it.)

### DIY Monitoring (No Tools)

Monthly manual check:
1. Pick your top 20 queries
2. Run each through ChatGPT, Perplexity, and Google
3. Record: Are you cited? Who is? What page?
4. Log in `ai-seo-monitoring.md`, one dated row per query per month, shaped `| YYYY-MM | query | cited? (by whom) | page cited |` — the Verify below greps exactly this shape. Track month-over-month

### Search Console expectations

Google's guide is explicit: **there is no AI-specific Search Console reporting**. AI Overviews and AI Mode use core Search ranking, so the standard Search Console reports (Performance, Coverage, Core Web Vitals) are still what you measure with for Google. The third-party tools above are the only way to see cross-platform AI citation behavior.

### Verify

The monitoring log exists and actually accumulates dated entries (a plan that prescribed monitoring nobody does is theater):

```bash
test -f ai-seo-monitoring.md || echo "FAIL: no monitoring log"
entries=$(grep -Ec "^\| 20[0-9]{2}-[0-9]{2}" ai-seo-monitoring.md)
months=$(grep -Eo "^\| 20[0-9]{2}-[0-9]{2}" ai-seo-monitoring.md | sort -u | wc -l)
echo "dated rows=$entries distinct months=$months (months should grow by 1 per month since the plan shipped)"
```

## What NOT to Do

Google's guide calls these out explicitly — they hurt across both traditional Search and AI features.

1. **Write separate content "for AI"**. Same content should serve people and AI. Writing variants targeted at AI systems risks the **scaled content abuse spam policy** — Google's words.
2. **Chunk pages into AI-bait fragments**. Google's guide is direct: *"Don't break your content into tiny pieces for AI to better understand it."* Use normal paragraph + heading structure.
3. **Generate at scale for ranking manipulation**. AI-generated content is fine *if* it meets Search Essentials and spam policies. Mass-producing thin variations does not.
4. **Pursue inauthentic mentions**. Don't fabricate citations or bulk-spam Reddit/Wikipedia for AI visibility. Real participation only.
5. **Block AI crawlers if you want citation**. Blocking GPTBot, PerplexityBot, ClaudeBot means those engines cannot cite you. Google-Extended is the hedged case — whether blocking it affects AI Overviews inclusion is unverified (see the AI Bot Access Check). Block training-only crawlers (CCBot) if you must, not the search-and-cite ones.
6. **Hide your main content behind JS that doesn't render**. Both core Search and AI agents need to see your content; JS-only rendering loses both audiences.
7. **Skip E-E-A-T fundamentals**. Author identity, first-hand experience, expertise signals, transparent sourcing — Google's guide leans heavily on these for AI features.

## Common Mistakes

- **Ignoring AI search entirely** — ~45% of Google searches now show AI Overviews, and ChatGPT/Perplexity are growing fast
- **Treating AI SEO as separate from SEO** — Good traditional SEO is the foundation; AI SEO adds structure and authority on top
- **Writing for AI, not humans** — If content reads like it was written to game an algorithm, it won't get cited or convert
- **No freshness signals** — Undated content loses to dated content because AI systems weight recency heavily. Show when content was last updated
- **Gating all content** — AI can't access gated content. Keep your most authoritative content open
- **Ignoring third-party presence** — You may get more AI citations from a Wikipedia mention than from your own blog
- **No structured data** — Schema markup gives AI systems structured context about your content (mind the rich-results dating above)
- **Keyword stuffing** — Unlike traditional SEO where it's just ineffective, keyword stuffing actively reduces AI visibility by 10% (Princeton GEO study)
- **Hiding pricing behind "contact sales" or JS-rendered pages** — AI agents evaluating your product on behalf of buyers can't parse what they can't read. Add a `/pricing.md` file
- **Blocking AI bots** — If GPTBot, PerplexityBot, or ClaudeBot are blocked in robots.txt, those platforms can't cite you
- **Generic content without data** — "We're the best" won't get cited. "Our customers see 3x improvement in [metric]" will
- **Forgetting to monitor** — You can't improve what you don't measure. Check AI visibility monthly at minimum
- **Trusting a strategy document as an audit** — the mistake this derivative adds to the base's list: a plan is hypotheses until an executing skill fetches the site and fills the evidence in

## Tool Integrations

Wire these through whatever integrations your agent framework provides (the base's registry link pointed inside its own repository and is removed here):

| Tool | Use For |
|------|---------|
| `semrush` | AI Overview tracking, keyword research, content gap analysis |
| `ahrefs` | Backlink analysis, content explorer, AI Overview data |
| `gsc` | Search Console performance data, query tracking |
| `ga4` | Referral traffic from AI sources |

## Task-Specific Questions

1. What are your top 10-20 most important queries?
2. Have you checked if AI answers exist for those queries today?
3. Do you have structured data (schema markup) on your site?
4. What content types do you publish? (Blog, docs, comparisons, etc.)
5. Are competitors being cited by AI where you're not?
6. Do you have a Wikipedia page or presence on review sites?

## Related Skills

These names are the upstream marketingskills suite's identifiers — they are pairings by role, not links that resolve here:

- **seo-audit**: For traditional technical and on-page SEO audits — the upstream name for the *executing* counterpart Conditions requires before any live-site claim; in this bundle that role resolves to geo-technical, geo-audit, or claude-seo (see When NOT to use)
- **schema**: For implementing structured data that helps AI understand your content
- **content-strategy**: For planning what content to create
- **competitors**: For building comparison pages that get cited
- **programmatic-seo**: For building SEO pages at scale
- **copywriting**: For writing content that's both human-readable and AI-extractable

## Findings

**Defects fixed**
- The base reads like an audit but it asks questions and produces a plan; it runs nothing — and it never said so. Conditions now state the boundary as a hard condition (never use this document as evidence about a live site's current state), require pairing with an executing audit skill, and every Verify step in this document checks the produced artifacts (`ai-seo-plan.md`, `ai-seo-monitoring.md`, and post-implementation the shipped files) rather than pretending to check the site.
- Dead link removed: the base's Tool Integrations pointed at a registry path that resolves only inside the upstream repository.
- The vendored `references/platform-ranking-factors.md` predates the rich-results corrections and still sells FAQPage/HowTo schema as a Google AI Overviews lever; dated caveats now sit at both body link points to that file (the hash-pinned file itself is untouched). Independent-review finding, fixed in revision.

**Excised**
- The base's assertion that non-Google engines parse `llms.txt` when present — an unverified vendor-behavior claim, replaced with the dated editorial finding (2026-07-30: no vendor confirmation) and a downgraded, clearly-speculative recommendation.
- The base's unhedged claim that blocking Google-Extended removes you from Gemini and AI Overviews citation — same unverified-vendor-behavior class as the llms.txt claim, now hedged explicitly in the bot list and What NOT to Do. Independent-review finding, fixed in revision.
- The registry link above.

**Security review**
- No executable surface in the base or this derivative: no scripts shipped, no tools declared, no instructed calls to third-party services. External references are documentation URLs only. All Verify commands run against the operator's own artifacts or (post-implementation) the operator's own site.

**Grafts**
- None. The superseded fork contributed zero text (its body is a subset of an older cut of the keeper).

**Era corrections applied**
- Version stamp and fork-gap warning (2.2.0 vs the frozen 1.1.0 fork) written into Era — the wild listings carry no such warning.
- FAQ/HowTo rich-results retirement dates and the `llms.txt` confirmation status added where the base's schema and machine-readable-file advice needed dating.
- Provenance note: the one-line resolution "never sold to a client as a Google lever" is an addition sourced from the batch editorial (2026-07-30), not keeper text — see the delta ledger.

## Attribution

- **Base:** `coreyhaines31/marketingskills/ai-seo` (MIT), version 2.2.0, content hash at derivation `cb70d0b5daf4cfe3cad30ca897007347bb3dc150c9384497334dbd9122c0143c`. The workflow, tables, and reference files are substantially retained from this source and upgraded per the Findings above.
- **Superseded cluster member:** `b1rdmania/ghostclaw/ai-seo` (MIT), a fork frozen at 1.1.0, content hash at derivation `7ef9eac488baafde07c816f6c24c1b250995bef730882cc05e4dfe32978d93eb`. Contributed **zero text**; listed to record that the same-name cluster was adjudicated and resolved in favor of the 2.2.0 keeper.
- **Vendored files:** five reference documents from the base skill's directory (per-file origin, hash, and fetch date in the frontmatter `files` list), carried verbatim under the base repository's MIT license.
- **This derivative:** © SkillFed, released under the MIT license.
