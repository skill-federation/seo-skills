---
name: geo-plan
description: 'Build-time GEO and answer-engine planning, current to 2026: decide what content and site
  structure to create so AI search (ChatGPT, Perplexity, Google AI Overviews, Claude) cites you — applied
  before a live site exists to audit. Emits a build plan naming the engine each item targets and a skip
  list for what is dead or unproven. It plans only: it fetches, renders, scores and audits nothing.'
license: MIT
treatment: synthesized
synthesized_from:
- slug: ai-seo
  content_hash_at_synthesis: 72dad603e35b593139f298cff98d6a163a8dea8b378eb317902e337f316586fb
  references_drawn:
  - path: references/content-patterns.md
    sha256: 8adcfcc020a3529eda71f783e4893d3e39e8b0f503fd2fa126e8b75a80963824
  - path: references/platform-ranking-factors.md
    sha256: ca3fb8c09fec3445abe611bab2cd1b5f20751c5d51a3a5c63ecd2b85cd458ee8
  - path: references/citations-vs-recommendations.md
    sha256: 88016418b43b7e798dd950eb1240f76dec08c3408038f9a5d83005aff5a4daa3
  - path: references/content-types.md
    sha256: 9ad0a871f866efa307fc0d6fe2bd19d443a2276cb396afdd5b4d81fe9b4167e3
  - path: references/okf.md
    sha256: 4abcab5b8ee90b63c5d09c98387a8ec3cdb8f5df33e75d3b4b91eb817283bfd8
- slug: geo-technical
  content_hash_at_synthesis: 593c7843b77896a475690c2a7a35681b3e60b4562bdcaf74e2756034eb5b9d8f
- slug: ai-bot-log-audit
  content_hash_at_synthesis: 910261c827a36fc2f2c7ae72e2eeb2b188061baa10898af2cf25b54d048a1765
- slug: geo-audit
  content_hash_at_synthesis: c139a4456503b182c0c0834ff202a4f39f9f5e8612fa8283c214fd670debefe9
- slug: seo
  content_hash_at_synthesis: 58640da8597b6fd8ee88ed0f15a8cb0d8eca09a938e3a8134e0a9a67446aa5f3
  references_drawn:
  - path: references/json-ld-templates.md
    sha256: cf4e5e63156119a5a47db62209f554802bf427cf8027dbb43e8b032ddcfe3a5c
targeted_version: 2026 build-time GEO best practices (synthesized 2026-08-10)
last_verified_at: 2026-08-10
---

# GEO Build Plan — the upstream, build-time framework

Every other AI-search skill in this bundle starts from a site that already
exists: it fetches pages, reads logs, and grades what shipped. This one starts a
step earlier, from the question far more people ask — *how do I build content and
a site that AI search will cite in 2026, what is worth building, and what is
already dead?* It answers with a plan an operator can build against, and it
inspects nothing. The plan is the deliverable; the citation is the goal.

## Conditions

### When to use

- You are **building or planning** content, a page, or a whole site whose goal is
  to be cited by AI search — ChatGPT, Perplexity, Google AI Overviews, Claude,
  Gemini, Copilot — and there is not yet a live site to inspect.
- You need the 2026 reality settled before you commit effort: which bets pay off,
  which are cosmetic, and which will actively cost you.
- Triggers this skill answers: "how do I get cited by ChatGPT or Perplexity",
  "GEO strategy for a new site", "AI SEO checklist for 2026", "build content that
  AI search cites", "what schema and structure should this new page ship with",
  "how do I get cited on Perplexity vs Claude vs Google".
- You want a written build plan whose every item is scoped to the engine it
  targets and grounded in a dated fact, so a builder can execute it and a
  reviewer can check it.

### When NOT to use

