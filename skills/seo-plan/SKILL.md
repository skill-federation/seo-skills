---
name: seo-plan
description: 'Build-time SEO planning for 2026: turns a new site or product into a written build plan
  — architecture, server-rendering, semantics, per-page schema, Core Web Vitals budgets, E-E-A-T, content
  structure — before any live URL exists. Use it to structure a site for search from the start, not audit
  a running one. Encodes the 2026 baseline (FAQ retired, HowTo dead, INP not FID, crawlers that skip JavaScript)
  and verifies the plan it writes. Pair with geo-plan for AI-search citation.'
license: MIT
treatment: synthesized
synthesized_from:
- slug: seo
  content_hash_at_synthesis: 58640da8597b6fd8ee88ed0f15a8cb0d8eca09a938e3a8134e0a9a67446aa5f3
  references_drawn:
  - path: references/json-ld-templates.md
    sha256: cf4e5e63156119a5a47db62209f554802bf427cf8027dbb43e8b032ddcfe3a5c
- slug: geo-technical
  content_hash_at_synthesis: 593c7843b77896a475690c2a7a35681b3e60b4562bdcaf74e2756034eb5b9d8f
- slug: seo-validate
  content_hash_at_synthesis: 4b9c5ae865ae1788de7b444c9e7e4f3ce62f8d582d5469655b2b8be94a3a924f
  references_drawn:
  - path: reference/spa-ssg-patterns.md
    sha256: 8271f0c3fcb9e52eb368f28b74e9975ba28d1f0fb8d9a72881eb62ad85962eb6
  - path: reference/core-web-vitals.md
    sha256: 3a5db2c3519899098ba85f44f67de0371e57f8d46300cec0dd92203ab36bdcf1
  - path: reference/w3c-guidelines.md
    sha256: ec5dd3b7356bd80129fbb62592914b2d448c0b84549b7c995388ee85ce1158cb
- slug: claude-seo
  content_hash_at_synthesis: 6c6aa917b552011339589f43df9c082ddde2ded75e3a17e3f5492ab96590704d
  references_drawn:
  - path: references/eeat-framework.md
    sha256: 6550ca35ca94180686c32e907baf3bb544832cc3c612a7df0b0afef0d0e279be
  - path: references/schema-types.md
    sha256: b829bb44b17bc32032a1036c925ecd0a172a6f1ea23c6c00edd1893fbc2b19cf
  - path: references/cwv-thresholds.md
    sha256: 0144772e781f532eb1263c2bacd15940f429de704ac123f60c6714bcac4a9816
  - path: references/quality-gates.md
    sha256: 5dec0bf50a443546cf4f222259cdcdfe2a891fcf97dd2278df59264c7738d36f
- slug: ai-seo
  content_hash_at_synthesis: 72dad603e35b593139f298cff98d6a163a8dea8b378eb317902e337f316586fb
last_verified_at: 2026-08-10
---

# seo-plan — build-time technical and content SEO plan (2026)

An authored, build-time planning skill. Given a site or product that does not exist yet — or a rebuild before launch — it produces one written artifact: a comprehensive SEO build plan covering information architecture, a rendering decision, HTML semantics and accessibility, the technical foundation, a per-page-type structured-data mapping, performance budgets, an E-E-A-T and trust layer, and content structure, each aimed at the 2026 search reality. It writes a plan and checks that plan against itself. It fetches nothing, scores nothing, and edits nothing.

## Conditions

### When to use

- You are designing a site's SEO foundation before there is a deployed URL to inspect: choosing the URL scheme and hierarchy, deciding what renders on the server, mapping page types to schema, setting performance budgets, and settling the semantics, trust, and content rules that ship correctly the first time rather than being retrofitted after an audit finds them missing.
- Triggers: "SEO plan for a new site", "how should I structure this site for SEO", "technical SEO checklist 2026", "site architecture for SEO", "what schema should each page type carry", "what Core Web Vitals budget should we build to", "how do I set up E-E-A-T from the start".
- You want the plan itself to be checkable — a document where every page type has a rendering mode, a schema mapping, and a performance budget stated, so a reviewer (or a later audit) can hold the build to it.

