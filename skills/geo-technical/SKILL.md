---
name: geo-technical
description: 'Score a live site''s readiness to be read by machines: fetch raw HTML, hold it against the
  browser render, and grade eight infrastructure categories out of 100 before any content or GEO work
  starts. Use when pages rank nowhere, AI assistants never cite the site, or a JavaScript framework may
  be hiding the copy from crawlers. Era-stamped for 2026 — retired rich-result types and unproven conventions
  stay out of the score.'
license: MIT
treatment: derivative
derived_from:
- id: zubair-trabzada/geo-seo-claude/geo-technical
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: 602355e470fff83367651c25068c5b51515f44cc7cf19c8aa3eaf5a9accb720b
targeted_version: web and AI-crawler behavior as of 2026-08
last_verified_at: 2026-08-10
---

# GEO Technical SEO Audit

## Conditions

### When to use
- A live, publicly reachable site needs a technical audit before (or alongside) AI-search or content work — this is the infrastructure layer both depend on.
- Pages rank nowhere or are never cited by AI assistants, and you suspect the cause sits below the content: blocked crawlers, client-side rendering, broken canonicals, slow servers.
- You need a scored, evidence-backed report (a 100-point rubric with per-category breakdowns) where every finding traces to a fetch that was actually run.
- No toolchain install is warranted or available: a shell with `curl` suffices here (see Prerequisites), where the orchestrated-suite alternative (claude-seo) needs its own isolated Python runtime and Chromium before it can audit anything.

### When NOT to use
- The work lives in a repository, not at a URL. This audit inspects a deployed site over HTTP; it cannot read a codebase or catch problems before they ship.
- You need content, keyword, or citation-quality analysis. This document scores infrastructure only and says nothing about what the words should be.
- The site is not fetchable from where you run (auth walls, intranet-only, geo-blocks). Every check here starts from a fetch; an unreachable site produces no score — report that instead of estimating.
- You want evidence of what AI crawlers actually did over time. That lives in server access logs, which this audit does not read.
- You just need a fast scored verdict on AI-crawler legibility, not an eight-category inspection: the bundle's ~30-second scripted check (geo-audit) answers that; return here when its low score needs diagnosis.
- On ordinary business sites, the 9.1 service-discovery result never reaches the report — the header capture itself rides the standard homepage fetch at no cost, so run it either way. The rule (stated in Category 9) scopes the report, not the fetch, and is repeated here so an agent scoping the engagement knows the section is intentionally absent for such sites.

### Prerequisites
- The target homepage URL plus 2-3 representative inner pages (an article, a product page, a category page).
- A shell with `curl` — every Verify block below uses it — plus an HTTP-fetch capability for full page retrieval.
- A way to see the browser-rendered DOM for the Category 7 comparison: a headless browser, browser devtools, or a rendering fetch tool.
- Write access to the working directory for the generated `GEO-TECHNICAL-AUDIT.md`. No credentials or third-party API keys are required.

### What breaks first
- The era facts. Schema-type status and emerging conventions (llms.txt, markdown content negotiation) rot faster than anything else in this category — the ## Era section pins their state as of this document's review date.
- The AI crawler roster in 1.2. New bots appear and user-agent strings change; treat the table as a snapshot to extend, not a complete census.
- Core Web Vitals metric definitions. The metric set has changed before (INP for FID in 2024) and can change again, taking Category 6's thresholds with it.
- The markdown content-negotiation check in 9.2 is currently Cloudflare-specific; the check outlives the vendor detail, but the remediation advice may not.

## Era

This document targets web and AI-crawler behavior as of August 2026 (reviewed 2026-08-10). The dated facts below are load-bearing; when one of them moves, the checks resting on it move too.