- **To audit or diagnose a site that already exists.** That question needs
  evidence about *your specific* deployment, and this skill gathers none.
  **geo-plan plans what to build; it inspects and scores nothing.** Route the
  live-site work to the skill that fetches the evidence:
  - a full technical inspection of a deployed site → **geo-technical**;
  - a fast scored read on AI-crawler legibility → **geo-audit**;
  - what AI crawlers actually fetched, skipped, or errored on → **ai-bot-log-audit**
    (it reads your server access logs);
  - which tactics apply to *your* site given that evidence → **ai-seo**.
- **For the traditional and technical SEO build — site architecture, schema
  implementation, Core Web Vitals budgets, the crawlability foundation — that is
  the sibling build-time skill **seo-plan**.** geo-plan owns AI-search and citation
  strategy; seo-plan owns the traditional and technical build; the two are
  build-time siblings that overlap only where structured data serves citation. If
  you landed here to plan a whole new site and want the foundation, start with
  seo-plan and pair this one for the citation layer.
- **The seam with ai-seo, stated plainly.** ai-seo adjudicates which tactics fit
  one specific site given its evidence, and it is built to pair with an executing
  audit that fetches that site. geo-plan is the general, build-time framework you
  apply *before* a site exists to audit — no site, no evidence, no adjudication of
  a particular deployment. When you have a live site and want a per-site call, use
  ai-seo; when you are deciding what to build in the first place, use this.
- For writing the actual JSON-LD, robots rules, or render config once the plan
  says to — that implementation reference is **seo**.
- As proof of anything about a running site. A plan is a set of hypotheses about
  what to build; it becomes fact only after something is built and an executing
  skill measures it.

### Prerequisites

- **You are planning or building, not auditing** — that is the whole precondition.
  No live URL, no server, no access logs, and no crawler are required or used;
  bring the project's goals, target queries, and the content or product you intend
  to create.
- A place to write the plan artifact — this skill standardizes on
  `geo-build-plan.md` in the working directory (shape defined below).
- For the Verify blocks: a shell with `grep`, run against the plan file you
  produce. The Verify steps here check the *plan*, never a site.

### What breaks first

- **The dated facts.** Engine behavior, retired schema types, and unproven
  conventions rot faster than anything else here; the ## Era section pins their
  state as of this document's review date, and a plan built on a stale pin is a
  plan built on sand.
- **The engine roster and their retrieval behavior.** New crawlers appear, vendors
  swap retrieval backends, and citation shares move without notice — treat any
  per-engine claim as a snapshot to re-verify, not a constant. Which index each
  engine reads (below) is the fastest-rotting part of the per-engine guidance.
- **Vendor stances.** A published position quoted below can be superseded by newer
  guidance; when a newer dated statement from the vendor conflicts with a pin
  here, the newer statement wins and this document needs re-verification.

## Era

This framework targets AI-search and crawler behavior as of August 2026 (reviewed
2026-08-10). Each dated fact below is drawn from a verified bundle member and is
load-bearing: when one moves, the build advice resting on it moves with it. Read
this section before planning anything — it is the difference between building for
how AI search worked last year and how it works now.

- **The technical floor.** **AI crawlers do not execute JavaScript.** GPTBot,
  PerplexityBot, ClaudeBot and their peers fetch raw HTML and parse it; whatever a
  client-side framework paints after load is invisible to them no matter how good
  the copy is. This single fact promotes rendering strategy from a footnote to a
  first decision in any build plan.