### When NOT to use

This skill plans what to build; it inspects and scores nothing. Route elsewhere when:

- There is already a live site to diagnose. For a scored, evidence-backed inspection of a deployed site, use geo-technical (the full eight-category live check) or geo-audit (the fast scored verdict); for a repository pre-ship validation, use seo-validate; for what AI crawlers actually did over time in server logs, use ai-bot-log-audit. seo-plan reads no site and emits no score.
- You need one tactic adjudicated against a specific site's evidence. ai-seo interviews a real site and pairs with an executing auditor to decide, per engine, which tactics that site should adopt. seo-plan is the general build-time framework that applies before a site exists, so there is no evidence to adjudicate against yet.
- The goal is AI-search / generative-engine citation — getting cited by ChatGPT, Perplexity, or Google AI Overviews. That is the job of the sibling skill geo-plan. seo-plan owns the traditional and technical SEO build (architecture, rendering, semantics, schema implementation, Core Web Vitals, crawlability, E-E-A-T); geo-plan owns AI-search citation strategy. The two meet only at structured data: seo-plan decides HOW each page type implements schema; geo-plan decides what to do with it for citation.

### Prerequisites

- You are planning or building, not auditing: no live site, no URL, and no server logs are required or used. What the plan needs is the product's intended page types (home, category or listing, detail, article, and any location or landing pages), the framework or stack under consideration, and the target markets and languages.
- A place to write the plan. This skill standardizes on a single artifact, `seo-plan.md`, in the working directory; every Verify block below greps that file.
- No credentials, no network access, no toolchain install. The only tool the Verify steps use is a shell with grep run against the plan you wrote.

### What breaks first

- The dated facts in ## Era. Schema-type status, the interactivity metric, the Quality Rater Guidelines edition, and emerging conventions rot faster than anything structural here; if you are reading this long after the last-verified date, re-check those pins before trusting the schema, performance, and E-E-A-T sections.
- Framework rendering defaults. "Which routes render on the server" turns on framework versions whose defaults change between majors; the plan states a rendering mode per page type precisely because the default is not stable.
- Invented metrics and levers. A raw model will confidently cite a "Core Web Vitals 2.0", a "Visual Stability Index", or a rich-result type that Google has retired; the plan pins the real set and refuses the rest. Anything phrased as a Google ranking promise is the softer claim, and is flagged as such where it appears.

## Era

This skill plans against the search reality of 2026 (authored and last verified 2026-08-10). Seven dated facts shape what the plan may and may not recommend. Each is a fact the SkillFed SEO bundle already verified — in a member's body or one of its pinned reference files — restated here in build terms.

- Google retired FAQ rich results for every site on 2026-05-07. A build plan may still specify valid FAQPage markup where a page genuinely answers questions, but it must never justify that markup as a Google rich-result play — there is no such result left to win, and the retirement superseded even the earlier government-and-health carve-out.
- HowTo rich results have been deprecated since September 2023. The plan never recommends adding HowTo markup for Google benefit; step-by-step content is organized with ordinary headings and ordered lists instead.
- AI crawlers do not execute JavaScript. Any content that must be crawled and indexed has to exist in the server response, which is why the rendering decision is the second thing this plan settles, not an afterthought late in the build.
- Google crawls ALL sites exclusively with mobile Googlebot. The mobile layout is the canonical layout the plan designs for; a desktop-only experience is planned as though it does not exist for search, and mobile content parity is a build requirement rather than a nice-to-have.
- INP replaced FID as the interactivity metric on March 12, 2024. The performance budgets below are written against INP; the retired FID is never a build target.
- llms.txt is a proposed convention at roughly 0.015% adoption with no vendor confirmation. If the plan chooses to ship one it is recorded as a cheap, speculative add — never load-bearing in the build, and never a ranking or citation lever.
- E-E-A-T evaluation follows the September 11, 2025 Quality Rater Guidelines update. The trust layer below is built to that edition, which puts Trustworthiness at the centre of the family and widens the highest-bar YMYL set to include elections and democratic processes.

## The plan artifact

Everything this skill produces goes into `seo-plan.md`. The Verify blocks grep it, so its shape is load-bearing:

