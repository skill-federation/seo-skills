# seo-validate

**Repo-reading pre-ship SEO audit for source code: detects the framework first, then applies framework-conditioned rules with severity and definitive-vs-heuristic confidence labels; strictly read-only. Reach for it when the pages to check live in a codebase rather than behind a live URL. Era-adjudicated 2026: retired FAQ/HowTo rich-result guidance excised, GEO checks demoted to hypothesis.**

An upgraded, era-verified derivative of [`softspark/ai-toolkit/seo-validate`](https://github.com/softspark/ai-toolkit) —
9 defect fixes and 6 excisions, with its guidance checked against platform reality current to 2026 (the kind
of dated facts a wild skill silently predates). Conditions are stated, every workflow step ends
in a runnable check, and what changed from the original is recorded with reasons.

## Install

```bash
npx skills add skill-federation/seo-skills --skill seo-validate
```

## When to use it

- The pages you need to audit live in a repository — framework projects (Next.js, Nuxt, Astro, Gatsby, SvelteKit, Remix, Angular, Vue/React SPAs) or plain static HTML — and you want SEO defects surfaced **before** anything ships.
- Pre-merge or CI gating: `--output json` plus the exit-code contract (non-zero on HIGH findings) makes this usable as a blocking check.
- Migration audits: `--scope rendering` isolates the SPA/CSR/SSG crawlability category when you are moving a client-rendered app toward SSR/SSG.
- You want findings with file paths, line numbers, severity, and an honest `definitive` vs `heuristic` confidence label rather than an unqualified score.

## When NOT to use it

- The target is a **live URL** rather than a repo checkout. This skill never fetches anything; use a crawling audit for deployed sites.
- You need runtime truth: real Core Web Vitals field data, server response headers, redirect chains, rendered-DOM comparisons. Static source analysis cannot see what only exists at runtime.
- You expect fixes to be applied. The contract is read-only: it reports, it never edits.
- The codebase is not a web frontend (APIs, CLIs, libraries) — there is nothing for the rules to bind to.

## Provenance & trust

Derived from [`softspark/ai-toolkit/seo-validate`](https://github.com/softspark/ai-toolkit) · Apache-2.0 · last
verified 2026-08-10. Every source, the full list of changes, and attribution are
in [SKILL.md](SKILL.md); every vendored file is pinned by sha256 in the bundle's
[`bundle.json`](../../bundle.json).

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
