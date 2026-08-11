# seo-validate

> Repo-reading pre-ship SEO audit for source code: detects the framework first, then applies framework-conditioned rules with severity and definitive-vs-heuristic confidence labels; strictly read-only. Reach for it when the pages to check live in a codebase rather than behind a live URL. Era-adjudicated 2026: retired FAQ/HowTo rich-result guidance excised, GEO checks demoted to hypothesis.

**Install**

```bash
npx skillfed install skill-federation/seo-skills/seo-validate
```

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

Targets: softspark/ai-toolkit seo-validate @ HEAD, fetched 2026-08-10 · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [softspark/ai-toolkit/seo-validate](https://github.com/softspark/ai-toolkit) (Apache-2.0)
- **License**: Apache-2.0 (this directory's LICENSE)
- **What domestication changed**: 9 defect(s) fixed, 6 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
