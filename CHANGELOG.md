# Changelog

## v3 — 2026-08-11

Content release — two authored build-time planning skills added; the bundle is now 9 skills,
bundle version `3d5634ce2d5f812b`.

- **seo-plan** (new, authored) — a build-time *technical* SEO planner. It turns a new or
  pre-launch site into one written build plan — information architecture, a rendering decision,
  HTML semantics, per-page schema, Core Web Vitals budgets, an E-E-A-T and trust layer, and
  content structure — and checks that plan against itself. It fetches nothing, scores nothing,
  and edits nothing.
- **geo-plan** (new, authored) — a build-time *AI-search citation* planner. Per-engine selection
  logic (Google AI Overviews, Gemini, ChatGPT, Perplexity, Copilot, Claude), a reusable
  content-block catalogue, the structured data worth shipping, and the machine-readable-files
  layer — emitted as a build plan with an explicit skip list of what is dead or unproven in 2026.
  It plans only.
- Both are `synthesized` skills: every fact they teach traces to an already-verified member of
  this bundle (or one of its reference files), restated in our own words, with nothing invented.
  Their `synthesized_from` provenance is recorded in frontmatter and `bundle.json`.

Also in this release, the published `SKILL.md` no longer ships the internal **Findings** section
(our what-changed-from-the-wild audit trail) — it over-shares process on a public repo, so it now
lives in the source of truth only; each skill's **Attribution** section (the license credit and
statement of changes) still ships. The seven existing skills' instructions are otherwise unchanged,
apart from a one-line reciprocal-scope note in `ai-seo`.

## v2 — 2026-08-11

Presentation release — bundle content (skill instructions) is unchanged, so the bundle
version is still `4e9dd6074ced64a1`. What changed is how each skill is published:

- **Leaner public `SKILL.md`** — the frontmatter now carries only what a consumer needs
  (name, description, license, provenance). Internal validation scaffolding that used to open
  the file (present/absent string lists, dropped-block records, findings bookkeeping) no
  longer ships; the full record still lives in each skill's own **Findings** and
  **Attribution** sections.
- **Per-skill READMEs rewritten as landing pages** — each leads with what the skill does and
  why it's an upgrade over the original, then when to use it and when not, then a compact
  provenance footer.
- `bundle.json` now records `published_sha256` (the shipped file) alongside `sha256` (the
  canonical document hash the bundle version derives from).

## v1 — 2026-08-11

Initial release. 7 skills, bundle version `4e9dd6074ced64a1`.

Every skill's own **Findings** section records what domestication changed relative to its
source: era corrections, added conditions and verify steps, defect fixes, excisions, and
grafts — each with its reason.