- **Google's own stance.** In Google's words, **Google's generative AI features on Search are rooted in its core Search ranking and quality systems — nothing has to be added to a page for them.** No special markup, no AI-only files, no separate variant of the content. For Google's surfaces, the baseline is helpful, people-first, crawlable content — nothing *must* be added to rank. Structured data is still worth shipping even here — third-party analysis finds it aids AI-Overview inclusion, and the non-Google engines lean on it harder — but never as a *rich-result* play, since those are retired below.
- **Two schema types are dead for rich results.** **Google retired FAQ rich results for every site on 2026-05-07**, and **HowTo has been deprecated since Sept 2023.** FAQPage and HowTo markup therefore win no Google display; their only remaining value is as extraction context for non-Google engines. Never put either in a plan as a Google lever, and never add HowTo at all.
- **One convention is unproven.** **llms.txt is a proposed convention at roughly 0.015% adoption with no vendor confirmation.** No major AI system is confirmed to read it. It is cheap enough to be a speculative add for a content site, but it is never a load-bearing plan item and never a Google tactic.
- **The current performance metric.** **INP replaced FID in March 2024**, so page-experience budgets are set against Interaction to Next Paint, not the retired First Input Delay. Build to the live metric: a slow or unstable page weakens the crawlable foundation the rest of this plan rests on, and a plan still budgeting for FID is dated on its face.
- **A dated protocol to watch.** Google introduced the Open Knowledge Format on 2026-06-12 — **Google's v0.1 markdown spec for representing site content as an agent-readable bundle**, built for data-team catalog metadata, with no confirmed AI-search signal today. Plan it, if at all, as a speculative protocol-layer bet (see Machine-readable files for agents), never a load-bearing fix.

## The build plan artifact

Everything this skill decides is written to `geo-build-plan.md`, in the shape
below. The Verify blocks in later sections grep this file, so the shape carries
weight:

```markdown
# GEO Build Plan — [project]

## Citation model
- Target engines: [ChatGPT | Perplexity | Google AI Overviews | Claude | Gemini | Copilot]
- Ladder aim: [the rung each effort targets — cited / mentioned; recommendation is off-site]
- Citation-worthiness bets: [what will make this content worth citing]

## Build items
### B1. [what to build]
Engine-target: [the engine(s) this item earns citation on]
Applies-to: [the page or content type this builds — product page, blog post, docs, comparison, home]
Basis: [the dated 2026 fact or bundle source that justifies it]
Build-or-skip: build
[the concrete build instruction]

## Skip list
- [tactic] — Skip because: [why it is dead, cosmetic, or unproven in 2026]
```

Two rules make the artifact honest. Every build item carries an `Engine-target:`
line, because a tactic that does not name its engine is an adjudication skipped —
FAQ structure helps Perplexity and does nothing for Google display, and a plan
that blurs that is wrong. And every build item carries a `Basis:` line, because a
build instruction that cannot name the fact behind it is a guess wearing a plan's
clothes. The `Applies-to:` line keeps items concrete: an item that names no page
or content type is a floating tactic, not a build task.

### Verify

The plan has the three load-bearing sections before anything downstream reads it:

```bash
for s in "## Citation model" "## Build items" "## Skip list"; do
  grep -qF "$s" geo-build-plan.md || echo "FAIL: plan missing section: $s"
done
```

## Decide the citation model first

Before any tactic, settle what actually earns a citation, because the evidence is
lopsided and building against the wrong half wastes the whole effort. The strongest
signal in the research is authority you can point at: **the Princeton GEO study (KDD 2024) ranks citing sources at the top of its nine-method list at roughly +40% visibility, while keyword stuffing at the bottom actively costs roughly 10%.** So
the first build decisions are not about markup at all — they are about whether the
content carries named sources, specific numbers, dated claims, and attributable
expertise. Plan those in, and plan keyword-density thinking out; on these engines
it is the one move that moves the number backwards.

Because the next distinction decides where the rest of the effort should go, make
it precise. AI visibility is a ladder, not a yes-or-no, and each rung is won
differently:

- **Retrieved** — the engine read the page while composing an answer but did not
  cite it; governed by crawlability and parseable structure, and mostly invisible
  except as hints in server logs.
- **Cited** — the page appears as a named source in the answer; governed by how
  useful and extractable the content is: structure, sourced statistics, clarity,
  freshness. This is the rung a build plan moves directly.
- **Mentioned** — the brand is named in the answer text; governed by entity
  recognition and by how the wider web already talks about the brand.
- **Recommended** — the product lands on the shortlist the buyer actually
  considers; governed largely by aggregate web consensus (reviews, forums,
  analysts, press, video) and mostly independent of anything on the brand's own
  domain.