```markdown
# SEO Build Plan — [site]

## Architecture
- route: /            type: home      depth: 0  render: ssg  words: 500
- route: /c/[slug]    type: category  depth: 1  render: ssr  schema: none  words: 400
- route: /p/[slug]    type: detail    depth: 2  render: ssr  schema: Product words: 400
- route: /blog/[slug] type: article   depth: 2  render: ssg  schema: Article words: 1500

## Rendering
- default render mode + per-type exceptions, each naming the framework mechanism that produces it

## Semantics
- doctype, lang, charset, one-h1 + heading order, landmark set per template

## Technical foundation
- canonical policy, param + facet + SRP + pagination handling, robots + sitemap, security headers, mobile viewport, hreflang (if multi-market), OG/Twitter cards

## Schema
- one row per page type -> schema type + required properties (or none)

## Performance
- LCP / INP / CLS budgets + TTFB and per-template asset-weight ceilings

## E-E-A-T
- authorship, trust signals, freshness policy, scaled-content boundary

## Content
- title / description / heading rules; answer-first lead; internal-linking model; per-type word floor
```

Two rules for the artifact. Every page type gets an Architecture row with a `render:` mode and, where it carries structured data, a `schema:` type. And every line is a build instruction — something you can implement — not a diagnosis of an existing page.

## Site architecture and crawl design

Settle the URL space and link graph before any page is built — they are the hardest things to change once URLs are indexed. Fix one canonical URL shape (lowercase, hyphenated, HTTPS, no session or tracking parameters in the indexed form) and let the path mirror the site's real hierarchy, so the structure is legible from the URL alone and every page a crawler should reach sits within about three clicks of the home page — depth beyond that earns little crawl budget.

Decide the discovery surface up front: one XML sitemap (or a sitemap index for large sites) listing only canonical, indexable URLs, referenced from `robots.txt`, which itself must leave the rendering resources crawlable. Plan the internal-linking model as part of the graph — a blog post of any length wants five to ten contextual internal links, a service page three to five, a category page a link to each child, and no page is left an orphan that nothing links to. Anchor text is descriptive and varied rather than a repeated exact-match keyword. Utility and thin routes (internal search results, faceted filter combinations, print variants) are marked for `noindex` or canonicalized to their clean base at design time, and you pick exactly one of those two treatments per pattern rather than mixing them.

Set a page-type budget the same way, because scale is where architecture turns into a penalty. Give each page type a minimum substance the template guarantees — on the order of a 500-word home page, 400 on a category or product page, 800 on a service page, 1,500 on an article — and treat programmatic expansion as a guarded decision, not a default. Near-duplicate location pages are the classic trap: plan a warning at thirty of them (each carrying at least 60% unique local substance) and a hard stop at fifty, past which the build proceeds only on a recorded justification, because Google's doorway-page systems demote thin location pages whose only difference is a swapped city name. Integration, glossary, and genuine product pages are safe to generate at scale; "city-swapped" location pages and thin "best-X-for-Y" pages are not.

### Verify

```bash
# every route row declares a crawl depth, and no important route sits deeper than 3 clicks
grep -nE "route:.*depth:\s*[0-9]+" seo-plan.md
grep -nE "depth:\s*[4-9]" seo-plan.md && echo "REVIEW: route planned deeper than 3 clicks from home"

# planned slugs are lowercase and hyphenated (flag underscores or uppercase in a route)
grep -nE "route:\s*\S*[_A-Z]" seo-plan.md && echo "REVIEW: non-canonical slug shape in the plan"

# the plan commits to a sitemap, and to a location-page guardrail if it plans many
grep -qi "sitemap" seo-plan.md || echo "FAIL: no sitemap plan"
grep -qiE "location|doorway|30\+|50\+" seo-plan.md || echo "NOTE: confirm no programmatic page-type needs a scale guardrail"
```

## Rendering strategy

