# Changelog

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
