# claude-seo

> Front door for a bundled SEO toolchain: /seo commands route bundled Python through the claude-seo launcher, with a doctor preflight and parallel full audits whose conditional specialists spawn only when site signals warrant them. Use it when an agent must produce client-grade SEO reports under 2026 rules — FAQ rich results retired, HowTo schema dead, llms.txt unproven — behind hard quality gates and with zero promotional content in deliverables.

**Install** (the [`skills`](https://www.npmjs.com/package/skills) CLI reads this repo's layout directly from GitHub)

```bash
npx skills add skill-federation/seo-skills --skill claude-seo
```

## Conditions

### When to use

- You want one front door over a full SEO toolchain: 20+ `/seo` commands backed by bundled Python tools, with parallel sub-agent fan-out for full site audits and a unified 0–100 health score.
- You are producing client-grade deliverables (site audits, technical reports, strategic plans) and want hard, enforced quality gates — location-page hard stops, retired-schema refusals — rather than advisory prose.
- The site's business type is unknown up front: the skill detects SaaS / local / e-commerce / publisher / agency signals from the homepage and spawns only the matching specialists.

### When NOT to use

- For a single quick scored check or a repo-level pre-ship validation: a narrower single-purpose skill costs less than this suite's runtime setup.
- For a one-off full technical audit where toolchain setup isn't warranted: a standalone curl-based audit (geo-technical in this bundle) covers the live eight-category inspection with nothing to install beyond a shell.
- For forensic traffic-drop diagnosis ("why did rankings fall last month") — out of scope across this bundle. `/seo drift` only compares against a baseline captured before the change, and seo-google's organic-traffic trends are data, not a forensic method; neither reconstructs a past you didn't baseline.
- On machines where an isolated Python runtime and Chromium cannot be installed — the bundled tools will not run and the skill degrades to unverified prose.
- When policy forbids sending site or keyword data to third-party vendors and the task depends on the extensions: every extension (Firecrawl, DataForSEO, image-gen, Ahrefs, Bing, Profound, SE Ranking, Unlighthouse) calls a third-party API.

### Prerequisites

- The upstream toolchain itself. This bundle ships the front door document (plus references and license) only: the launcher, the bundled Python tools, and the 24 sub-skills it orchestrates come from installing the upstream repository — https://github.com/AgriciDaniel/claude-seo — as a plugin or a repo checkout. Acquire that first; nothing in this bundle provides it. The doctor preflight below verifies the acquisition before anything else runs.
- The `claude-seo` launcher. Plugin installs expose it automatically; repository users run `./bin/claude-seo`; manual installers rewrite the command to the isolated launcher path. Run bundled Python tools only through `claude-seo run <script.py>`. Never invoke bundled scripts with a bare Python interpreter.
- An isolated Python runtime plus Chromium, created only on explicit `/seo setup` (or an explicit repair request). If any `claude-seo run` command reports that setup is required, suggest `/seo setup` — do not improvise a `pip install`, and do not fall back to global or user package installation.
- Optional, feature-gating: Google API credentials (`claude-seo run google_auth.py --check`), backlink API keys (`claude-seo run backlinks_auth.py --check`), a DataForSEO MCP, a Firecrawl MCP.
- Extensions require their own installers (each extension's `install.sh` / `install.ps1`) plus third-party accounts — and every extension call sends the URLs, keywords, or log-derived queries you are analyzing to that vendor's servers. Treat this as data egress: get sign-off before enabling any extension on a client engagement.

### What breaks first

- The runtime, loudly: bundled scripts invoked outside the launcher, or a missing Chromium, stop commands cold. Run the doctor preflight (below) before an engagement; this suite fails before it misleads.
- Schema recommendations, silently: FAQ/HowTo/llms.txt status is the category's fastest-rotting ground. The gates below pin their 2026 status; if you read this long after the last-verified date, re-check those pins first.
- Extension integrations: vendor auth schemes, rate limits (DataForSEO caps at 2,000 API calls/minute per `references/maps-api-endpoints.md`), and pricing change without notice.
- Programmatic location-page expansion: the 30-page warning and 50-page hard stop fire. A fired gate is the system working, not an obstacle to route around.

## Era

Targets: 2.2.4 · claims last verified **2026-08-10**.
Every dated fact this document depends on is pinned in [SKILL.md](SKILL.md)'s Era section.

## Provenance

- **Derived from**: [AgriciDaniel/claude-seo/seo](https://github.com/AgriciDaniel/claude-seo) (MIT)
- **Sibling** (zero text taken): AgriciDaniel/codex-seo/seo
- **Sibling** (zero text taken): AgriciDaniel/claude-seo/seo-audit
- **Sibling** (zero text taken): AgriciDaniel/codex-seo/seo-audit
- **License**: MIT (this directory's LICENSE)
- **What domestication changed**: 3 defect(s) fixed, 2 excision(s) — full record with reasons in [SKILL.md](SKILL.md)'s Findings and Attribution sections.

Part of the [seo-skills bundle](../../README.md) · curated by [skillfed.io](https://skillfed.io)