Because AI crawlers do not execute JavaScript, and because Google crawls ALL sites exclusively with mobile Googlebot, the rendering decision is a first-class part of the build rather than a framework default you inherit by accident. For every route that must be crawled and indexed, the meaningful body text, the headings, the metadata (title, description, canonical), the internal links, and any JSON-LD must be present in the initial server response — not injected after a client framework hydrates. A page whose content only appears once JavaScript runs is, to a non-executing crawler, an empty page. The same server-render decision is also what makes a page legible to AI search engines at all; turning that legibility into citations — and which engines it matters for — is geo-plan's job, not this plan's.

Decide the mode by asking one question per route type: does the server return meaningful HTML before the client takes over? If it renders at request time that is server-side rendering; at build time, static generation; cached and revalidated on an interval, incremental static regeneration. All three are safe for search. Only client-side rendering, where the server returns a shell and the browser paints the page, is a crawlability risk, and it is reserved for authenticated or app surfaces that are deliberately kept out of the index. Even the crawler that does run JavaScript defers it into a separate rendering pass that can lag discovery by days, so "Googlebot will eventually see it" is not a plan.

Name the mechanism per framework so the build is unambiguous rather than aspirational. Next.js App Router routes are static by default, opt into request-time rendering or timed revalidation explicitly, and turn client-only the moment a hero is wrapped in a `ssr: false` dynamic import — which blocks the largest paint as well as the crawl. Nuxt renders on the server unless a config flag switches it to SPA mode; Astro ships static HTML with interactive islands and only goes client-only where a component is marked to render on the client alone; SvelteKit and Remix render on the server per route by default; Angular is client-only until its server package is added, and a plain Vite-React, Vue, or Create React App SPA is client-only until a prerender step or an SSR framework is introduced. Two build-time traps close the gap either way: hash-based routes are treated as fragments and never indexed as separate URLs, so public routes use real history paths; and metadata set only at runtime is invisible to the first response, so titles, descriptions, canonicals, and Open Graph tags are produced in the server render, not written by client script. Where a rebuild onto a server-rendering framework is not feasible, a build-time prerender step over the known routes is the fallback for static content, while legacy request-sniffing dynamic-rendering middleware is a last resort, not a target.

One rule follows straight from mobile-only crawling and belongs in the render spec: the mobile version is the version Google sees, so it must carry the equivalent primary content, structured data, and metadata as any wider layout. Content that only exists on desktop, or that hides behind a mobile interaction a crawler will not trigger, is content the index does not have. Plan parity as a build constraint on every template rather than discovering the gap in an audit.

### Verify

```bash
# a rendering mode is declared, and it is server-side for anything crawlable and indexable
grep -qiE "render:\s*(ssr|ssg|static|isr|prerender)" seo-plan.md || echo "FAIL: no server rendering mode declared"

# a crawlable route planned as client-only contradicts the Era facts above
grep -nEi "render:\s*(csr|client)" seo-plan.md && echo "REVIEW: crawlable route planned client-only - its initial HTML would be empty to a non-JS crawler"

# public routing is history-based, and metadata is planned into the server render
grep -niE "hashrouter|createwebhashhistory|/#/" seo-plan.md && echo "REVIEW: hash routing on a public route is not indexed as a URL"
```

## HTML semantics and accessibility

Specify the document skeleton every template emits, because the same semantics that assistive technology relies on are what crawlers and machine parsers read. Each page opens with the HTML5 doctype (its absence drops older browsers into quirks mode) and an `<html>` element carrying a `lang` attribute as a valid BCP 47 tag — `en`, `en-US`, `pt-BR`, `zh-Hant`, never an underscore form like `en_US` and never a bare word like `english`. A `<meta charset="utf-8">` is the first thing in the head, inside the first kilobyte, and the responsive viewport meta is mandatory since the mobile render is the one Google indexes.

Fix the outline as a template rule rather than a per-author choice: exactly one `h1` naming the page's subject, heading levels that descend without skipping (an `h1` followed by an `h3` breaks the outline for both screen readers and crawlers), and levels chosen for meaning with CSS doing the visual sizing. Give every template the landmark set — a `header`, a primary `nav`, exactly one `main`, and a `footer`, with `article` and `section` where they carry an accessible name — instead of a wall of `div`s, because semantic containers are what let a parser separate the primary content from the chrome. Fold the accessibility rules that double as ranking hygiene into the same spec: descriptive `alt` on every non-decorative image and an empty `alt` on the decorative ones, a real label on every form control, an accessible name on icon-only controls, and genuine `button`/`a` elements for anything interactive rather than a click handler bolted to a `div`. This layer is the substrate the schema and content layers sit on; get it wrong and the richest structured data still describes a page a crawler cannot parse.

