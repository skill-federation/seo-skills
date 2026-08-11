---
name: seo-validate
description: >-
  Repo-reading pre-ship SEO audit for source code: detects the framework
  first, then applies framework-conditioned rules with severity and
  definitive-vs-heuristic confidence labels; strictly read-only. Reach for it
  when the pages to check live in a codebase rather than behind a live URL.
  Era-adjudicated 2026: retired FAQ/HowTo rich-result guidance excised, GEO
  checks demoted to hypothesis.
slug: seo-validate
treatment: derivative
source_minibatch: 940
derived_from:
  - id: softspark/ai-toolkit/seo-validate
    role: base
    license_at_derivation: Apache-2.0
    content_hash_at_derivation: 0f350ff0a8d9945b9be7fd2aeba22491135813a31b21006a03d46a5d05e336c3
files:
  - path: reference/w3c-guidelines.md
    sha256: ec5dd3b7356bd80129fbb62592914b2d448c0b84549b7c995388ee85ce1158cb
    source_url: https://raw.githubusercontent.com/softspark/ai-toolkit/HEAD/app/skills/seo-validate/reference/w3c-guidelines.md
    from_skill_id: softspark/ai-toolkit/seo-validate
    license: Apache-2.0
    fetched_at: 2026-08-10
  - path: reference/core-web-vitals.md
    sha256: 3a5db2c3519899098ba85f44f67de0371e57f8d46300cec0dd92203ab36bdcf1
    source_url: https://raw.githubusercontent.com/softspark/ai-toolkit/HEAD/app/skills/seo-validate/reference/core-web-vitals.md
    from_skill_id: softspark/ai-toolkit/seo-validate
    license: Apache-2.0
    fetched_at: 2026-08-10
  - path: reference/spa-ssg-patterns.md
    sha256: 8271f0c3fcb9e52eb368f28b74e9975ba28d1f0fb8d9a72881eb62ad85962eb6
    source_url: https://raw.githubusercontent.com/softspark/ai-toolkit/HEAD/app/skills/seo-validate/reference/spa-ssg-patterns.md
    from_skill_id: softspark/ai-toolkit/seo-validate
    license: Apache-2.0
    fetched_at: 2026-08-10
  - path: scripts/seo-scanner.py
    sha256: 58fd4f2ed646e1f567f1e59e43296f48ff506bf62d733c27a286881cc540d94b
    source_url: https://raw.githubusercontent.com/softspark/ai-toolkit/HEAD/app/skills/seo-validate/scripts/seo-scanner.py
    from_skill_id: softspark/ai-toolkit/seo-validate
    license: Apache-2.0
    fetched_at: 2026-08-10
targeted_version: "softspark/ai-toolkit seo-validate @ HEAD, fetched 2026-08-10"
era_pins:
  - "Google retired FAQ rich results for every site on 2026-05-07"
  - "HowTo has been deprecated since September 2023"
  - "roughly 0.015% adoption with no vendor confirmation"
  - "chunking content for AI is the exact practice Google names as a mistake"
last_verified_at: 2026-08-10
license: Apache-2.0
needles:
  present:
    - "Google retired FAQ rich results for every site on 2026-05-07"
    - "HowTo has been deprecated since September 2023"
    - "roughly 0.015% adoption with no vendor confirmation"
    - "chunking content for AI is the exact practice Google names as a mistake"
    - 'Above-the-fold `<img loading="lazy">`'
    - "Never modify any files"
    - "read as a hypothesis, never a checklist"
    - "Never recommend adding FAQPage or HowTo for Google benefit"
    - "whether it also affects AI Overviews inclusion is unverified"
    - "a green scanner exit is not a pass on them"
  absent:
    - "FAQ rich result needs Q&A pairs"
    - "Highly extractable by LLMs"
    - "AI cannot extract cleanly"
    - "Each section must be a self-contained answer unit"
    - "Gemini training (NOT AI Overviews)"