There is a shadow rung as well: on detailed, requirements-heavy queries the engines
increasingly name products to *avoid*, with sources, so weak third-party consensus
is no longer merely absence from the shortlist — it can be an explicit rule-out.

The build consequence is sharp. A build plan owns the cited rung outright and
influences mentioned; it cannot manufacture recommended, because that is earned
off-site. This is why a self-ranked "best [category]" guide is a double-edged
build: it reliably gets the page cited as a source *about the category*, but for an
emerging brand the engine tends to harvest the competitor names the guide compiled
and recommend those instead — the guide becomes research that helps rivals. Build
the genuinely useful guide when it serves the audience, but set the expectation
(citation and category framing, not near-term recommendation) and steer the
remaining effort to where recommendation is actually decided: real third-party
validation on the review platforms buyers check, presence in the communities they
read, and analyst and press coverage. The test to apply before building another
self-ranked guide is simple — if an engine ignored everything on your own domain,
would the rest of the web still put you on the shortlist? Where the answer is no,
that gap is the priority, and it is not a content-you-publish problem.

Record the target engines, the ladder rung each effort is aiming at, and the
citation-worthiness bets in the plan's `## Citation model` section, then let every
build item trace back to one of those bets.

### Verify

Every build item is scoped to an engine and grounded in a basis:

```bash
items=$(grep -c "^### B" geo-build-plan.md)
targets=$(grep -c "^Engine-target:" geo-build-plan.md)
bases=$(grep -c "^Basis:" geo-build-plan.md)
echo "build_items=$items engine_targets=$targets bases=$bases (must be equal and > 0)"
```

## Build for each engine's selection logic

The engines do not share a retrieval pipeline, and a plan that treats "AI search"
as one target leaves citations on the table. Three things are table stakes
everywhere — the page has to be in that engine's index, reachable by its crawler,
and extractable as self-contained passages — and beyond those, each engine weighs
different signals. Plan the build for the engines your audience actually uses, in
priority order, and tag every item with the engine it serves.

**Google AI Overviews** draw on Google's own index and inherit the traditional
ranking signals a site already has (or lacks) — backlinks, page authority, topical
relevance — with the AI layer adding a preference for cited sources and structured
data on top. Two build consequences follow. The overview does not simply re-list
the classic top ten, so a page that never reaches the first results page can still
be pulled in when it carries clean structured data and a direct, extractable
answer — structure is leverage even for lower-authority pages. And the queries that
trigger overviews most are the explainer and how-to shapes, so build the cluster of
pages that answers a topic together with its neighbouring questions rather than one
thin page per keyword. Named, sourced citations in the copy and real author
credentials are the extra signals the AI layer rewards. Gemini reads the same Google index (plus the Knowledge Graph), so it needs no separate plan — build for it exactly as for AI Overviews.

**ChatGPT** searches a Bing-based index and then cites what it leaned on, so being
in Bing's index — not only Google's — is the precondition many sites miss. Freshness
is a major differentiator here, so build a refresh cadence
into the plan for competitive topics instead of treating content as write-once. The
signal that matters most is fit: the closer a page's shape is to how ChatGPT would
itself phrase the answer — conversational, direct, cleanly headed — the likelier it
is to be the cited source. Off the domain, ChatGPT leans on third-party surfaces
such as Wikipedia, Reddit, and established press, so an accurate entity presence
there is part of the build, not an afterthought.

**Perplexity** always shows its sources and runs retrieved results through several
reranking passes, discarding whole sets that miss its quality bar, which makes it
the most research-oriented target. It rewards a handful of concrete build choices:
FAQ-structured Q&A, publicly reachable PDF resources (whitepapers and reports it
prioritises — un-gate the ones stuck behind a form), a real publishing cadence, and
atomic, self-contained paragraphs it can lift cleanly. It also leans on a curated
set of authoritative domains and evaluates fresh content quickly, so a newer
publisher with tight, well-sourced pages has a genuine shot at citation.