### Verify

```bash
# the semantics section commits to the load-bearing skeleton rules
grep -qiE "doctype" seo-plan.md || echo "FAIL: no doctype rule"
grep -qiE "lang" seo-plan.md && grep -qiE "charset|utf-8" seo-plan.md || echo "FAIL: lang/charset rules missing"
grep -qiE "one h1|single h1|exactly one .?h1" seo-plan.md || echo "FAIL: no single-h1 rule"
grep -qiE "landmark|<main>|<nav>|<header>|<footer>" seo-plan.md || echo "FAIL: no landmark plan"
```

## Technical foundation

With architecture, rendering, and semantics fixed, specify the plumbing that keeps the built pages indexable, de-duplicated, and trustworthy. Canonical policy first: a self-referential, absolute canonical on every indexable page, one host-and-scheme chosen as authoritative with the alternates 301-redirected to it. Since Google retired the Search Console parameter tool in April 2022, the only remaining duplicate-control signals are the canonical tag, `robots.txt`, and the `robots` meta, so the plan spells out each parameter class: tracking parameters (`utm_*`, `gclid`, `fbclid`, `ref`) canonicalize to the clean URL; a faceted listing canonicalizes to its clean base when the facet is only a re-sort or a filter view, but a facet that is genuinely a distinct listing is its own canonical; an internal search-results page is kept out of the index (Google's guidelines name these explicitly) by exactly one of `noindex, follow` or a `robots.txt` disallow — picking both is self-defeating, since blocking the crawl means the `noindex` line is never fetched to be obeyed; and paginated pages each self-canonicalize, with `rel="prev"`/`rel="next"` planned as valid markup for the engines that still read it but never as a Google signal, which it stopped being in 2019.

Layer the rest of the plumbing on top. State the `robots.txt` intent, including a deliberate per-bot decision for AI crawlers — a `Disallow` removes you from that bot's results, so it is a choice made on purpose, and its citation consequences belong to geo-plan. Set a security-headers baseline as a trust and robustness signal (HSTS, `X-Content-Type-Options: nosniff`, a frame policy, a referrer policy, a content-security policy). For a multi-market site, plan `hreflang` as a fully reciprocal set — if page A points to page B, page B must point back or Google ignores the pair — with a self-reference and an `x-default` fallback, valid BCP 47 tags, and the region gotchas designed out (British English is `en-GB`; `uk` is Ukrainian, not the United Kingdom). Finally, plan the social-card metadata the same crawlers of record consume: Open Graph `og:title`/`og:description`/`og:image`/`og:url`/`og:type` with an absolute image URL around 1200×630, and a Twitter card tag that falls back to the Open Graph values.

### Verify

```bash
grep -qi "canonical" seo-plan.md || echo "FAIL: no canonical policy in the plan"
grep -qiE "utm_|tracking|facet|search result|srp|pagination" seo-plan.md || echo "FAIL: no parameter/facet/SRP handling"
grep -qi "viewport" seo-plan.md || echo "FAIL: no mobile viewport decision"
grep -qiE "hreflang|x-default" seo-plan.md || echo "NOTE: no hreflang plan - confirm the site is single-market"
grep -qiE "og:image|open graph|twitter:card" seo-plan.md || echo "NOTE: no social-card plan"
```

## Schema plan

Map each page type to one primary schema.org type and list the properties that type requires, all as JSON-LD (Google recommends JSON-LD over Microdata and RDFa), so the build ships correct structured data instead of guessing at it. A workable default mapping: `Organization` on the brand and home surface (name, url, logo, contactPoint, and `sameAs` profiles); `WebSite` at the site level (a `SearchAction` is machine-readable only and no longer earns a Google sitelinks search box); `Article`, `BlogPosting`, or `NewsArticle` on editorial pages (headline, author, datePublished, dateModified, image, publisher); `Product` with a nested `Offer` on detail pages (name, image, offers with price, priceCurrency, and availability — plus `aggregateRating` only where the ratings are real); `BreadcrumbList` on hierarchical routes; `LocalBusiness` with address, telephone, and opening hours on location pages; and `Person` or `ProfilePage` on author pages, which is also where the E-E-A-T layer plugs into the markup. Across every type, hold the invariants: `@context` is `https://schema.org`, `@type` values are case-sensitive, dates are ISO 8601, URLs are absolute, no placeholder text survives into production, the markup mirrors what is visible on the page, and ratings are never fabricated. In the plan, every page type maps to a schema type or is explicitly marked none, and candidate markup is validated against validator.schema.org before it ships. For writing the actual JSON-LD — and the robots, canonical, and render config the rest of the plan calls for — hand off to the implementation reference seo.

Match the type menu to the site's archetype so the mapping is specific rather than generic. A SaaS product uses `SoftwareApplication`, or `WebApplication` for a browser-based app (name, applicationCategory, an operatingSystem or browserRequirements, offers, featureList); a service business uses `Service` (name, provider, areaServed, offers); a store carries `Product` with `Offer` and can now declare shipping and return policies at the organization level rather than only per product; an events site uses `Event` (name, startDate, endDate, location, organizer); a publisher leans on `Article` or `NewsArticle` with `Person` authorship and `BreadcrumbList`; a media library uses `VideoObject` or `ImageObject`; a careers section uses `JobPosting`; and a course provider uses `Course`. Prefer the most specific subtype a page fits — a `Restaurant` over a bare `LocalBusiness`, a `BlogPosting` over a bare `Article` — because the narrower type carries the stronger signal. Newer additions worth planning for where they apply include `ProductGroup` for variant catalogues and `ProfilePage` for author hubs, both of which reinforce the E-E-A-T layer below.

The retirement and deprecation status is the part a stale model gets wrong, so the plan pins it. FAQPage and HowTo are still valid schema.org vocabulary and still useful as extraction context, but they are no longer Google rich-result levers: Google retired FAQ rich results for every site on 2026-05-07, and HowTo rich results have been deprecated since September 2023. So the plan specifies FAQPage only where a page truly is question-and-answer, routes genuine single-question user pages to `QAPage` (Google's supported type for that case) instead, never adds HowTo for Google benefit, and never promises a rich result from either. Several other types have also left Google's rich-result surface — among them ClaimReview, EstimatedSalary, LearningVideo, SpecialAnnouncement, and VehicleListing — so the plan does not reach for them either. Structured markup here is good organization, not a Google ranking lever; what it earns for AI-search citation specifically is geo-plan's call, and that is the one place the two skills overlap by design.

### Verify

```bash
# every page type in the Architecture is present, and a schema mapping exists in the plan
grep -nE "type:\s*\w+" seo-plan.md
grep -qi "schema:" seo-plan.md || echo "FAIL: no page-type-to-schema mapping in the plan"

# no retired rich-result type is sold as a Google lever (read any surviving hit in context)
grep -niE "(add|recommend|implement)[^.]*\b(FAQPage|HowTo)\b[^.]*\bgoogle\b" seo-plan.md \
  | grep -viE "never|not |retired|deprecated|informational" \
  && echo "REVIEW: a retired rich-result type may be sold as a Google lever"
```

## Performance budgets

Turn Core Web Vitals into build budgets — numbers each template is engineered to hit — rather than metrics you hope to pass after launch. The field measurement lives at the 75th percentile of real user data (Google reads it from CrUX, at both the page and the origin level, and treats it as a tiebreaker that matters most when competing content is otherwise similar), but the targets are set now: Largest Contentful Paint under 2.5 seconds, Interaction to Next Paint under 200 milliseconds, and Cumulative Layout Shift under 0.1. Budget the metric that is actually in force: INP replaced FID as the interactivity metric on March 12, 2024, so the interactivity number is INP. Those three are the entire Core Web Vitals set — a plan should refuse the blog-invented "Core Web Vitals 2.0", "Visual Stability Index", or a lowered LCP target; none is real.

Give each template the supporting budgets that make the headline numbers reachable, worked backward from where the time goes. LCP decomposes into time-to-first-byte, resource load delay, resource load time, and render delay, so the plan sets a TTFB target near 800 milliseconds or below and treats the largest above-the-fold element as a first-class asset: explicit `width` and `height` (or a reserved `aspect-ratio`) on every image and embed to hold layout still, `fetchpriority="high"` and no lazy-loading on that hero element, a matching `<link rel="preload">` when its URL is known at build, and preloaded webfonts declared `crossorigin` with `font-display: swap` or `optional` so text is never invisible while a font loads. Below-the-fold media is the mirror image: `loading="lazy"`, `decoding="async"`, responsive `srcset`/`sizes` so a phone is not shipped a desktop-width image, and a next-generation image format (WebP or AVIF) throughout so the same pixels ship far fewer bytes. Interactivity budgets keep the main thread free: scripts load `async` or `defer` rather than blocking the parser, third-party analytics and chat load lazily, `document.write` is banned outright, and the per-template JavaScript weight has a ceiling (a bundle over ~300 KB gzipped gating interaction is a red flag). Layout stability is mostly reserved space — dimensioned media, `aspect-ratio` boxes for embeds and ad slots, and metric-matched fallback fonts. Order the resource hints deliberately at the top of the head — `preconnect` for the few critical third-party origins, `preload` for the LCP image and fonts, `dns-prefetch` and `modulepreload` where they help — and stop before over-hinting, since more than a handful of preloads starts to contend with the critical path.

Write the budget with the right instrument in mind. The number that ranks is field data — real users at the 75th percentile — so the plan states field targets, but a build cannot measure field data before it has traffic; that is what lab tools are for. The build-time loop is to engineer against the budgets, profile each template in a lab tool to catch regressions, and treat the field data as the source of truth once it exists, never letting a green lab score stand in for a passing field measurement. Because a client-rendered SPA has historically been a blind spot for this measurement, another reason the rendering decision above leans server-side is that a server-rendered page is the one whose vitals are cleanly attributable in the first place.

### Verify

```bash
# the three Core Web Vitals targets are all present as budgets
for m in LCP INP CLS; do grep -qi "$m" seo-plan.md || echo "FAIL: no $m budget"; done

# a TTFB / server budget backs the LCP number
grep -qiE "ttfb|first byte|time to first byte" seo-plan.md || echo "NOTE: no TTFB budget behind LCP"

# FID must not appear as a live target - it was replaced
grep -nE "\bFID\b" seo-plan.md | grep -viE "replaced|retired|not |never" \
  && echo "REVIEW: FID referenced as a live metric"
```

## E-E-A-T and trust

Design the site's authority and trust signals into the build, because they are structural, not something sprinkled on afterward. The frame is E-E-A-T — Experience, Expertise, Authoritativeness, Trustworthiness — and its 2026 shape is set by the Quality Rater Guidelines: E-E-A-T evaluation follows the September 11, 2025 Quality Rater Guidelines update, in which Trustworthiness is the centre of the family (the other three exist to support the reader's assessment of trust) and the highest-bar YMYL topics — health, finance, legal, news, and now elections and democratic processes — demand the strongest signals. E-E-A-T is a rater concept that informs the ranking and helpful-content systems, not a dial you set, so the plan builds the signals a rater would look for rather than chasing a number.

Concretely, that means naming the trust and authorship surfaces up front. Trustworthiness gets the load-bearing structure: a reachable contact surface (address, phone, email), an about page that says who makes the content and why, a privacy policy and terms, HTTPS with a valid certificate, and visible corrections or update history. Experience and Expertise get real authorship: bylined authors with credentials, backed by `Person`/`ProfilePage` schema (the point where this layer meets the Schema plan), and content carrying first-hand signals — original screenshots and data, specific worked examples, process documentation — that generic or scraped text cannot fake. Authoritativeness is earned off-site over time (external citations, mentions, a consistent publishing record), so the plan reserves room for it rather than pretending markup creates it. For a YMYL site the same signals are non-negotiable rather than optional, and the plan sizes the effort accordingly. Because Google now makes continuous, unannounced core updates between the named ones, the helpful-content posture is treated as always-on: the plan builds the trust surface once and keeps it current rather than waiting for a labelled update to react to. Two 2026 boundaries are hard build rules: AI-assisted content is acceptable only when it carries genuine E-E-A-T, and producing an AI-targeted variant of your content falls under Google's scaled-content-abuse policy — so the plan writes one set of pages for people, never a machine-only twin. The AI-search-citation dimension of authority is geo-plan's; here the concern is the site's traditional trustworthiness and the reader in front of it.

### Verify

```bash
# the trust layer is actually planned, not assumed
grep -qiE "e-e-a-t|eeat|trust" seo-plan.md || echo "FAIL: no E-E-A-T / trust layer in the plan"
grep -qiE "author|byline|credential" seo-plan.md || echo "FAIL: no authorship plan"
grep -qiE "contact|about|privacy" seo-plan.md || echo "FAIL: no trust-surface plan (contact/about/privacy)"
# scaled-content boundary is respected: no plan to build an AI-only variant
grep -niE "(separate|variant|version).{0,30}for (ai|llm|chatgpt)" seo-plan.md \
  | grep -viE "never|not |avoid|scaled.content" \
  && echo "REVIEW: a machine-only content variant may be planned - that is scaled-content abuse"
```

## Content structure

Specify the on-page rules as template constraints the build enforces, not as advice writers may follow: a title of roughly 50–60 characters (30 at the very least), unique, with the primary term early; a meta description of roughly 150–160 characters (120 at the least), unique, written as a SERP call to action; exactly one `h1` with a heading hierarchy that mirrors how people phrase the topic; descriptive anchor text; and meaningful `alt` (about 10–125 characters) on every non-decorative image. Give each page type a word floor the template guarantees so thin pages cannot ship, and a freshness policy — a visible publication date on articles, a last-updated date where content is materially revised — since undated content ages badly against dated competitors. Two rules carry more weight than the rest. Lead each section with a direct, self-contained answer before elaborating — that is good writing that also reads cleanly to any extractor, but it is organization, not a Google ranking lever. And plan the content as a topical cluster rather than one thin page per keyword, so the site covers a subject instead of chasing a term.

That is where this skill stops. Turning a well-structured site into an AI-search citation strategy — which engines reward which structures, and how a page earns a citation — is geo-plan's work, and the content plan should hand off to it once the structure is sound.

### Verify

```bash
grep -qiE "title" seo-plan.md && grep -qiE "description|meta" seo-plan.md \
  || echo "FAIL: title/description rules missing"
grep -qiE "h1|heading" seo-plan.md || echo "FAIL: no heading-structure rule"
grep -qiE "word|words:" seo-plan.md || echo "NOTE: no per-type word floor set"
```

## Attribution

Synthesized by SkillFed from the seo-skills bundle members and their pinned reference files: seo (schema/robots/canonical/hreflang/mobile implementation, the FAQ, HowTo, and llms.txt era facts, and the JSON-LD templates in `references/json-ld-templates.md`); geo-technical (the technical-foundation categories — crawlability, indexability, rendering, mobile, Core Web Vitals, and speed — and the facts that AI crawlers do not execute JavaScript and that Google crawls with mobile Googlebot only); seo-validate (framework-conditioned build rules plus its `reference/spa-ssg-patterns.md` rendering-mode decisions, `reference/core-web-vitals.md` performance detail, and `reference/w3c-guidelines.md` semantics and hreflang rules); claude-seo (planning structure and its `references/eeat-framework.md` E-E-A-T framework, `references/schema-types.md` per-type schema status, `references/cwv-thresholds.md` budgets, and `references/quality-gates.md` page-type and location-page gates, plus the INP-replaced-FID fact); and ai-seo (the principle that structural patterns are good organization, not a Google ranking lever, and the scaled-content-abuse boundary). Every fact traces to a verified source and the prose is original; no wild skill body was used. Once the site is built, verify the plan with the auditors (geo-technical, geo-audit, seo-validate); for AI-search citation specifically, pair with geo-plan. Licensed under MIT.