- **AI crawlers do not execute JavaScript.** GPTBot, PerplexityBot, ClaudeBot and their peers fetch raw HTML and parse it; a client-rendered page is invisible to them regardless of copy quality. This is the main basis of Category 7's 15/100 weight — the rest of the retained rationale is Googlebot's rendering-queue deprioritization of JS-rendered content — and it makes server-side rendering a first-class scored category here, not a footnote.
- **Google retired FAQ rich results for every site on 2026-05-07**, and HowTo has been deprecated since Sept 2023. When inspecting structured data (Category 7's JSON-LD check), treat existing FAQPage or HowTo markup as inert: never recommend deploying either for rich-result benefit, and never count their absence against the score.
- **llms.txt is a proposed convention at roughly 0.015% adoption with no vendor confirmation.** This audit deliberately assigns it no points and no check; if a client asks, report its presence as informational at most.
- **Since July 2024 there is no desktop crawling — Google crawls ALL sites exclusively with mobile Googlebot** (Category 5).
- **INP replaced FID in March 2024**; Category 6 carries the 2026 thresholds, benchmarked at the 75th percentile of field data.
- Google has ignored `rel="next"` / `rel="prev"` since 2019; Bing still reads them (Category 2).

## Purpose

Technical SEO forms the foundation of both traditional search visibility and AI search citation. A technically broken site cannot be crawled, indexed, or cited by any platform. This skill audits 8 categories of technical health with specific attention to GEO requirements — most critically, **server-side rendering** (AI crawlers do not execute JavaScript) and **AI crawler access** (many sites inadvertently block AI crawlers in robots.txt).

## How to Use This Skill

1. Collect the target URL (homepage + 2-3 key inner pages)
2. Fetch each page using curl/WebFetch to get raw HTML and HTTP headers
3. Run through each of the 8 audit categories below
4. Score each category using the rubric
5. Generate GEO-TECHNICAL-AUDIT.md with results
6. Score a category only after running its `### Verify` commands — findings cite command output, never assumptions

---

## Category 1: Crawlability (15 points)

### 1.1 robots.txt Validity
- Fetch `https://[domain]/robots.txt`
- Check for syntactic validity: proper `User-agent`, `Allow`, `Disallow` directives
- Check for common errors: missing User-agent, wildcards blocking important paths, Disallow: / blocking entire site
- Verify XML sitemap is referenced: `Sitemap: https://[domain]/sitemap.xml`

### 1.2 AI Crawler Access (CRITICAL for GEO)
Check robots.txt for directives targeting these AI crawlers:

| Crawler | User-Agent | Platform |
|---|---|---|
| GPTBot | GPTBot | ChatGPT / OpenAI |
| Google-Extended | Google-Extended | Gemini / Google AI training |
| Googlebot | Googlebot | Google Search + AI Overviews |
| Bingbot | bingbot | Bing Copilot + ChatGPT (via Bing) |
| PerplexityBot | PerplexityBot | Perplexity AI |
| ClaudeBot | ClaudeBot | Anthropic Claude |
| Amazonbot | Amazonbot | Alexa / Amazon AI |
| CCBot | CCBot | Common Crawl (used by many AI models) |
| FacebookBot | FacebookExternalHit | Meta AI |
| Bytespider | Bytespider | TikTok / ByteDance AI |
| Applebot-Extended | Applebot-Extended | Apple Intelligence |

**Scoring for AI crawler access:**
- All major AI crawlers allowed: 5 points
- Some blocked but Googlebot + Bingbot allowed: 3 points
- GPTBot or PerplexityBot blocked: 1 point (significant GEO impact)
- Googlebot blocked: 0 points (fatal)

**Important nuance**: Blocking Google-Extended does NOT block Googlebot. Google-Extended only controls AI training data usage, not search indexing. Whether blocking Google-Extended affects AI Overviews inclusion is unverified (2026-08-10) — blocking Googlebot is what verifiably removes AI Overviews presence. Recommend allowing Google-Extended unless there is a specific data licensing concern.

### 1.3 XML Sitemaps
- Fetch sitemap (check robots.txt for location, or try `/sitemap.xml`, `/sitemap_index.xml`)
- Validate XML syntax
- Check for `<lastmod>` dates (should be present and accurate)
- Count URLs — compare to expected number of indexable pages
- Check for sitemap index if large site (50,000+ URLs per sitemap max)
- Verify all sitemap URLs return 200 status codes (sample check)

### 1.4 Crawl Depth
- Homepage = depth 0. Check that all important pages are reachable within **3 clicks** (depth 3)
- Pages at depth 4+ receive significantly less crawl budget and are less likely to be cited by AI
- Check internal linking: are key content pages linked from the homepage or main navigation?

### 1.5 Noindex Management
- Check for `<meta name="robots" content="noindex">` on pages that SHOULD be indexed
- Check for `X-Robots-Tag: noindex` HTTP headers
- Common mistakes: noindex on paginated pages, category pages, or key landing pages

**Category Scoring:**
| Check | Points |
|---|---|
| robots.txt valid and complete | 3 |
| AI crawlers allowed | 5 |
| XML sitemap present and valid | 3 |
| Crawl depth within 3 clicks | 2 |
| No erroneous noindex directives | 2 |

### Verify
Run against the audited domain (replace `example.com` throughout):

```bash
# robots.txt exists, parses, and references a sitemap
curl -s https://example.com/robots.txt | grep -inE '^(user-agent|allow|disallow|sitemap):'

# AI crawler directives actually present in robots.txt
curl -s https://example.com/robots.txt | grep -iE 'gptbot|google-extended|perplexitybot|claudebot|ccbot|bytespider|applebot-extended|amazonbot|bingbot'

# robots.txt permission is a claim; the server's answer is the fact.
# If an allowed AI bot gets a 403 here, the block lives in the WAF/CDN layer, not robots.txt.
curl -s -o /dev/null -w 'GPTBot UA  -> %{http_code}\n' -A 'GPTBot' https://example.com/
curl -s -o /dev/null -w 'default UA -> %{http_code}\n' https://example.com/

# sitemap resolves and is XML
curl -s -o /dev/null -w '%{http_code} %{content_type}\n' https://example.com/sitemap.xml

# sample 3-5 sitemap URLs for 200s
curl -s -o /dev/null -w '%{http_code}\n' https://example.com/some-page-from-sitemap
```

Pass looks like: robots.txt parses with no site-wide `Disallow: /`, the two user-agent fetches return the same 2xx status, and every sampled sitemap URL returns 200. A status mismatch between the UA fetches is a finding robots.txt inspection alone cannot see. A matching status clears UA-level blocks only: a WAF that verifies real crawlers by IP/ASN can pass a spoofed user-agent while still blocking the genuine bot, so a match is one-directional evidence, never proof of access.

---

## Category 2: Indexability (12 points)

### 2.1 Canonical Tags
- Every indexable page must have a `<link rel="canonical" href="...">` tag
- Canonical must point to itself (self-referencing) for the authoritative version
- Check for conflicting canonicals (canonical in HTML vs. HTTP header)
- Check for canonical chains (A canonicals to B, B canonicals to C — should be A to C)

### 2.2 Duplicate Content
- Check for www vs. non-www (both should resolve, one should redirect)
- Check for HTTP vs. HTTPS (HTTP should redirect to HTTPS)
- Check for trailing slash consistency (pick one pattern and redirect the other)
- Check for parameter-based duplicates (`?sort=price` creating duplicate pages)

### 2.3 Pagination
- If paginated content exists, check for `rel="next"` / `rel="prev"` (note: Google ignores these as of 2019, but Bing still uses them)
- Preferred: use `rel="canonical"` on paginated pages pointing to a view-all page or the first page
- Ensure paginated pages are not noindexed if they contain unique content

### 2.4 Hreflang (international sites)
- Check for `<link rel="alternate" hreflang="xx">` tags
- Validate: reciprocal hreflang (if page A points to page B, B must point back to A)
- Validate: x-default fallback exists
- Check for language/region code validity (ISO 639-1 / ISO 3166-1)

### 2.5 Index Bloat
- Estimate number of indexed pages (check sitemap count, use `site:domain.com` estimate)
- Compare indexed pages to actual valuable content pages
- Flag if indexed pages significantly exceed content pages (index bloat from thin/duplicate/parameter pages)

**Category Scoring:**
| Check | Points |
|---|---|
| Canonical tags correct on all pages | 3 |
| No duplicate content issues | 3 |
| Pagination handled correctly | 2 |
| Hreflang correct (if applicable) | 2 |
| No index bloat | 2 |

### Verify

```bash
# canonical present and self-referencing on each audited page
curl -s https://example.com/ | grep -io '<link[^>]*rel="canonical"[^>]*>'

# no HTTP-header canonical conflicting with the HTML one
curl -sI https://example.com/ | grep -i '^link:.*canonical'

# duplicate-surface resolution: one scheme + host should win via 301
curl -sI -o /dev/null -w '%{http_code} -> %{redirect_url}\n' http://example.com/
curl -sI -o /dev/null -w '%{http_code} -> %{redirect_url}\n' https://www.example.com/
```

Pass looks like: exactly one canonical per page pointing at the fetched URL, and both alternate-surface fetches answering 301 to the single canonical origin. Two 200s on different hosts is a duplicate-content finding.

---

## Category 3: Security (10 points)

### 3.1 HTTPS Enforcement
- Site must load over HTTPS
- HTTP must redirect to HTTPS (301 redirect)
- No mixed content warnings (HTTP resources on HTTPS pages)
- SSL/TLS certificate must be valid and not expired

### 3.2 Security Headers
Check HTTP response headers for:

| Header | Required Value | Purpose |
|---|---|---|
| `Strict-Transport-Security` | `max-age=31536000; includeSubDomains` | Forces HTTPS |
| `Content-Security-Policy` | Appropriate policy | Prevents XSS |
| `X-Content-Type-Options` | `nosniff` | Prevents MIME sniffing |
| `X-Frame-Options` | `DENY` or `SAMEORIGIN` | Prevents clickjacking |
| `Referrer-Policy` | `strict-origin-when-cross-origin` or stricter | Controls referrer data |
| `Permissions-Policy` | Appropriate restrictions | Controls browser features |

**Category Scoring:**
| Check | Points |
|---|---|
| HTTPS enforced with valid cert | 4 |
| HSTS header present | 2 |
| X-Content-Type-Options | 1 |
| X-Frame-Options | 1 |
| Referrer-Policy | 1 |
| Content-Security-Policy | 1 |

### Verify

```bash
# HTTP must 301 to HTTPS
curl -sI -o /dev/null -w '%{http_code} -> %{redirect_url}\n' http://example.com/

# all six security headers in one pass
curl -sI https://example.com/ | grep -iE '^(strict-transport-security|content-security-policy|x-content-type-options|x-frame-options|referrer-policy|permissions-policy):'

# certificate validity (curl prints cert details verbosely; an invalid cert fails the fetch outright)
curl -sv -o /dev/null https://example.com/ 2>&1 | grep -iE 'expire|subject:|issuer:'
```

Pass looks like: a 301 to the HTTPS origin, all six headers present in the grep output, and a certificate expiry date comfortably in the future. Score each header from this output, not from assumption.

---

## Category 4: URL Structure (8 points)

### 4.1 Clean URLs
- URLs should be human-readable: `/blog/seo-guide` not `/blog?id=12345`
- No session IDs in URLs
- Lowercase only (no mixed case)
- Hyphens for word separation (not underscores)
- No special characters or encoded spaces

### 4.2 Logical Hierarchy
- URL path should reflect site architecture: `/category/subcategory/page`
- Flat where appropriate — avoid unnecessarily deep nesting
- Consistent pattern across the site

### 4.3 Redirect Chains
- Check for redirect chains (A redirects to B redirects to C)
- Maximum 1 hop recommended (A redirects to C directly)
- Check for redirect loops
- All redirects should be 301 (permanent), not 302 (temporary), unless intentionally temporary

### 4.4 Parameter Handling
- URL parameters should not create duplicate indexable pages
- Use canonical tags or `robots.txt` Disallow for parameter variations
- Configure parameter handling in Bing Webmaster Tools; Google Search Console no longer offers a parameter-handling control, so on the Google side the canonical and robots.txt guidance above carries the whole job

**Category Scoring:**
| Check | Points |
|---|---|
| Clean, readable URLs | 2 |
| Logical hierarchy | 2 |
| No redirect chains (max 1 hop) | 2 |
| Parameter handling configured | 2 |

### Verify

```bash
# redirect chains: hops > 1 on a common entry path means a chain
curl -sIL -o /dev/null -w 'hops: %{num_redirects}  final: %{url_effective}\n' https://example.com/old-path

# repeat for case and trailing-slash variants — each should resolve in one hop
curl -sIL -o /dev/null -w 'hops: %{num_redirects}  final: %{url_effective}\n' https://example.com/Blog/
```

Pass looks like: `hops: 0` or `hops: 1` on every variant tested, all landing on the same canonical form. `hops: 2+` is a chain finding with the exact path as evidence.

---

## Category 5: Mobile Optimization (10 points)

### Critical Context
As of **July 2024**, Google crawls ALL sites exclusively with mobile Googlebot. There is no desktop crawling. If your site does not work on mobile, it does not work for Google. Period.

### 5.1 Responsive Design
- Check for `<meta name="viewport" content="width=device-width, initial-scale=1">`
- Content must not require horizontal scrolling on mobile
- No fixed-width layouts wider than viewport

### 5.2 Tap Targets
- Interactive elements (buttons, links) must be at least 48x48 CSS pixels
- Minimum 8px spacing between tap targets
- Check that navigation is usable on mobile

### 5.3 Font Sizes
- Base font size should be at least 16px
- No text requiring zoom to read
- Sufficient contrast ratio (WCAG AA: 4.5:1 for normal text, 3:1 for large text)

### 5.4 Mobile Content Parity
- All content visible on desktop must also be visible on mobile
- No hidden content behind "read more" toggles that Googlebot cannot expand (though Google has improved at expanding these as of 2025)
- Images and media must load on mobile

**Category Scoring:**
| Check | Points |
|---|---|
| Viewport meta tag correct | 3 |
| Responsive layout (no horizontal scroll) | 3 |
| Tap targets appropriately sized | 2 |
| Font sizes legible | 2 |

### Verify

```bash
# viewport meta present in the raw HTML
curl -s https://example.com/ | grep -io '<meta[^>]*name="viewport"[^>]*>'
```

Pass looks like: exactly one viewport meta containing `width=device-width` — zero matches is an immediate viewport-meta fail, and duplicate viewport tags are a finding in their own right. This is the crawl-side half. Tap targets, font sizes, and horizontal scroll need the rendered viewport — verify them in browser devtools mobile emulation, and record which pages you emulated in the report.

---

## Category 6: Core Web Vitals (15 points)

### 2026 Metrics and Thresholds
Core Web Vitals use the **75th percentile** of real user data (field data) as the benchmark. Lab data is useful for debugging but field data determines the ranking signal.

| Metric | Good | Needs Improvement | Poor | Notes |
|---|---|---|---|---|
| **LCP** (Largest Contentful Paint) | < 2.5s | 2.5s - 4.0s | > 4.0s | Measures loading — time until largest visible element renders |
| **INP** (Interaction to Next Paint) | < 200ms | 200ms - 500ms | > 500ms | Replaced FID in March 2024. Measures ALL interactions, not just first |
| **CLS** (Cumulative Layout Shift) | < 0.1 | 0.1 - 0.25 | > 0.25 | Measures visual stability — unexpected layout movements |

### How to Assess Without CrUX Data
When real user data is unavailable, estimate from page characteristics:
- **LCP**: Check largest above-fold element. Is it an image (check size/format)? Is it text (check web font loading)? Server response time (TTFB)?
- **INP**: Check for heavy JavaScript on page. Long tasks (>50ms) block interactivity. Check for third-party scripts.
- **CLS**: Check for images without explicit width/height. Check for dynamically inserted content above the fold. Check for web fonts causing layout shift (FOUT/FOIT).

### Common LCP Fixes
1. Optimize hero images: WebP/AVIF format, correct sizing, preload with `<link rel="preload">`
2. Reduce server response time (TTFB < 800ms)
3. Eliminate render-blocking CSS/JS
4. Preconnect to critical third-party origins

### Common INP Fixes
1. Break up long tasks (>50ms) into smaller chunks using `requestIdleCallback` or `scheduler.yield()`
2. Reduce third-party JavaScript
3. Use `content-visibility: auto` for off-screen content
4. Debounce/throttle event handlers

### Common CLS Fixes
1. Always include `width` and `height` attributes on images and videos
2. Reserve space for ads and embeds with CSS `aspect-ratio` or explicit dimensions
3. Use `font-display: swap` with size-adjusted fallback fonts
4. Avoid inserting content above existing content after page load

**Category Scoring:**
| Check | Points |
|---|---|
| LCP < 2.5s | 5 |
| INP < 200ms | 5 |
| CLS < 0.1 | 5 |

### Verify

```bash
# CLS risk: images shipped without explicit dimensions
curl -s https://example.com/ | grep -io '<img[^>]*>' | grep -vic 'width='

# LCP risk: lazy-loading near the top of the document (should be 0)
curl -s https://example.com/ | head -c 20000 | grep -ic 'loading="lazy"'

# server share of LCP
curl -o /dev/null -s -w 'TTFB: %{time_starttransfer}s\n' https://example.com/
```

These are lab-side proxies for scoring when field data is out of reach: a non-zero count on either grep is a concrete CLS/LCP finding with the offending tags as evidence. When CrUX field data is available to you, it wins — the thresholds above are defined against the field, not the lab.

---

## Category 7: Server-Side Rendering (15 points) — CRITICAL FOR GEO

### Why SSR Is Mandatory for AI Visibility
AI crawlers (GPTBot, PerplexityBot, ClaudeBot, etc.) do **NOT execute JavaScript**. They fetch the raw HTML and parse it. If your content is rendered client-side by React, Vue, Angular, or any other JavaScript framework, AI crawlers see an empty page.

Even Googlebot, which does execute JavaScript, deprioritizes JS-rendered content due to the additional crawl budget required. Google processes JS rendering in a separate "rendering queue" that can delay indexing by days or weeks.

### Detection Method
1. Fetch the page with curl (no JavaScript execution): `curl -s [URL]`
2. Compare the raw HTML to the rendered DOM (via browser)
3. If key content (headings, paragraphs, product info, article text) is MISSING from the curl output, the site relies on client-side rendering

### What to Check
- **Main content text**: Is the article body / product description / page content in the raw HTML?
- **Headings**: Are H1, H2, H3 tags present in raw HTML?
- **Navigation**: Is the main navigation server-rendered?
- **Structured data**: Is JSON-LD in the raw HTML or injected by JavaScript?
- **Meta tags**: Are title, description, canonical, OG tags in the raw HTML?
- **Internal links**: Are navigation and content links in the raw HTML? (Critical for crawlability)

### SSR Solutions to Recommend
| Framework | SSR Solution |
|---|---|
| React | Next.js (SSR/SSG), Remix, Gatsby (SSG) |
| Vue | Nuxt.js (SSR/SSG) |
| Angular | Angular Universal |
| Svelte | SvelteKit |
| Generic | Prerender.io (prerendering service) |

### Scoring Detail
- All key content server-rendered: 15 points
- Main content server-rendered but some elements JS-only: 10 points
- Critical content requires JS (product info, article text): 5 points
- Entire page is client-rendered (empty body in raw HTML): 0 points

**Category Scoring:**
| Check | Points |
|---|---|
| Main content in raw HTML | 8 |
| Meta tags + structured data in raw HTML | 4 |
| Internal links in raw HTML | 3 |

### Verify
The detection method above is itself the verification loop — run it as commands, not as a judgment call:

```bash
# key-content presence: replace the quoted string with a phrase you can read in the
# BROWSER-rendered article body (run once per phrase, 2-3 phrases per page)
curl -s https://example.com/article | grep -c -iF 'a phrase copied from the rendered article body'

# headings visible to a no-JS fetcher
curl -s https://example.com/article | grep -c -iE '<h[1-3]'

# meta tags and JSON-LD in the raw HTML
curl -s https://example.com/article | grep -c -iE '<title>|name="description"|rel="canonical"|application/ld\+json'

# corroborating signal only: words visible to a no-JS fetcher, with multi-line
# script/style payloads stripped so hydration blobs and inline CSS cannot count as words
curl -s https://example.com/article | perl -0777 -pe 's/<script\b.*?<\/script>//gis; s/<style\b.*?<\/style>//gis; s/<[^>]*>/ /g' | tr -s '[:space:]' ' ' | wc -w
```

Pass is decided on key content, not word magnitude: copy 2-3 phrases you can read in the browser-rendered body (the opening sentence, one mid-article claim, the closing line) and run the key-content grep for each — every phrase must be found in the raw HTML, headings > 0, and the meta/JSON-LD grep > 0. The word count corroborates the verdict but never decides it: a curl-side count far below the browser-rendered count confirms client-side rendering, while a healthy-looking count proves nothing on its own — surviving markup or data can still inflate it. A missing key phrase IS the client-side-rendering finding: quote the phrase and both word counts in the report, and score the category from what the raw HTML actually contains.

---

## Category 8: Page Speed & Server Performance (15 points)

### 8.1 Time to First Byte (TTFB)
- Target: **< 800ms** (ideally < 200ms)
- Measure with curl: `curl -o /dev/null -s -w 'TTFB: %{time_starttransfer}s\n' [URL]`
- If TTFB > 800ms: check server location, caching, database queries, CDN usage

### 8.2 Resource Optimization
- Total page weight target: **< 2MB** (critical pages < 1MB)
- Check for uncompressed resources (gzip/brotli compression should be enabled)
- Check for unminified CSS and JavaScript
- Check for unused CSS/JS (can represent 50%+ of downloaded bytes on many sites)

### 8.3 Image Optimization
- Check image formats: WebP or AVIF preferred over JPEG/PNG
- Check for oversized images (images larger than display size)
- Check for lazy loading: images below fold should have `loading="lazy"`
- Check for explicit dimensions (width/height attributes prevent CLS)
- Above-fold images should NOT be lazy loaded (harms LCP)

### 8.4 Code Splitting and Lazy Loading
- JavaScript should be code-split so each page only loads what it needs
- Check for large JavaScript bundles (> 200KB compressed is a warning, > 500KB is critical)
- Third-party scripts should load asynchronously (`async` or `defer`)
- Check for render-blocking resources in `<head>`

### 8.5 Caching
- Check `Cache-Control` headers on static resources (images, CSS, JS)
- Static assets should have long cache times: `max-age=31536000` (1 year) with content-hashed filenames
- HTML pages should have shorter cache or `no-cache` with validation (`ETag` or `Last-Modified`)

### 8.6 CDN Usage
- Check if static resources are served from a CDN (different domain or CDN-specific headers)
- For global audience, CDN is critical for consistent performance
- Check for CDN-specific headers: `CF-Ray` (Cloudflare), `X-Cache` (AWS CloudFront), `X-Served-By` (Fastly)

**Category Scoring:**
| Check | Points |
|---|---|
| TTFB < 800ms | 3 |
| Page weight < 2MB | 2 |
| Images optimized (format, size, lazy) | 3 |
| JS bundles reasonable (< 200KB compressed) | 2 |
| Compression enabled (gzip/brotli) | 2 |
| Cache headers on static resources | 2 |
| CDN in use | 1 |

### Verify

```bash
# timing and weight in one fetch
curl -o /dev/null -s -w 'TTFB: %{time_starttransfer}s  total: %{time_total}s  bytes: %{size_download}\n' https://example.com/

# compression and cache validation headers
curl -sI -H 'Accept-Encoding: gzip, br' https://example.com/ | grep -iE '^(content-encoding|cache-control|etag|last-modified):'

# CDN fingerprints
curl -sI https://example.com/ | grep -iE '^(cf-ray|x-cache|x-served-by|server):'
```

Pass looks like: TTFB under 0.8s, a `content-encoding` of gzip or br, cache headers on the response, and (for the CDN point) at least one CDN fingerprint header. That covers 8 of the category's 15 points (TTFB, compression, caching, CDN). The `bytes:` figure is the HTML document alone — the 8.2 page-weight target counts all resources — so page weight, image optimization, and JS bundle size are scored from a rendered-page resource inventory (browser devtools Network panel or a rendering fetch tool), not from these outputs.

---

## Category 9: Agent-Readiness Signals (non-scoring)

These checks surface emerging AI agent compatibility signals. None contribute to the numeric score — they produce a pass or a recommendation. The underlying standards are either IETF drafts or early-adoption features; penalizing absence would be unfair.

### 9.1 RFC 8288 Link Headers (Service Discovery)

RFC 8288 (Web Linking) defines the HTTP `Link:` response header. Servers can use it to advertise related resources — API catalog, service docs, MCP server card — in a machine-readable way, without HTML parsing.

**How to check:** Capture all `Link:` response headers from the standard homepage fetch (no extra request).

**What to look for:**
- Parse `<url>; rel="relation-type"` pairs.
- High-value rel types: `api-catalog` (RFC 9609), `describedby`, `service-doc`, `mcp-server-card`.

**When to surface a recommendation:** Only for API-first sites (API docs linked in nav, `/api/` or `/developers/` paths, swagger/OpenAPI in sitemap). Omit this section entirely for standard business sites — absence is expected and not noteworthy.

| State | Treatment |
|---|---|
| `Link:` headers present, known rel types | Informational — document what was found |
| `Link:` headers present, unknown rel types | Informational — note and explain |
| Absent, API-first site | Recommendation — explain and suggest implementation |
| Absent, standard business site | Omit — do not surface |

### 9.2 Markdown Content Negotiation

Checks if the server responds to `Accept: text/markdown` with `Content-Type: text/markdown`. Cloudflare's "Markdown for Agents" feature enables this — AI agents receive clean Markdown instead of HTML, eliminating boilerplate stripping and improving content extraction accuracy.

**How to check:** Send a GET to the homepage with `Accept: text/markdown`. This is one additional HTTP request per audit.

**Evaluation:**
- If response `Content-Type` is `text/markdown` (or `text/markdown; charset=utf-8`): pass — note as a leading-edge capability.
- Otherwise: forward-looking recommendation, not a failure.
- If the request errors or returns non-200: skip and note the error. Do not penalize.

| State | Treatment |
|---|---|
| `text/markdown` returned | Bonus — note as a leading-edge capability |
| Standard HTML returned | Forward-looking recommendation |
| Request errors / non-200 | Skip, note the error, do not penalize |

### Verify

```bash
# Link headers ride the standard homepage fetch — no extra request
curl -sI https://example.com/ | grep -i '^link:'

# markdown content negotiation — the one additional request this category allows
curl -s -o /dev/null -w '%{http_code} %{content_type}\n' -H 'Accept: text/markdown' https://example.com/
```

Outputs here inform pass/recommendation notes only; nothing in this block moves the score, and for a standard business site the 9.1 result is omitted from the report entirely per the table above.

---

## IndexNow Protocol

### What It Is
IndexNow is an open protocol that allows websites to notify search engines instantly when content is created, updated, or deleted. Supported by Bing, Yandex, Seznam, and Naver. Google does NOT support IndexNow but monitors the protocol.

### Why It Matters for GEO
ChatGPT uses Bing's index. Bing Copilot uses Bing's index. Faster Bing indexing means faster AI visibility on two major platforms.

### Implementation Check
1. Check for IndexNow key file: `https://[domain]/.well-known/indexnow-key.txt` or similar
2. Check if CMS has IndexNow plugin (WordPress: IndexNow plugin; many modern CMS platforms support it natively)
3. If not implemented, recommend adding it with instructions

### Verify

```bash
# key file at the conventional location (also try the root and CMS-specific paths)
curl -s -o /dev/null -w '%{http_code}\n' https://example.com/.well-known/indexnow-key.txt
```

A 200 means IndexNow is provisioned at that path; a 404 alone is not conclusive (keys may live at other paths or be CMS-managed), so pair the fetch with the CMS plugin check before recommending.

---

## Overall Scoring

| Category | Max Points | Weight |
|---|---|---|
| Crawlability | 15 | Core foundation |
| Indexability | 12 | Core foundation |
| Security | 10 | Trust signal |
| URL Structure | 8 | Crawl efficiency |
| Mobile Optimization | 10 | Google requirement |
| Core Web Vitals | 15 | Ranking signal |
| Server-Side Rendering | 15 | GEO critical |
| Page Speed & Server | 15 | Performance |
| **Total** | **100** | |

Non-scoring checks (Category 9) appear in the output under "Agent-Readiness Signals" and do not affect this total.

### Score Interpretation
- **90-100**: Excellent — technically sound for both traditional SEO and GEO
- **70-89**: Good — minor issues to address but fundamentally solid
- **50-69**: Needs Work — significant technical debt impacting visibility
- **30-49**: Poor — major issues blocking crawling, indexing, or AI visibility
- **0-29**: Critical — fundamental technical failures requiring immediate attention

---

## Output Format

Generate **GEO-TECHNICAL-AUDIT.md** with:

```markdown
# GEO Technical SEO Audit — [Domain]
Date: [Date]

## Technical Score: XX/100

## Score Breakdown
| Category | Score | Status |
|---|---|---|
| Crawlability | XX/15 | Pass/Warn/Fail |
| Indexability | XX/12 | Pass/Warn/Fail |
| Security | XX/10 | Pass/Warn/Fail |
| URL Structure | XX/8 | Pass/Warn/Fail |
| Mobile Optimization | XX/10 | Pass/Warn/Fail |
| Core Web Vitals | XX/15 | Pass/Warn/Fail |
| Server-Side Rendering | XX/15 | Pass/Warn/Fail |
| Page Speed & Server | XX/15 | Pass/Warn/Fail |

Status: Pass = 80%+ of category points, Warn = 50-79%, Fail = <50%

## AI Crawler Access
| Crawler | User-Agent | Status | Recommendation |
|---|---|---|---|
| GPTBot | GPTBot | Allowed/Blocked | [Action] |
| Googlebot | Googlebot | Allowed/Blocked | [Action] |
[Continue for all AI crawlers]

## Critical Issues (fix immediately)
[List with specific page URLs and what is wrong]

## Warnings (fix this month)
[List with details]

## Recommendations (optimize this quarter)
[List with details]

## Agent-Readiness Signals (non-scoring)

### RFC 8288 Link Headers (Service Discovery)

**Status:** Present / Absent / Not Applicable

<!-- If present: -->
| Relation Type | URL | Meaning |
|---|---|---|
| api-catalog | /.well-known/api-catalog | Machine-readable index of available APIs |
| mcp-server-card | /.well-known/mcp.json | MCP server capability declaration |

AI agents and API clients can discover your services without parsing HTML.

<!-- If absent, API-first site only: -->
**Informational Recommendation:** This site has API/developer-oriented content but no `Link:` headers advertising discoverable services.

Example: `Link: </.well-known/api-catalog>; rel="api-catalog"`

Relevant for: sites with public APIs, OpenAPI docs, or MCP server integrations.
Reference: RFC 8288, RFC 9609.

<!-- If absent, standard business site: omit this section entirely -->

### Markdown Content Negotiation

**Status:** Supported / Not Supported
**Test:** GET [url] with `Accept: text/markdown`
**Response Content-Type:** [value]

<!-- If supported: -->
This site serves clean Markdown to AI agents on request. AI crawlers that support content negotiation receive formatted text without HTML boilerplate.

<!-- If not supported: -->
**Forward-Looking Recommendation:** Cloudflare Workers/Pages sites can enable Markdown content negotiation with a one-line configuration change. When an AI agent sends `Accept: text/markdown`, the server responds with clean Markdown instead of HTML.

- Currently Cloudflare-specific
- Relevant for: sites already on Cloudflare infrastructure
- Other CDNs and frameworks expected to adopt this pattern as AI agent traffic grows

## Detailed Findings
[Per-category breakdown with evidence]

## Era Notes
This audit applied the era facts pinned in the auditing skill's Era section (skill reviewed [skill last-verified date]): AI crawlers evaluated on raw HTML only; FAQ rich results retired 2026-05-07; HowTo deprecated Sept 2023; llms.txt not scored (proposed convention, no vendor confirmation).
```

---

## Findings

Recorded from our editorial review of the base document (2026-08-10):

- **Defects fixed:** one, applied at the bundle review (Stage 2.5, 2026-08-10): the base's 1.2 nuance hedged that blocking Google-Extended could cost AI Overviews presence — an unverified vendor-behavior claim no input confirms. It now states the effect as unverified, with blocking Googlebot named as what verifiably removes AI Overviews presence. Otherwise none in the retained text: the base was current on its own dated facts at review time — its Core Web Vitals table already carries the 2026 thresholds, and its agent-readiness category was already explicitly non-scoring. Two instructions our review judged stale were excised rather than fixed (below).
- **Security review:** every fenced Verify command performs read-only HTTP fetches against the domain under audit — none contacts a third-party endpoint — and the only local write is the generated report. Retained base guidance does involve third parties when followed: the `site:` operator estimate in 2.5 queries a search engine, and 4.4 configures Bing Webmaster Tools. The AI-crawler user-agent comparison in Category 1's Verify block sends a bot user-agent string to the audited site as a diagnostic — run it only against sites you are authorized to audit.
- **Excised (2):** the 4.4 instruction to configure URL parameters in Google Search Console (the tool it named is retired and the step cannot be executed; the Bing half is kept) and the Rendertron entry in Category 7's SSR-solutions table (archived upstream; Prerender.io remains). Beyond these, the base carries no retired-schema recommendations, no llms.txt scoring, and no promotional insertions; the guards in ## Era exist to keep those category-wide failure modes out of audit reports, not to correct ones that were present here.
- **Grafts:** none. This is a single-source derivative.

## Attribution

- Base: `zubair-trabzada/geo-seo-claude/geo-technical` — MIT License. This document is a derivative work: the audit structure, category rubrics, scoring tables, restraint rules, and report format originate there. The Conditions and Era sections, the inline Verify blocks, and the report template's Era Notes are additions made for the SkillFed domesticated collection.
- This derivative is published under the MIT License.