**Microsoft Copilot** rides entirely on Bing's index across Edge, Windows, and
Microsoft 365, so if Bing has not indexed a page, Copilot cannot cite it — submit
to Bing's webmaster tooling and use the IndexNow protocol to push new and updated
pages into Bing quickly. The Microsoft-ecosystem tie is a real build lever the
other engines do not offer: presence on LinkedIn and GitHub helps here
specifically. Copilot also weights page speed more sharply, so keep load times
tight, and write explicit, extractable entity definitions.

**Claude** differs at the root: **Claude uses Brave Search as its search backend when web search is enabled — not Google, not Bing**, so its ability to find and cite a
site is gated by that site's visibility in Brave — a separate index most SEO work
never touches. Claude also cites sparingly and rewards precision, so the build bet
is factual density (specific numbers, named sources, dated claims) over
general-purpose prose. Allow both the ClaudeBot and anthropic-ai user agents, and
confirm the key pages actually surface in Brave.

Where to start when the plan cannot do everything at once: put the effort where the
audience is. Google AI Overviews reach the widest audience and usually build on SEO
foundations already in place; ChatGPT is the most-used standalone tool for tech and
business readers; Perplexity pays off for research-leaning audiences; Copilot and
Claude come first only when the audience skews Microsoft-enterprise or
developer-and-analyst respectively. The fundamentals — extractable structure,
sourced claims, schema, crawler access — compound across all of them.

### Verify

Every Engine-target names a concrete engine, never a vague "AI":

```bash
grep "^Engine-target:" geo-build-plan.md \
  | grep -viE "google ai overviews|ai overviews|chatgpt|perplexity|copilot|claude|gemini|all-non-google" \
  && echo "FAIL: an Engine-target names no concrete engine"
```

## Structure content for machine extraction

AI systems pull passages, not whole pages, so the build target is a page that
reads cleanly in fragments. Two structural facts drive the plan. First, lead each
section with a self-contained direct answer — roughly forty to sixty words that
stand without the surrounding prose — because that is the unit a summarizer lifts.
Second, respect how these models read long inputs: **Place key claims, definitions, and statistics at the START and END of pages/sections**, since the
middle of a long passage gets the least attention. Tables and lists survive the
middle better than flowing prose, so structured comparisons and step lists can
live there; the load-bearing claims belong at the edges.

Beyond the shape of the page, there is a small catalogue of content *blocks* worth
building deliberately, each matched to a query shape an engine is answering. Treat
them as reusable units rather than reinventing structure per page:

- A **definition block** answers "what is X" — the term, a one-line definition,
  then a short expansion — and is the unit an overview lifts for explainer queries.
- A **step block** answers "how do I X" as a short numbered sequence with named
  steps, which extracts cleanly as a list.
- A **comparison table** answers "X vs Y" — criteria down the side, options across
  the top — because a table survives extraction where the same content in prose
  does not.
- A **pros-and-cons block** answers "is X worth it" and "should I X" evaluation
  queries with balanced, labelled trade-offs and a one-line verdict.
- An **FAQ block** collects the real questions a page's audience asks, each with a
  direct first-sentence answer. Build it for the non-Google engines that reward
  Q&A structure; per Era it earns no Google rich result.

For citation specifically, layer in the blocks that make a claim quotable and
trustworthy:

- A **statistic block** states the claim, attributes the number to a named source,
  and dates it — an unsourced number is a liability, a sourced-and-dated one is a
  citation magnet.
- An **expert-quote block** carries a named person, their title, and their
  organisation around the quote.
- A **self-contained answer block** is a single paragraph that still makes sense
  lifted out of the page entirely; the test is whether it reads correctly with
  everything around it deleted.
- An **evidence-sandwich block** opens with a claim, lists the supporting data with
  sources, and closes on the actionable takeaway.

One more content-shape decision cuts across all of these: cover the topical
cluster, not a single keyword. The engines generate related sub-queries and
synthesize across them, so a page that answers a parent question with its
neighbours covered is retrieved more often than a thin page targeting one exact
phrase. Plan for depth of coverage over keyword-per-page multiplication.

### Verify