dropped:
  - needle: "reference/schema-types.md ('Triggers rich FAQ results in SERP.'; HowTo listed among rich-result-eligible types)"
    reason: >-
      Era-stale reference file excluded from the vendored set: vendoring it
      unmodified would reimport retired rich-result guidance (FAQ retired for
      every site 2026-05-07; HowTo deprecated September 2023). The still-valid
      type coverage - the required-property matrix plus Event, WebSite/
      SearchAction, Recipe and VideoObject notes and the common-mistake items
      - is folded into Category 3; the full JSON-LD templates are not carried
      (author against validator.schema.org).
  - needle: "reference/geo-aeo-patterns.md ('FAQPage is the highest-precision signal'; HowTo schema pattern checks; 'llms.txt present at domain root' checklist)"
    reason: >-
      Era-stale reference file excluded: treats FAQPage and HowTo as live
      answer-engine options and instructs standing up llms.txt, all on the
      wrong side of the 2026 era facts stated in ## Era. Its era-clean
      robots.txt AI-crawler directives (the User-agent table and the
      Googlebot/Google-Extended caution) are folded into Category 8.
  - needle: "reference/geo-guidelines.md ('The 375-word rule'; 'Pair with HowTo schema for critical procedures')"
    reason: >-
      Era-stale reference file excluded: teaches chunking-for-AI as a rule and
      HowTo as a live pairing. Chunking for AI is the practice Google names as
      a mistake; corrected guidance lives in Category 6 of the body. Its
      era-clean native details/summary DOM-visibility exemption is folded
      into the Category 6 hidden-content row.
  - needle: "reference/content-citability.md ('Each H2 section should stay within ~375 words. If a section exceeds this, split with an H3 sub-heading')"
    reason: >-
      Era-stale reference file excluded: its chunk-architecture section
      teaches restructuring content to a claimed 500-token retrieval window as
      a rule. Demoted to hypothesis in Category 6 instead of vendored.
  - needle: "reference/ai-pipeline.md (format-routing table maps 'how to X' queries to HowTo and persona queries to FAQPage; chunk-position targeting strategy)"
    reason: >-
      Era-stale reference file excluded: routes queries to retired/deprecated
      schema types as live signals and teaches chunk-position targeting;
      single uncorroborated agency source throughout.
  - needle: "Pattern: CSR-only React app (Vite) with no prerender plugin"
    reason: >-
      Excuses the Output Format template block, which is carried in full with
      two anchor corrections: the base's sample findings point their See:
      lines at headings that do not exist in its own reference files;
      corrected to the real headings (#above-the-fold-heuristics,
      #prerendering-strategies-for-spas). Pre-existing base defect.
  - needle: "$ARGUMENTS harness macro and original command frontmatter (user-invocable, argument-hint, allowed-tools, agent)"
    reason: >-
      Not portable into the domesticated-skill frontmatter model; the CLI
      flags the macro carried are documented verbatim under ## Usage.
findings:
  defects_fixed:
    - "Category 3 FAQPage row demoted WARN to INFO and re-dated: structural validation of existing markup only, reported as informational (FAQ rich results retired for every site 2026-05-07)"
    - "Category 6 chunking row demoted WARN to INFO and stripped of its restructure-for-AI imperative; the whole GEO category demoted to hypothesis tier, read as hypothesis never checklist"
    - "Category 6 add-FAQPage recommendation row replaced with an informational existing-FAQPage/HowTo flag; recommending either for Google benefit is now explicitly forbidden"
    - "Category 10 AI-signal rationale (Gecko, Blyskall figures, AI-citation rates) conditioned to the same hypothesis tier; the structural link checks stay load-bearing"
    - "Vendored scanner's llms.txt INFO finding era-conditioned in the body: informational-only, never a recommended fix (roughly 0.015% adoption, no vendor confirmation)"
    - "Top summary, Rules, and Usage scopes re-labeled so GEO output can never be read as a checklist; new rule bullet forbids recommending retired rich-result schema"
    - "Era-clean AI-crawler robots.txt directives recovered from the excluded AEO reference and folded into Category 8 (User-agent table; blocking Googlebot blocks AI Overviews - Google-Extended is the Gemini-training opt-out, its effect on AI Overviews inclusion unverified per the Stage 2.5 bundle adjudication) with two new intent-check rows"
    - "Remaining clean schema-type coverage folded into Category 3 (Event, WebSite/SearchAction, Recipe, VideoObject, case-sensitive @type, no fabricated ratings); native details/summary DOM-visibility exemption restored in the Category 6 hidden-content row"
    - "Two dead anchor fragments in the sample report corrected to real headings (#above-the-fold-heuristics, #prerendering-strategies-for-spas) - pre-existing base defect"
  security_findings:
    - "Editorial review of scripts/seo-scanner.py (19,211 bytes): Python stdlib only, filesystem reads only, no network egress, no file writes, no subprocess use; exit codes 0 (clean), 1 (HIGH findings), 2 (bad path). Consistent with the document's read-only contract."
  excised:
    - "reference/schema-types.md - presents FAQ rich results as live SERP features and HowTo as rich-result-eligible"
    - "reference/geo-aeo-patterns.md - FAQPage as highest-precision answer-engine signal, HowTo pattern checks, llms.txt-at-domain-root checklist"
    - "reference/geo-guidelines.md - 375-word chunk checklist and pair-with-HowTo instruction"
    - "reference/content-citability.md - chunk-architecture rules (keep H2 under ~375 words, split with an H3)"
    - "reference/ai-pipeline.md - routes how-to queries to HowTo and persona queries to FAQPage; chunk-position targeting"
    - "Original harness frontmatter and the $ARGUMENTS macro (flags documented under Usage)"
  grafts: []
license_notes:
  - >-
    softspark/ai-toolkit/seo-validate: repo and skill license Apache-2.0; the
    SKILL.md body carries no embedded license declaration. The vendored
    scripts/seo-scanner.py header declares 'SPDX-License-Identifier:
    Apache-2.0' (Copyright 2024-2026 Lukasz Krzemien), agreeing with the repo
    license - no doc-level conflict.
---

# seo-validate — SEO Validation Scanner (domesticated derivative)

Scan a codebase for SEO issues using pattern-matching heuristics. Detects W3C/HTML violations, meta tag gaps, structured data problems, hreflang errors, Core Web Vitals risks (LCP/INP/CLS), resource-hint misuse, above-the-fold anti-patterns, GEO signals (hypothesis tier — hedging language, decision frameworks, semantic triples, freshness; see Category 6), topical authority gaps (pillar/cluster structure, orphan pages, cannibalization), SPA/CSR/SSG crawlability problems, technical SEO misconfigurations, and accessibility-for-SEO issues. Read-only — never modifies files.

**Standards basis**: W3C HTML5 Recommendation, W3C WCAG 2.2, Schema.org vocabulary, IETF RFC 5646 (BCP 47 language tags) for hreflang, web.dev Core Web Vitals thresholds (LCP <2.5s, INP <200ms, CLS <0.1), Google Search Central crawlability guidelines. GEO (Generative Engine Optimization) material is hypothesis-tier and era-adjudicated — see ## Era.

## Conditions

### When to use

- The pages you need to audit live in a repository — framework projects (Next.js, Nuxt, Astro, Gatsby, SvelteKit, Remix, Angular, Vue/React SPAs) or plain static HTML — and you want SEO defects surfaced **before** anything ships.
- Pre-merge or CI gating: `--output json` plus the exit-code contract (non-zero on HIGH findings) makes this usable as a blocking check.
- Migration audits: `--scope rendering` isolates the SPA/CSR/SSG crawlability category when you are moving a client-rendered app toward SSR/SSG.
- You want findings with file paths, line numbers, severity, and an honest `definitive` vs `heuristic` confidence label rather than an unqualified score.

### When NOT to use

- The target is a **live URL** rather than a repo checkout. This skill never fetches anything; use a crawling audit for deployed sites.
- You need runtime truth: real Core Web Vitals field data, server response headers, redirect chains, rendered-DOM comparisons. Static source analysis cannot see what only exists at runtime.
- You expect fixes to be applied. The contract is read-only: it reports, it never edits.
- The codebase is not a web frontend (APIs, CLIs, libraries) — there is nothing for the rules to bind to.

### Prerequisites

- A local checkout of the project (the scan roots itself at `.git` or `package.json`).
- Agent tool access to Read, Grep, Glob, and Bash.
- Python 3 for the vendored mechanical scanner (`scripts/seo-scanner.py` — stdlib only, no packages to install).
- `package.json` for framework detection; without it, detection falls back to `static` and framework-specific rules stay silent.

### What breaks first

- **Framework detection on monorepos and unusual layouts** — the wrong `package.json` wins and the wrong rule set is applied. Verify detection (Step 1) before trusting framework-specific findings.
- **Above-the-fold inference** — always heuristic; hero-component naming conventions and first-image position are proxies, so expect false positives on unconventional layouts.
- **Anything injected at runtime** — meta tags set by an edge function or CMS at request time look "missing" to a static scan. Confirm against the deployed page before filing.
- **The GEO category read as a checklist** — it is era-adjudicated to hypothesis tier (see ## Era); treating its output as required fixes is the failure mode this derivative exists to prevent.

## Era

This derivative targets softspark/ai-toolkit `seo-validate` at HEAD as fetched 2026-08-10 (content hash `0f350ff0a8d9…e336c3`; see ## Attribution). Its framework material targets the ecosystem the base and its vendored references describe: Next.js 13+ App Router era, Angular 17+ SSR via `@angular/ssr`, CRA deprecated. Dated facts this document is pinned to:

- **2026-05-07** — Google retired FAQ rich results for every site on 2026-05-07 (they had been restricted to authoritative government and health sites since August 2023, per the upstream schema reference). **September 2023** — HowTo has been deprecated since September 2023; Google stopped showing HowTo rich results. Consequence, enforced throughout this document: **Never recommend adding FAQPage or HowTo for Google benefit; flag existing markup as informational.**
- **llms.txt (2026)** — still a proposed convention at roughly 0.015% adoption with no vendor confirmation that any major AI engine reads it. Any llms.txt signal — including the vendored scanner's INFO finding — is informational-only, never a recommended fix.
- **Chunking (2026 editorial adjudication, batch 940)** — the upstream GEO category argued from a claimed ≤500-token retrieval window that long H2 sections are defects to restructure. That claim traces to a single agency source, and chunking content for AI is the exact practice Google names as a mistake. The entire GEO category is therefore demoted: its output is read as a hypothesis, never a checklist.
- **April 2022** — Google deprecated the Search Console URL Parameters tool; canonical tags, `robots.txt` rules, and `noindex` are the remaining parameter-handling signals (retained from the base, Category 8).

## Usage

```
/seo-validate                                # Scan full project, auto-detect framework
/seo-validate src/                           # Scan specific path
/seo-validate --scope rendering              # Only SPA/CSR/SSG crawlability checks
/seo-validate --scope performance            # Only Core Web Vitals static signals
/seo-validate --scope geo                    # Only GEO (Generative Engine Optimization)
/seo-validate --scope topical               # Only topical authority and cluster architecture
/seo-validate --severity high                # Filter to HIGH findings only
/seo-validate --framework next               # Force framework (skip auto-detection)
/seo-validate --rendering csr                # Force rendering-mode interpretation
/seo-validate --output json                  # Structured JSON output for CI integration
```

**Scopes:**
- `full` (default) — all 10 categories
- `technical` — HTML semantics, hreflang, CWV, rendering, technical SEO (categories 1, 4, 5, 7, 8)
- `content` — meta/OG, structured data, GEO, a11y-for-SEO (categories 2, 3, 6, 9)
- `performance` — only CWV static signals (category 5)
- `geo` — only GEO / citability checks (category 6; hypothesis tier — see ## Era)
- `rendering` — only category 7 (SPA/CSR/SSG crawlability) — useful for migration audits
- `topical` — only topical authority and cluster architecture (category 10)

**Severity filtering:** `--severity high` shows only HIGH, `--severity warn` shows HIGH+WARN, `--severity info` shows all. Default: all.

## What This Command Does

1. **Detect framework and rendering mode** from `package.json`, config files, and entry HTML.
2. **Scan the codebase** using `Grep`/`Glob`/`Read` against framework-aware patterns for each category in scope.
3. **Interpret findings** with specific fix suggestions tied to the detected framework.
4. **Report** findings with file paths, line numbers, severity, confidence, and standards citations.

## Steps

### Step 1: Detect Framework & Rendering Mode

Run detection before scanning so category patterns can adapt. Detection order:

1. **Read `package.json`** (if present) and inspect `dependencies` + `devDependencies`:

| Deps contain | Framework | Default rendering |
|--------------|-----------|-------------------|
| `next` | `next` | hybrid (per-route) |
| `nuxt` | `nuxt` | ssr |
| `astro` | `astro` | ssg |
| `gatsby` | `gatsby` | ssg |
| `@sveltejs/kit` | `sveltekit` | hybrid |
| `@remix-run/*` | `remix` | ssr |
| `@angular/core` + `@angular/ssr` or `@nguniversal/*` | `angular` | ssr |
| `@angular/core` alone | `angular` | csr (flag as SPA) |
| `vue` + `nuxt` | see nuxt row | — |
| `vue` without `nuxt` | `vue` | csr (flag as SPA) |
| `react` + `vite` without Next/Remix | `vite-spa` | csr (flag as SPA) |
| `react-scripts` | `cra` | csr (flag as SPA) |
| no `package.json` OR no framework deps | `static` | static |

2. **Read config files** to refine:
   - `next.config.*` — check `output: 'export'` (forces SSG), `images`, i18n settings.
   - `nuxt.config.*` — check `ssr: false`, `generate` blocks (SSG export).
   - `astro.config.*` — check `output: 'server'|'static'|'hybrid'` and `prerender` directives.
   - `gatsby-config.*` — plugin list (`gatsby-plugin-react-helmet`, `gatsby-plugin-sitemap`).
   - `svelte.config.*` — adapter choice (`static`, `node`, `vercel`).
   - `vite.config.*` + `package.json` scripts — look for `vite-plugin-ssr`, `vite-plugin-prerender`.
   - `angular.json` — look for SSR builder config.

3. **Read entry HTML** (`public/index.html`, `index.html`, `app/layout.tsx`, `src/app.html`, etc.) to confirm whether meaningful content is prerendered or only a mount point (`<div id="root"></div>`).

4. **Override precedence**: `--framework` and `--rendering` flags override detection.

Report the detected framework and rendering mode in the Summary table.

### Verify

Prove the detection before any framework-specific rule fires:

```bash
# The framework you detected must actually be in the dependency manifest:
grep -nE '"(next|nuxt|astro|gatsby|@sveltejs/kit|@remix-run/[a-z-]+|@angular/(core|ssr)|react-scripts|react|vite)"' package.json

# And the rendering call must match what the entry HTML really prerenders
# (a bare mount div with no content inside means CSR; 2>/dev/null silences
# the candidates that don't exist in this project):
grep -nE '<div id="(root|app|__next)">' index.html public/index.html src/app.html 2>/dev/null
```

If the grep contradicts the detection (for example, `next` present but you classified `static`), redo Step 1 — every framework-conditioned finding downstream depends on it.

### Step 2: Run Category Scans

For each category in `--scope`, apply the pattern set below using `Grep` (for regex across files) and `Read` (for config parsing / ordered checks). Patterns are framework-aware — use the framework detected in Step 1 to select the right rule set.

### Verify

Cross-check the manual scan with the vendored mechanical scanner:

```bash
# Interface: seo-scanner.py [path] [--output json|text]
# Exit codes: 0 = no HIGH findings, 1 = HIGH findings exist, 2 = path does not exist.
python scripts/seo-scanner.py . --output json
```

The script is a stdlib-only standalone subset of this document's rules — it checks meta tags, heading hierarchy, image `alt`, JSON-LD presence, lazy-loading/script-in-head CWV signals, hreflang (when i18n is detected), `robots.txt`, sitemap, and `llms.txt` presence. Reconciliation rules:

- Every HIGH the script reports must appear in your findings or be explicitly dismissed as a scanner false positive (with the evidence).
- Your manual scan should be a superset of the script's; the reverse is not true. If the script found something you missed, your category pass was incomplete — rescan that category.
- The script's `llms.txt` finding is INFO and its message wording ("recommended for Generative Engine Optimization") predates this derivative's era review — per ## Era, report it as informational-only, never as a fix.

CI wiring and the gate's honest scope. The invocation above is written from the skill's own directory — `scripts/seo-scanner.py` is relative to where this skill is installed, not to the repo being scanned. In CI, where the job's cwd is the audited repo checkout, resolve the scanner absolutely:

```bash
# CI step (any runner); blocking because exit code 1 on HIGH findings fails the job
SKILL_DIR=/path/to/installed/seo-validate    # wherever this skill's files are installed
python "$SKILL_DIR/scripts/seo-scanner.py" . --output json
```

That exit-code gate enforces the scanner's standalone subset only. The framework-conditioned rules in the category tables — the Next.js `generateMetadata`, `dynamic(..., { ssr: false })`, and `'use client'` rows a Next.js migration audit typically cares about — run in the agent layer and are not enforced by the scanner's exit code: a green scanner exit is not a pass on them. To gate those too, run the full skill through an agent step and fail the pipeline on its HIGH findings.

### Step 3: Interpret and Enrich

For each finding:

1. **Read the flagged file/lines** to confirm the match is real (not a comment, not a type-only reference).
2. **Add a specific fix** tied to the framework (e.g., "use `next/image` with `priority` prop" vs. "add `<link rel="preload" as="image">` to `<head>`").
3. **Mark confidence**: `definitive` for regex matches against known-bad patterns, `heuristic` for co-occurrence / absence checks.
4. **Skip false positives** when context shows the concern is addressed elsewhere (e.g., meta tags set in a layout file the route inherits from).

### Step 4: Report

Present findings sorted by severity (HIGH → WARN → INFO), then by file path.

### Verify

Two closing checks — one on the contract, one on the report itself:

```bash
# 1) Read-only contract: the scan must leave the working tree untouched.
git status --porcelain 2>/dev/null \
  || echo "not a git checkout - verify instead that source file mtimes predate the scan"
# Expect: no modified tracked files. Any modification means the contract was broken.

# 2) Report hygiene: no finding may recommend adding retired rich-result schema.
grep -inE "(add|create|implement|introduce)[^.]{0,60}(FAQPage|HowTo)" seo-report.md \
  | grep -viE "(never|not |avoid|refuse|forbid|retired|deprecated|informational)" \
  && echo "REVIEW: possible retired-schema recommendation - read each hit in context" \
  || echo "PASS"
# (substitute seo-report.md with whatever report artifact you produced)
```

The report-hygiene grep is an attention hook, not a gate: the second filter drops compliant negative sentences ("do not add FAQPage…"), but phrasing varies — read any surviving hit in context, and remember passive recommendations ("FAQPage should be added") also count as violations even if a pattern misses them.

---

## Scanner Reference

### Category 1: HTML Semantics & W3C

Scan HTML/JSX/Vue/Svelte/Astro templates for W3C HTML5 compliance.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| `<html>` without `lang` attribute | HIGH | definitive | HTML5 §3.2.6 — `lang` required for SEO + a11y |
| Missing `<meta charset="utf-8">` in `<head>` | HIGH | definitive | HTML5 §4.2.5.5 — required first |
| Missing `<meta name="viewport">` | HIGH | definitive | Mobile-first indexing requires viewport |
| Multiple `<h1>` per page/route component | WARN | heuristic | One H1 per document is standard SEO practice |
| No `<h1>` in page component | WARN | heuristic | Every indexable page should have H1 |
| Heading level skip (h1 → h3) | WARN | heuristic | Document outline breaks assistive tech + crawlers |
| Missing landmarks (`<main>`, `<nav>`, `<header>`, `<footer>`) | WARN | heuristic | Semantic HTML aids both a11y and crawlers |
| Missing `<!DOCTYPE html>` | HIGH | definitive | Triggers quirks mode in older browsers |

See: [reference/w3c-guidelines.md](reference/w3c-guidelines.md)

---

### Category 2: Meta & Open Graph

Check `<head>` composition in entry HTML, framework metadata exports, and route-level metadata.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Missing `<title>` / framework title | HIGH | definitive | Required for SERP display |
| `<title>` >60 chars OR <10 chars | WARN | definitive | Recommended 50–60 char range |
| Missing `<meta name="description">` | HIGH | definitive | Required for SERP snippets |
| Description >160 chars OR <50 chars | WARN | definitive | Recommended 150–160 char range |
| Missing `<link rel="canonical">` on indexable pages | HIGH | definitive | Prevents duplicate-content dilution |
| `<meta name="robots" content="noindex">` on production route | WARN | heuristic | Confirm intentional — blocks indexing |
| Missing OG tags: `og:title`, `og:description`, `og:image`, `og:url`, `og:type` | WARN | definitive | Required for rich social cards |
| Missing Twitter Card (`twitter:card`) | WARN | definitive | Required for Twitter/X rich previews |
| OG image without absolute URL | WARN | definitive | OG spec requires absolute URLs |

**Framework adapters**:
- **Next.js App Router**: look for `export const metadata = { ... }` or `generateMetadata()` in `layout.tsx`/`page.tsx`.
- **Next.js Pages Router**: look for `<Head>` from `next/head`.
- **Nuxt**: look for `useHead()` / `definePageMeta({ title, ... })`.
- **Astro**: look for `<BaseHead>` component or direct `<meta>` in layout.
- **Gatsby**: look for `<Helmet>` from `react-helmet`.
- **SvelteKit**: look for `<svelte:head>` blocks.
- **SPAs (Vue/Vite/CRA/Angular)**: look for `react-helmet-async`, `vue-meta`, `@angular/platform-browser`'s `Meta`/`Title` services. Flag runtime-only meta as a rendering-crawlability issue (Category 7).

---

### Category 3: Structured Data / Schema.org

Scan for JSON-LD (`<script type="application/ld+json">`) presence and correctness on key page types.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| No JSON-LD on article/blog route | WARN | heuristic | `Article` schema improves rich results |
| JSON-LD missing `@context` | HIGH | definitive | Must be `https://schema.org` |
| JSON-LD missing `@type` | HIGH | definitive | Type declaration is required |
| `Article` missing `headline` / `author` / `datePublished` | WARN | definitive | Required properties per schema.org |
| `FAQPage` present but missing `mainEntity` array | INFO | definitive | Malformed markup — validate structure only. FAQ rich results are retired (2026-05-07); report as informational, never as a rich-result opportunity |
| `BreadcrumbList` missing `itemListElement` | WARN | definitive | Breadcrumb rich result needs list |
| `Organization` missing `name` / `url` / `logo` | WARN | definitive | Knowledge Graph signals |
| `Product` missing `name` / `offers` / `aggregateRating` | WARN | definitive | Product rich results |
| `LocalBusiness` missing `address` / `telephone` / `openingHours` | WARN | definitive | Local SEO signals |

**Required properties per type** (folded from the upstream schema reference, era-corrected):

- `Article` — required: `headline`, `author`, `datePublished`, `image`; strongly recommended: `dateModified`, `publisher`, `mainEntityOfPage`. Subtypes: `NewsArticle`, `BlogPosting`, `TechArticle`.
- `BreadcrumbList` — `itemListElement` array with `position` + `name` (+ `item` on every entry except the last, which is the current page).
- `Organization` — `name`, `url`, `logo`; `sameAs` recommended for Knowledge Graph disambiguation.
- `Product` — `name`, `image`, `offers` (with `price`, `priceCurrency`, `availability`); `aggregateRating`, `review`, `brand` recommended for rich results.
- `LocalBusiness` — `name`, `address`, `telephone`; `openingHoursSpecification`, `geo`, `url`, `image` recommended. Prefer specific subtypes (`Restaurant`, `Store`, …).
- `Event` — `name`, `startDate`, `location` (or `eventAttendanceMode: OnlineEventAttendanceMode`).
- `WebSite` — with a `SearchAction` under `potentialAction` to enable the sitelinks search box. `Recipe` and `VideoObject` are also covered upstream; author their key fields per schema.org. The full JSON-LD templates are not carried here — build against https://validator.schema.org/.
- All types — `@context` must be `https://schema.org`, `@type` values are case-sensitive (`article` is invalid; must be `Article`), dates in ISO 8601, URLs absolute, and markup must match visible content (duplicate conflicting JSON-LD blocks are a defect). Fake reviews or fabricated `aggregateRating` values violate Google guidelines — flag, never suggest.
- `FAQPage` / `HowTo` — **validated structurally when already present, reported as informational.** Google retired FAQ rich results for every site on 2026-05-07, and HowTo has been deprecated since September 2023. Never recommend adding FAQPage or HowTo for Google benefit.

Validate candidates against https://validator.schema.org/ and the Google Rich Results Test.

---

### Category 4: Hreflang & i18n

Scan all locale variants for hreflang correctness.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Hreflang pair not bidirectional (A→B but not B→A) | HIGH | definitive | Google ignores unidirectional hreflang |
| Missing `hreflang="x-default"` | WARN | definitive | Fallback required for unmatched locales |
| Missing self-referencing hreflang tag | WARN | definitive | Each version must reference itself |
| Invalid BCP 47 code (e.g., `en_US` instead of `en-US`) | HIGH | definitive | RFC 5646 requires hyphen-separated subtags |
| Unknown language code (not ISO 639-1) | HIGH | definitive | Invalid language subtag |
| Unknown region code (not ISO 3166-1 alpha-2) | HIGH | definitive | Invalid region subtag |
| Hreflang points to URL returning canonical to different URL | WARN | heuristic | Canonical must match hreflang target |

---

### Category 5: Core Web Vitals (Static Signals)

Detect code patterns that cause CWV regressions. Covers LCP, INP, CLS, resource hints, and above-the-fold optimization.

#### 5a. LCP (Largest Contentful Paint, target <2.5s)

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| `<img>` without `width`/`height` attributes | HIGH | definitive | Causes CLS + delays LCP |
| Above-the-fold `<img>` without `fetchpriority="high"` (or framework equivalent) | HIGH | heuristic | LCP image must be prioritized |
| Above-the-fold `<img loading="lazy">` | HIGH | definitive | Actively harmful — delays LCP |
| `@font-face` without `font-display` | HIGH | definitive | Blocks text paint |
| Missing `<link rel="preload" as="image">` for known hero image | WARN | heuristic | Preload accelerates LCP |
| Missing `<link rel="preload" as="font" crossorigin>` for self-hosted webfonts | WARN | heuristic | Fonts are a common LCP blocker |
| Missing `<link rel="preconnect">` for 3rd-party font/image/CDN origins on critical path | WARN | heuristic | Saves ~100–300ms per origin |
| Render-blocking `<link rel="stylesheet">` without `media` split or critical-inline | WARN | heuristic | Blocks first paint |
| Responsive image: `<img>` >600px without `srcset`+`sizes` or `<picture>` | WARN | heuristic | Over-fetches on mobile |
| **Next.js**: `<img>` used instead of `next/image` in route component | WARN | definitive | Misses automatic optimization |
| **Next.js**: `next/image` without `priority` on detected LCP element | HIGH | heuristic | LCP will under-perform |
| **Nuxt**: `<img>` instead of `<NuxtImg>`/`<NuxtPicture>` | WARN | definitive | Misses auto-optimization |
| **Astro**: `<img>` instead of `<Image>` from `astro:assets` | WARN | definitive | Misses auto-optimization |
| **Gatsby**: `<img>` instead of `GatsbyImage` | WARN | definitive | Misses auto-optimization |

#### 5b. INP (Interaction to Next Paint, target <200ms)

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| `<script>` in `<head>` without `async`/`defer` | HIGH | definitive | Render-blocking |
| Third-party analytics/chat/ads without `async`/`defer` or framework lazy strategy | WARN | definitive | Blocks main thread |
| `document.write` usage | HIGH | definitive | Blocks parser; disabled by modern browsers |
| Heavy top-level `useEffect(() => {...}, [])` (many sync calls) | WARN | heuristic | Long tasks delay INP |
| Client bundle estimated >300KB gzipped gating interaction | WARN | heuristic | Excessive JS delays hydration + INP |
| **Next.js**: `<Script>` without `strategy` prop on non-critical scripts | WARN | definitive | Defaults to `afterInteractive` — often not optimal |
| Missing `fetchpriority="low"` on deferrable below-the-fold resources | INFO | heuristic | Helps browser prioritize LCP |

#### 5c. CLS (Cumulative Layout Shift, target <0.1)

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Images without `width`/`height` or `aspect-ratio` CSS | HIGH | definitive | Primary CLS cause |
| Iframes (YouTube/maps/ads) without dimensions or aspect-ratio | HIGH | definitive | Embeds shift layout |
| Dynamically injected ads/embeds without reserved placeholder space | WARN | heuristic | Shifts layout on load |
| `@font-face` without `font-display: swap`/`optional` | WARN | definitive | FOIT/FOUT shifts |
| SSR hydration mismatch: `typeof window` branches rendering different content | WARN | heuristic | Hydration-triggered shift |
| Skeleton → content of different height | WARN | heuristic | Load-state shift |

#### 5d. Resource Hints & Route Prefetching

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| `<link rel="preload">` for non-critical resource | WARN | heuristic | Wastes bandwidth + contention |
| Next-route not prefetched when framework supports it (Next `<Link>`, Nuxt `<NuxtLink>`, SvelteKit `data-sveltekit-preload-data`) | INFO | heuristic | Hurts soft-navigation UX |
| External origin referenced in critical path without `<link rel="preconnect">` | WARN | definitive | Adds 100–300ms per origin |
| Less-critical external origin without `<link rel="dns-prefetch">` | INFO | heuristic | Lightweight fallback |
| ESM chunks on critical path without `<link rel="modulepreload">` | INFO | heuristic | Helps browser parse ahead |
| `<link rel="preload">` appears AFTER resource that uses it in document order | WARN | heuristic | Preload must come first to help |
| >6 `<link rel="preload">` directives on one page | WARN | heuristic | Over-hinting — browsers throttle |

#### 5e. Above-the-Fold Heuristic

"Above-the-fold" candidates (confidence: heuristic):
- First `<img>` / `<Image>` / `<NuxtImg>` / `<Image from 'astro:assets'>` / `GatsbyImage` inside a page/route component.
- First child of `<main>` or `<section>`.
- Components named `Hero`, `Banner`, `Masthead`, `Jumbotron`, `HeroSection`, `CoverImage`.
- Images inside `<header>` that appear before any scroll-margin content.

Rules for ATF elements:
- MUST have explicit `width` + `height`.
- MUST have high priority (`fetchpriority="high"` or `priority` prop).
- MUST NOT have `loading="lazy"`.
- SHOULD have a matching `<link rel="preload">` entry.

Rules for below-the-fold:
- SHOULD have `loading="lazy"` + `decoding="async"`.
- MAY have `fetchpriority="low"`.

See: [reference/core-web-vitals.md](reference/core-web-vitals.md)

---

### Category 6: GEO (Generative Engine Optimization) — hypothesis tier

Content-structure signals for AI answer engines (ChatGPT, Perplexity, Google AI Overviews, Bing Copilot, Google AI Mode). **Every finding in this category is severity `INFO`, confidence `heuristic`, and the category's output is read as a hypothesis, never a checklist.** The load-bearing categories of this audit are HTML semantics, meta/OG, structured data, hreflang, and Core Web Vitals (Categories 1–5); run GEO for orientation, not for a punch list.

Two era adjudications (2026, batch 940 editorial review) govern this category:

- The upstream version argued from a claimed ≤500-token (~375-word) retrieval-chunk window that long H2 sections are defects to restructure. That claim traces to a single agency source, and restructuring pages to target AI retrieval windows is not a safe recommendation — chunking content for AI is the exact practice Google names as a mistake. The section-length row below is retained as an observation only; it carries no restructure instruction.
- Google retired FAQ rich results for every site on 2026-05-07, and HowTo has been deprecated since September 2023. **Never recommend adding FAQPage or HowTo for Google benefit; flag existing markup as informational.**

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Existing `FAQPage` or `HowTo` JSON-LD detected | INFO | heuristic | Informational only — retired/deprecated rich results (see above); validate structure via Category 3; do not recommend adding more for Google benefit |
| No `speakable` schema on summary content | INFO | heuristic | Voice/audio answer engines; unverified benefit |
| H2 section body exceeds ~375 words without an H3 sub-heading | INFO | heuristic | Hypothesis: derives from an unverified retrieval-window claim. Report as an observation; do not instruct a restructure |
| First paragraph under a heading exceeds 60 words before a concrete fact, number, or direct recommendation | INFO | heuristic | Front-loading answers is sound writing on its own merits; the AI-extraction rationale is hypothesis |
| Hedging language in recommendation or product context: "may be", "might be", "could be", "worth considering", "for many", "for most people" | INFO | heuristic | Declarative recommendations read better; the claimed citation-signal benefit is hypothesis |
| No decision framework ("if X → choose Y" / "for X, use Y") in guide or category content | INFO | heuristic | Useful structure on its own merits; the claimed AI-citation weighting is hypothesis |
| No contrast or comparison ("X vs Y", "unlike X", "in contrast to X") in content with comparative headings | INFO | heuristic | Same hypothesis tier as above |
| No negative definition ("not recommended for", "not suitable for", "avoid if") on product or category pages | INFO | heuristic | Same hypothesis tier as above |
| Author name uses generic placeholder: "Admin", "Team", "Staff", "Editor", or no author at all | INFO | heuristic | Named authorship is standard E-E-A-T practice; the specific suppression-rule claim is hypothesis |
| Author block contains fewer than 30 words of bio text near the author name | INFO | heuristic | Same hypothesis tier as above |
| Article `dateModified` (JSON-LD or `<time>`) is older than 13 weeks with no visible update notice | INFO | heuristic | The 13-week figure comes from a single uncorroborated study; treat as a freshness prompt, not a deadline |
| Missing explicit citation/source markup (`<cite>`, author bylines) | INFO | heuristic | Attributable sourcing is good practice; the claimed engine preference is hypothesis |
| No `<q>` or quote schema on quoted content | INFO | heuristic | Same hypothesis tier as above |
| No Q&A structure on how-to content | INFO | heuristic | Visible headings/Q&A structure only — never via FAQPage or HowTo schema for Google benefit |
| Heavy reliance on `<div>` over semantic HTML | INFO | heuristic | Semantic HTML is load-bearing in Category 1 regardless of any AI rationale |
| Key facts hidden behind JS interactions (tabs, accordions) | INFO | heuristic | Overlaps Category 7 rendering reality: non-rendering crawlers see the initial DOM only. Native `<details>`/`<summary>` is exempt — its content stays in the initial DOM, merely collapsed |

---

### Category 7: Rendering Mode & SPA/CSR/SSG Crawlability ⭐

**The most critical category for JS apps.** A CSR-only app with no prerendering is effectively invisible to most crawlers.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Entry HTML contains only mount point (`<div id="root">` or `<div id="app">`) with no prerendered content, and no SSR/SSG configured | HIGH | definitive | Crawlers see empty page |
| Meta/title set only in JS runtime (react-helmet-async, vue-meta, `document.title = ...`) with no SSR/SSG fallback | HIGH | definitive | Public routes won't have crawlable meta |
| `HashRouter` / hash-based routing (`/#/about`) on public routes | HIGH | definitive | Google ignores fragments for indexing |
| CSR app without `<noscript>` fallback containing meaningful content | WARN | heuristic | Minimum no-JS signal for crawlers |
| **Next.js**: `'use client'` at top of every page/layout forcing CSR | WARN | heuristic | Defeats SSR/SSG benefits |
| **Next.js**: Content page missing `generateMetadata` / static `metadata` export | WARN | heuristic | No crawlable metadata |
| **Next.js**: `dynamic(..., { ssr: false })` wrapping LCP / above-the-fold content | HIGH | definitive | Blocks both SSR and LCP |
| **Nuxt**: `ssr: false` in config or route with public content | WARN | heuristic | Disables SSR intentionally |
| **Astro**: `client:only` on hero/content components | WARN | heuristic | Component not prerendered |
| **SvelteKit**: `export const ssr = false` on public route | WARN | heuristic | Disables SSR |
| **Gatsby**: route excluded from prerender (`gatsby-plugin-exclude`) | WARN | heuristic | Verify intent |
| **Angular SPA**: project uses `@angular/core` without `@angular/ssr` or `@nguniversal/*` | HIGH | definitive | Default Angular is CSR-only |
| **Vue SPA / React SPA / CRA / Vite-SPA**: no prerender plugin detected (no `vite-plugin-ssr`, `react-snap`, `prerender-spa-plugin`, `vite-plugin-prerender`) | HIGH | definitive | Content invisible to crawlers |
| `suppressHydrationWarning` overuse (>3 occurrences) | WARN | heuristic | Masks real hydration mismatches |
| `typeof window !== 'undefined'` / `isBrowser` checks in render paths | WARN | heuristic | Often signals hydration mismatch |
| Static `robots.txt` references dynamic routes that aren't prerendered | WARN | heuristic | Crawlers hit empty pages |
| `prerender.io` / `rendertron` / dynamic-rendering middleware detected | INFO | definitive | Legacy pattern — Google now prefers SSR/SSG |

See: [reference/spa-ssg-patterns.md](reference/spa-ssg-patterns.md)

---

### Category 8: Technical SEO

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Missing `robots.txt` | HIGH | definitive | Blocks crawler directives + sitemap reference |
| `robots.txt` contains `Disallow: /` in production build | HIGH | definitive | Blocks entire site |
| Missing `sitemap.xml` / framework sitemap generator | HIGH | definitive | Slows discovery |
| `robots.txt` missing `Sitemap:` directive | WARN | definitive | Crawlers may not find sitemap |
| Canonical URLs inconsistent with actual deployed URLs | WARN | heuristic | Dilutes link equity |
| Canonical URL includes query params on parametrized pages (e.g., `?q=`, `?page=`, `?sort=`) | HIGH | heuristic | Canonical must point to clean base URL, not parametrized variant — else each query variant is a duplicate |
| Site has search feature (detected: `<input type="search">`, `<form action="/search">`, route `/search`, `?q=` / `?query=` / `?s=` / `?search=`) but `robots.txt` does NOT `Disallow` the search URL pattern | HIGH | heuristic | Parametrized search URLs create unlimited duplicate-content pages — crawl budget waste + index bloat |
| Site has faceted navigation (filters, sort params, pagination like `?filter=`, `?sort=`, `?page=`, `?color=`) without `robots.txt` Disallow rules OR parameter-handling via canonical | WARN | heuristic | Faceted URLs multiply indexable variants exponentially |
| Search result page (SRP) missing `<meta name="robots" content="noindex, follow">` | HIGH | heuristic | SRPs are thin/duplicate content per Google Search Essentials; indexing wastes crawl budget |
| Search result page missing self-referencing canonical OR canonical with dynamic query in it | WARN | heuristic | SRP should either canonical to clean `/search` or be noindexed entirely |
| Parametrized URLs (tracking: `utm_*`, `gclid`, `fbclid`, `ref=`) served without canonical to clean URL | HIGH | heuristic | Tracking params create duplicate URLs — canonical must strip them |
| Trailing-slash inconsistency (some pages `/about/`, some `/about`) | WARN | heuristic | Duplicate-content risk |
| HTTPS not enforced (hardcoded `http://` internal links) | WARN | definitive | Mixed-content + security |
| No 404 page / no custom `not-found` route | WARN | heuristic | Default 404s hurt UX |
| Meta `robots: noindex,nofollow` on indexable production routes | HIGH | heuristic | Blocks indexing — verify intent |
| `robots.txt` disallows `Googlebot` where the apparent intent is an AI opt-out | HIGH | heuristic | Blocking `Googlebot` blocks AI Overviews and organic indexing together; `Google-Extended` is the Gemini-training opt-out (see AI-crawler directives below) |
| `robots.txt` has no explicit AI-crawler `User-agent` rules | INFO | heuristic | Intent check, not a defect: absence means default-allow for AI training and retrieval bots — confirm that is deliberate |

**AI-crawler `robots.txt` directives** (folded from the upstream AEO reference — the era-clean part of an otherwise excluded file). Known AI crawler `User-agent` strings:

| Bot | Owner | Purpose |
|-----|-------|---------|
| `GPTBot` | OpenAI | ChatGPT training + search |
| `OAI-SearchBot` | OpenAI | ChatGPT Search real-time retrieval |
| `ClaudeBot` | Anthropic | Claude training |
| `anthropic-ai` | Anthropic | Claude real-time retrieval |
| `PerplexityBot` | Perplexity | Real-time answer grounding |
| `Google-Extended` | Google | Gemini training opt-out; effect on AI Overviews inclusion unverified |
| `Googlebot` | Google | Organic + AI Overviews |

Blocking `Googlebot` blocks AI Overviews. Blocking `Google-Extended` opts out of Gemini training; whether it also affects AI Overviews inclusion is unverified (2026-08-10, bundle adjudication). These directives are real, honored-by-policy `robots.txt` mechanics — unlike `llms.txt` (see ## Era), they carry no adoption caveat; the audit's job is to check that what the file allows or blocks matches the site owner's actual intent.

**Parameter-handling guidance**: Google deprecated the Search Console URL Parameters tool in April 2022. Today the only signals are:
1. **Canonical tags** — every parametrized variant must `<link rel="canonical">` to the clean base URL.
2. **`robots.txt` Disallow rules** — block crawlers from following parameter patterns entirely (`Disallow: /*?q=*`, `Disallow: /search?*`).
3. **`noindex` meta** — allow crawl (for link discovery) but prevent indexing on SRPs and thin faceted pages.

Choose ONE strategy per parameter type — mixing `Disallow` + `noindex` is contradictory (Disallow prevents crawler from ever seeing the noindex directive).

**Example `robots.txt` for a site with search**:
```
User-agent: *
Disallow: /search?*
Disallow: /*?q=*
Disallow: /*?query=*
Disallow: /*?s=*
Disallow: /*?utm_*
Disallow: /*?gclid=*
Disallow: /*?fbclid=*
Allow: /

Sitemap: https://example.com/sitemap.xml
```

**Example canonical on a parametrized page** (`/products?category=shoes&color=red&sort=price`):
```html
<link rel="canonical" href="https://example.com/products">
```

The canonical points to the clean page; the specific filter combination is a view, not a distinct URL.

---

### Category 9: Accessibility for SEO

Accessibility ↔ SEO overlap. WCAG compliance improves ranking signals.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| `<img>` missing `alt` attribute | WARN | definitive | WCAG 1.1.1 + image SEO |
| `<img alt="">` on informational image | WARN | heuristic | Empty alt only for decorative |
| Icon-only `<button>` without `aria-label` | WARN | definitive | Screen readers + semantic crawlers |
| Form `<input>` without associated `<label>` | WARN | definitive | WCAG 3.3.2 |
| `<div>` used for interactive element (click handler on `<div>`) | WARN | heuristic | Should be `<button>` or `<a>` |
| Link text is "click here" / "read more" | WARN | heuristic | Anchor text is a ranking signal |
| `<a>` without `href` (fake link) | WARN | definitive | Not crawlable |

---

### Category 10: Topical Authority & Cluster Architecture

Topical authority is the degree to which a domain is recognised as an expert source across an entire topic, not just individual pages. Classical SEO benefits are the load-bearing case here — Senuto's study of 212K phrases across 7,200 semantic groups showed topical coverage dominates top-10 rankings independently of individual technical metrics. Where a row below cites AI-retrieval rationale (Gecko embedding similarity, Blyskall citation-rate figures, Query Fan Out), that rationale is hypothesis-tier exactly as in Category 6; the underlying link-structure checks stand on classic crawl-budget and anchor-semantics grounds regardless.

| Pattern | Severity | Confidence | Description |
|---------|----------|------------|-------------|
| Long-form page (>800 words) has internal link density below 1 link per 800 characters of body text | WARN | heuristic | Google's internal linking guideline: ~1 contextual internal link per 800 chars; low density = weak cluster signal |
| Internal link uses generic anchor text: "click here", "read more", "here", "this page", "learn more" | WARN | definitive | Anchor text is a topical signal; descriptive claim-based anchors transfer semantic context to the linked page |
| Page >2,000 words with no outbound internal links to topically related pages | INFO | heuristic | Pillar pages must link out to cluster articles; absence breaks the pillar→cluster signal |
| Page has >500 words of indexable content with zero detected inbound internal links (orphan page) | WARN | heuristic | Orphan pages receive minimal crawl budget and no authority pass-through; every content page needs at least one inbound link |
| Content page URL slug contains numeric IDs, UUIDs, or is purely numeric (e.g., `/post/12345`, `/p/abc-uuid`) | WARN | heuristic | Natural-language slugs are better anchors and more readable; the +11.4% AI-citation figure attached upstream is hypothesis-tier |
| Two or more pages on the same domain target the same primary keyword in H1 and title | WARN | heuristic | Keyword cannibalization: pages compete against each other, diluting authority; consolidate into pillar + cluster |

**Topical authority strategy note:** the Query Fan Out claim — AI generating 50+ sub-queries per user question, 95% with zero Monthly Search Volume in any keyword tool — is hypothesis-tier, but pillar + cluster architecture is sound information architecture with or without it: it serves long-tail coverage that keyword tools under-report.

---

## Output Format

```markdown
## SEO Validation Report

### Summary
| Metric | Value |
|--------|-------|
| Scope | full / technical / content / performance / geo / rendering / topical |
| Framework detected | next / nuxt / astro / gatsby / sveltekit / remix / angular / vue / react-spa / vite-spa / cra / static |
| Rendering mode | csr / ssr / ssg / isr / hybrid |
| Files scanned | N |
| Public routes found | N |
| Routes with prerendering | N of N |
| Findings: HIGH | N |
| Findings: WARN | N |
| Findings: INFO | N |

### Findings

#### [HIGH] app/layout.tsx:12
Category: HTML Semantics & W3C
Confidence: definitive
Pattern: `<html>` element missing `lang` attribute
W3C Rule: HTML5 §3.2.6
Fix: Add `lang="en"` (or appropriate BCP 47 code) to the `<html>` element.
See: reference/w3c-guidelines.md#lang-attribute

#### [HIGH] components/HomeHero.tsx:24
Category: Core Web Vitals (LCP)
Confidence: definitive
Pattern: Above-the-fold `<img>` with `loading="lazy"`
Rule: LCP anti-pattern — lazy loading the LCP element delays it
Fix: Remove `loading="lazy"`, add `fetchpriority="high"`. For Next.js use `<Image priority />`.
See: reference/core-web-vitals.md#above-the-fold-heuristics

#### [HIGH] src/App.tsx:1
Category: Rendering Mode & SPA Crawlability
Confidence: definitive
Pattern: CSR-only React app (Vite) with no prerender plugin
Rule: Content-site SPAs without SSR/SSG are invisible to most crawlers
Fix: Add `vite-plugin-ssr` or migrate to Next.js/Remix; OR add `react-snap` for build-time prerender.
See: reference/spa-ssg-patterns.md#prerendering-strategies-for-spas
```

**Confidence values**:
- `definitive` — regex match against a known-bad pattern with high precision.
- `heuristic` — co-occurrence / absence / ordering / above-the-fold inference — may be false positive.

**Exit codes** (when `--output json`):
- `0` — no HIGH findings.
- `1` — one or more HIGH findings.
- `2` — the given path does not exist (matching the vendored scanner's contract in Step 2).

## Rules

- **Read-only**: Never modify any files. Report findings only.
- **Framework-aware**: Always detect framework first; apply the correct rule set.
- **Standards citation**: Every HIGH/WARN finding must cite a W3C/Schema.org/RFC/web.dev reference.
- **Skip non-source files**: Binary files, lock files (`package-lock.json`, `yarn.lock`, `pnpm-lock.yaml`), vendored directories (`node_modules/`, `vendor/`, `.git/`, `dist/`, `build/`, `out/`, `.next/`, `.nuxt/`, `.svelte-kit/`, `public/build/`).
- **No false confidence**: Label heuristic findings clearly; above-the-fold detection is always heuristic.
- **GEO severity**: All Category 6 findings are `INFO`, hypothesis tier — read as a hypothesis, never a checklist. Never raise GEO findings to HIGH.
- **Retired rich results**: Never recommend adding FAQPage or HowTo for Google benefit (FAQ retired for every site 2026-05-07; HowTo deprecated September 2023). Flag existing markup as informational.
- **SPA HIGH bar**: Only flag Category 7 HIGH when the app is clearly a content site (has public routes with meaningful content). Auth-gated apps (dashboards, admin panels) should stay at WARN/INFO since SEO is not a concern.
- **Noscript is not a substitute for SSR/SSG**: `<noscript>` catches only the "no-JS" case, not the "crawler without JS execution" case — don't upgrade a CSR HIGH to WARN just because noscript exists.
- **No auto-fix in v1**: Fixing SEO issues requires design/content decisions beyond pattern matching.

## Reference Documents

Vendored with this skill (clean at the 2026-08-10 era review):

- [reference/w3c-guidelines.md](reference/w3c-guidelines.md) — HTML5 semantic requirements, meta tag specs, language tag rules, canonical and parameter handling.
- [reference/core-web-vitals.md](reference/core-web-vitals.md) — LCP/INP/CLS thresholds, resource hints, above-the-fold heuristic, per-framework image components.
- [reference/spa-ssg-patterns.md](reference/spa-ssg-patterns.md) — Rendering-mode decision tree, SPA pitfalls, per-framework detection patterns, prerendering strategies.
- [scripts/seo-scanner.py](scripts/seo-scanner.py) — stdlib-only mechanical scanner (a standalone subset of the categories above); the Step 2 Verify block runs it. Its llms.txt finding is informational-only under ## Era.

Excluded from the upstream set as era-stale (see ## Findings for the specifics): reference/schema-types.md, reference/geo-aeo-patterns.md, reference/geo-guidelines.md, reference/content-citability.md, reference/ai-pipeline.md. Their still-valid content — the structured-data required-property matrix — is folded into Category 3 above.

## Findings

### Defects fixed

- **Category 3 FAQPage row** demoted WARN → INFO and re-dated: existing markup is validated structurally and reported as informational, because Google retired FAQ rich results for every site on 2026-05-07.
- **Category 6 chunking row** demoted WARN → INFO and stripped of its restructure imperative; the entire GEO category is demoted to hypothesis tier because its retrieval-window rationale is single-source and chunking content for AI is the exact practice Google names as a mistake.
- **Category 6 add-FAQPage row** replaced with an informational existing-FAQPage/HowTo flag. Never recommend adding FAQPage or HowTo for Google benefit; HowTo has been deprecated since September 2023.
- **Category 10** AI-signal rationale (Gecko, Blyskall figures, Query Fan Out) conditioned to hypothesis tier; the structural link checks remain load-bearing.
- **Vendored scanner's llms.txt finding** era-conditioned: llms.txt sits at roughly 0.015% adoption with no vendor confirmation, so the finding is informational-only, never a recommended fix.
- **Summary, Rules, and Usage scopes** re-labeled so the GEO output cannot be read as a checklist; a new rule bullet forbids recommending retired rich-result schema.
- **Era-clean AI-crawler robots.txt directives recovered** from the excluded AEO reference and folded into Category 8: the User-agent table plus the caution that blocking `Googlebot` blocks AI Overviews while `Google-Extended` is the Gemini-training opt-out (whether it also affects AI Overviews inclusion is unverified — Stage 2.5 bundle adjudication, 2026-08-10), with two new intent-check rows.
- **Remaining clean schema-type coverage folded** into Category 3 (Event, WebSite/SearchAction, Recipe, VideoObject, case-sensitive `@type`, no fabricated ratings), and the native `<details>`/`<summary>` DOM-visibility exemption restored in the Category 6 hidden-content row.
- **Two dead anchor fragments** in the sample report corrected to real headings (`#above-the-fold-heuristics`, `#prerendering-strategies-for-spas`) — a pre-existing base defect; the base pointed at headings that do not exist in its own reference files.

### Security review (editorial)

- `scripts/seo-scanner.py` reviewed line by line: Python stdlib only, filesystem reads only, no network egress, no file writes, no subprocess use. Exit codes 0/1/2 as documented in the Step 2 Verify block. The script's behavior is consistent with the document's read-only contract.

### Excised

Five upstream reference files were excluded from the vendored set because each teaches an era-stale practice; vendoring them unmodified would reimport the defects this derivative fixes:

- `reference/schema-types.md` — states "Triggers rich FAQ results in SERP." and lists HowTo among rich-result-eligible types. Its still-valid type coverage (required-property matrix, Event/WebSite/Recipe/VideoObject notes, common-mistake items) is folded into Category 3; the full JSON-LD templates are not carried.
- `reference/geo-aeo-patterns.md` — calls FAQPage the "highest-precision signal", ships HowTo pattern checks, and its checklist requires llms.txt at the domain root. Its era-clean robots.txt AI-crawler directives are folded into Category 8.
- `reference/geo-guidelines.md` — teaches "The 375-word rule" as a checklist item and instructs pairing procedures with HowTo schema. Its era-clean native `<details>`/`<summary>` exemption is folded into the Category 6 hidden-content row.
- `reference/content-citability.md` — its chunk-architecture section instructs keeping every H2 under ~375 words and splitting with an H3, i.e. chunking-for-AI as a rule.
- `reference/ai-pipeline.md` — routes "how to X" queries to HowTo and persona queries to FAQPage as live format signals, and teaches chunk-position targeting; single uncorroborated agency source throughout.

Also excised: the original harness frontmatter and `$ARGUMENTS` macro (not portable into this collection's frontmatter model; the CLI flags are documented verbatim under ## Usage).

### Grafts

None.

## Attribution

Derived from **softspark/ai-toolkit/seo-validate** (repository: https://github.com/softspark/ai-toolkit, skill directory `app/skills/seo-validate`), Copyright 2024-2026 Lukasz Krzemien, licensed under the Apache License, Version 2.0. This derivative is itself distributed under the Apache License, Version 2.0.

Vendored files, all from softspark/ai-toolkit/seo-validate (Apache-2.0, fetched 2026-08-10): `reference/w3c-guidelines.md`, `reference/core-web-vitals.md`, `reference/spa-ssg-patterns.md`, `scripts/seo-scanner.py` (retains its SPDX header and copyright notice).

Changes:
- Demoted the GEO category (Category 6) to hypothesis tier: all findings INFO/heuristic, output read as a hypothesis, never a checklist; rewrote the category preamble to state the era adjudication.
- Removed the chunking row's restructure-for-AI imperative and demoted it WARN → INFO.
- Re-dated all FAQPage/HowTo guidance (FAQ rich results retired for every site 2026-05-07; HowTo deprecated September 2023); replaced the add-FAQPage recommendation with an informational existing-markup flag; added a rule forbidding recommending either for Google benefit.
- Excluded five era-stale reference files (`reference/schema-types.md`, `reference/geo-aeo-patterns.md`, `reference/geo-guidelines.md`, `reference/content-citability.md`, `reference/ai-pipeline.md`) from the vendored set; removed all body pointers to them; folded a corrected structured-data required-property matrix into Category 3.
- Added an era note conditioning the vendored scanner's llms.txt INFO finding (roughly 0.015% adoption, no vendor confirmation).
- Conditioned Category 10's AI-retrieval rationale to hypothesis tier while keeping its structural checks.
- Added the `## Conditions` block (when to use / when NOT to use / prerequisites / what breaks first), the `## Era` section, this `## Findings` record, and inline `### Verify` blocks after Steps 1, 2, and 4 — including one that runs `scripts/seo-scanner.py` and one that greps the produced report for retired-schema recommendations.
- Annotated the top summary paragraph, the standards-basis line, and the Usage scopes list so the GEO category is always presented as hypothesis tier ("chunk architecture" removed from the summary's gap list; "emerging GEO practices" replaced with a pointer to ## Era).
- Folded the era-clean AI-crawler robots.txt directives from the otherwise-excluded AEO reference into Category 8: the User-agent table, the Googlebot/Google-Extended caution, and two new intent-check rows.
- Folded the remaining clean schema-type coverage into Category 3 (Event, WebSite/SearchAction, Recipe, VideoObject, case-sensitive `@type`, prohibition on fabricated ratings) and restored the native `<details>`/`<summary>` DOM-visibility exemption in Category 6.
- Corrected two dead anchor fragments in the sample report to real headings (`#above-the-fold-heuristics`, `#prerendering-strategies-for-spas`) — a pre-existing defect in the base.
- Replaced the original command frontmatter (`user-invocable`, `argument-hint`, `allowed-tools`, `agent`, `$ARGUMENTS`) with this collection's domesticated-skill frontmatter and wrote a fresh description.
- Kept unchanged: framework/rendering detection, Categories 1, 2, 4, 5, 7 and 9, Category 3's rule table apart from the FAQPage row, Category 8's rule set apart from the two added AI-crawler rows, the above-the-fold rules (including the HIGH/definitive above-the-fold `loading="lazy"` flag), the output format apart from the two anchor corrections, the robots.txt/canonical parameter-handling guidance, and the exit-code contract.