The plan names concrete block patterns and records edge placement, not just "good
structure":

```bash
grep -qiE "definition block|step block|comparison table|answer block|self-contained|evidence sandwich|statistic block|pros-and-cons|faq block" geo-build-plan.md \
  || echo "MISSING: no concrete content-block pattern planned"
grep -qi "start and end" geo-build-plan.md \
  || echo "MISSING: edge-placement plan for extractable answers"
```

## Plan by content type

The build differs by what the page *is*. A short per-type checklist keeps the plan
concrete instead of generic:

- **SaaS product pages** aim to be cited for "what is [category]" and "best
  [category]" queries. Build a plain opening statement of what the product does and
  who it is for; a comparison framing it against the whole category, not only named
  rivals; quantified capability claims rather than adjectives; visible pricing (and
  a machine-readable pricing file, below, for agent buyers); and a buyer-question
  FAQ. Citation is the realistic goal — recommendation depends on the off-site
  consensus covered in the citation model.
- **Blog posts** aim to be cited as a topic authority. Build one target query per
  post with the heading matched to it, a definition in the opening for explainer
  queries, original data or research or named-expert quotes, a visible last-updated
  date, an author byline with real credentials, and internal links to the related
  product pages.
- **Comparison and alternative pages** target "X vs Y" and "best X alternatives".
  Build a structured comparison table with explicit criteria and scores, keep the
  treatment genuinely balanced (visibly biased comparisons are penalised), and keep
  pricing and feature data current.
- **Documentation and help content** target "how to X with your product". Build
  numbered step sequences, code samples where relevant, screenshots with
  descriptive alt text, and stated prerequisites and outcomes. Organise the steps
  with ordinary headings — do not reach for HowTo markup, which per Era earns
  nothing now.
- **Local and ecommerce** pages, where Google pulls from feeds and profiles: keep
  the Merchant Center feed accurate and current, complete the Google Business
  Profile (hours, services, photos, answered Q&A), keep reviews recent and
  responded-to, and add service-area schema.

### Verify

Build items name the page or content type they build, so none is a floating
tactic:

```bash
items=$(grep -c "^### B" geo-build-plan.md)
scoped=$(grep -c "^Applies-to:" geo-build-plan.md)
echo "build_items=$items scoped_to_page_or_type=$scoped (aim: every item carries an Applies-to)"
```

## Structured data to ship

Structured data gives the engines a clean, machine-readable copy of what a page
means, and the non-Google engines lean on it more reliably than they parse prose.
Plan these JSON-LD types, scoped to what they actually buy in 2026:

- **Organization** on the identity pages, with the logo and a `sameAs` list linking
  the brand's real profiles — this is how an engine tells your brand apart from
  every similarly named thing.
- **Article** (or **BlogPosting**) on content, carrying the author as a `Person`
  with their own `sameAs` links and credentials, the publisher, and both published
  and modified dates — the authorship and freshness signals the engines weigh.
- **Product** on product pages, with `offers` (price, currency, availability) and
  `aggregateRating`, so the agent-buyer surfaces have real numbers to compare.
- **FAQPage** on Q&A content, for the non-Google engines only. It parses as
  structure and Perplexity in particular rewards it, but per Era it earns no Google
  rich result, so never file it as a Google lever.

Two build rules bind all of them. The schema must match the visible content exactly
— markup claiming what the page does not show is a liability, not a signal — and
every dated or numeric value in the schema should be one the page itself states.
Writing the actual JSON-LD blocks is the implementation reference **seo**'s job;
this plan only decides which types to ship and why.

### Verify

No schema item promises a retired Google rich result, and the citation-relevant
types are actually planned:

```bash
grep -niE "(faqpage|howto)[^\n]{0,40}google[^\n]{0,30}rich result" geo-build-plan.md \
  && echo "FAIL: a retired schema type is sold as a Google rich-result lever"
grep -qiE "organization|article|blogposting|product|faqpage" geo-build-plan.md \
  || echo "MISSING: no structured-data build items"
```

## Build the technical foundation

Content quality is wasted if a crawler cannot read the page, so the plan needs an
infrastructure layer under the content layer. The non-negotiable item follows
directly from the era fact that AI crawlers parse raw HTML only: **the primary
content, headings, links, and structured data must be present in the server-sent
HTML**, via server-side rendering, static generation, or prerendering. A page that
is blank until JavaScript runs is, to every AI crawler and to a deprioritized
corner of Googlebot's rendering queue, an empty page. This is usually the single
highest-leverage item in a build plan for a JavaScript-framework site.

The second foundation item is access: name the crawlers you intend to allow so a
default-deny robots.txt or a WAF does not silently remove you from the engines you
are building for. Allowing GPTBot, PerplexityBot, ClaudeBot, and the anthropic-ai
agent is what keeps those engines able to cite you at all; blocking a
search-and-cite bot is a decision to be invisible on that engine. Google-Extended
is the hedged case — it is Google's AI opt-out control, and whether blocking it
affects AI Overviews inclusion is not something this framework can assert; blocking
Googlebot is what verifiably removes a site from Google's surfaces.

The third foundation item is discovery, and the same no-JS fact from Era decides it,
not just the body copy. Internal links have to resolve as real `href` values in the
server-sent HTML — a menu built from `<div onclick>` handlers is a dead end to a
crawler that never runs the handler, so whole sections of a JavaScript app go
undiscovered even when the pages render fine in a browser. Give those links anchor
text that names the destination rather than "click here" or "learn more"; a crawler
weighing anchor text gets nothing from the generic version. Ship an XML sitemap and
reference it from robots.txt so freshly built pages are found without a deep crawl,
and give every page a self-referencing canonical so duplicate surfaces (www vs bare,
trailing-slash, query variants) do not split the authority an engine would otherwise
attribute to one URL. Because ChatGPT and Copilot both read Bing's index, wiring the
IndexNow protocol so new and changed pages reach Bing fast is one move that buys
faster AI visibility on two engines at once. These are the discovery bets a fast
legibility check scores next — plan them as crawler-scoped build items, so the site
ships ready to pass that check rather than failing it and backfilling later.

### Verify

The plan records a rendering strategy and an explicit crawler-access decision:

```bash
grep -qiE "server-side|prerender|static (html|render|generation)|SSR|SSG" geo-build-plan.md \
  || echo "MISSING: no rendering strategy in the plan"
grep -qiE "gptbot|perplexitybot|claudebot|anthropic-ai|robots\.txt" geo-build-plan.md \
  || echo "MISSING: AI-crawler access not planned"
```

## Machine-readable files for agents

A growing share of the audience is not a human reader but an agent acting for one —
comparing products, pulling prices, answering on a user's behalf — and a few plain
files make a site legible to them. None is a confirmed ranking signal, so plan them
as cheap, clearly-scoped bets, never load-bearing fixes.

- **A structured pricing file** (`/pricing.md`) hands an agent your plans as
  parseable text instead of a JavaScript-rendered pricing page it may not read. If
  pricing hides behind "contact sales" or a rendered widget, agents comparing
  options skip you; a plain markdown file with tiers, prices, and limits is
  trivially parseable. Build it for the agent-buyer surfaces.
- **An llms.txt index** points an agent at the handful of pages you most want read.
  Per Era it is unproven and unconfirmed, so it stays a five-minute speculative add,
  never a load-bearing item.
- **An OKF bundle** goes further. In June 2026 Google published the Open Knowledge
  Format (see Era) — a directory of cross-linked markdown files, each a concept with
  light frontmatter, served at `/okf/`. Google built it for data teams sharing
  catalog metadata; pointing it at a marketing site is a clever repurposing, not its
  primary use. Nothing crawls the web for OKF bundles today and no engine has
  announced reading them, so treat it as protocol-layer registration — the same
  shape of bet early schema.org adoption was, which took most of a decade to pay
  off. One benefit lands immediately regardless: generating the bundle graphs your
  pages and their links, so orphans and islands show up at a glance.

These files stack rather than compete — the sitemap says which URLs exist,
robots.txt permits the crawlers, llms.txt signposts the priority pages, the pricing
file hands over the numbers, the OKF bundle hands over the content as linked
concepts, and schema marks up each page. Build the ones that fit the platform (a
closed site builder that will not serve custom paths cannot host an OKF bundle at
all), and skip the bundle entirely on sites under about ten pages or where nobody
will budget the quarterly refresh.

### Verify

Unproven machine-readable files are filed as speculative, never as load-bearing
build items:

```bash
grep -nE "^### B" geo-build-plan.md | grep -iE "llms\.txt|okf|open knowledge format" \
  && echo "FAIL: an unproven machine-readable file is planned as a load-bearing build item"
```

## What to skip and what is dead in 2026

A build plan is as much about what you refuse to build as what you ship, and 2026
has a clear dead list. Do not build a separate, AI-targeted variant of your
content: beyond wasting effort, **producing an AI-targeted variant of your content falls under Google's scaled-content spam policy** — the same content should serve
people and machines, organized with ordinary headings, never chopped into
AI-bait fragments. Do not add HowTo markup, and do not add FAQPage expecting a
Google rich result; both lost that channel (HowTo in 2023, FAQ in 2026). Do not
lean on keyword density — the citation-model evidence says it actively costs
visibility on the AI engines.

Treat the machine-readable conventions as footnotes rather than fixes. An llms.txt
file is a five-minute speculative add for a content site and it cannot hurt, and an
OKF bundle is a protocol-layer bet with no confirmed consumer yet — but neither
earns a place among the load-bearing recommendations, and a plan that files either
as a real fix is misreading the evidence. Anything on this list that appears in the
plan at all belongs under `## Skip list` with the reason attached, never among the
build items.

### Verify

Dead and unproven tactics are quarantined to the skip list, never planned as
build items:

```bash
grep -nE "^### B" geo-build-plan.md | grep -iE "llms\.txt|faqpage|howto|open knowledge format" \
  && echo "FAIL: a dead or unproven tactic is planned as a build item"
grep -A20 "## Skip list" geo-build-plan.md | grep -qiE "llms\.txt|faqpage|howto|keyword stuff" \
  || echo "MISSING: skip list should record the 2026 dead/unproven tactics"
```

## Hand off to verification

This framework ends where a live site begins. Its one *parallel* companion runs
before then, not after: pair this citation plan with **seo-plan** for the
traditional and technical foundation (architecture, rendering, per-page schema,
Core Web Vitals) it assumes is in place. Once the plan is built and deployed, the
plan's hypotheses become checkable facts — and checking them is a different skill's
job, not this one's. Send the built site forward:

- To confirm the rendering and crawler-access items actually landed on the
  deployed site, run a full technical inspection with **geo-technical**, or a fast
  scored legibility read with **geo-audit**.
- To learn what AI crawlers really did with the new pages once traffic accrues —
  what they fetched, skipped, or errored on — read the server access logs with
  **ai-bot-log-audit**.
- To adjudicate which of the planned tactics actually fit the finished site given
  that evidence, and to keep the ongoing monitoring cadence, use **ai-seo**.
- To implement the concrete markup, robots, and render config the plan called for,
  use **seo**.

The rule that keeps this skill in its lane also keeps the bundle honest: plan here,
build, then verify there. A claim about a running site never originates in this
document.

## Attribution

Synthesized by SkillFed from the seo-skills bundle members ai-seo, geo-technical,
ai-bot-log-audit, geo-audit, and seo (all MIT, minibatch 940, verified 2026-08-10),
drawing on both their SKILL.md bodies and the reference files pinned in
`synthesized_from.references_drawn` (ai-seo's content-patterns, platform-ranking-factors,
citations-vs-recommendations, content-types, and okf; seo's json-ld-templates).
Every fact traces to one of those verified sources; the prose is original, written
for this document. Published by SkillFed under the MIT license.
