---
name: geo-audit
description: 'A scored technical audit of whether a live domain is legible to AI-search crawlers, current
  to 2026: one stdlib Python script, about 30 seconds, five load-bearing checks (robots.txt bot access,
  pre-JS rendering, sitemap, JSON-LD, internal links) with llms.txt reported as informational only. Reach
  for it when a site needs a fast numeric verdict on AI-crawler visibility before content spend; it refuses
  to emit numbers when the script cannot run or the domain will not resolve.'
license: MIT
treatment: derivative
derived_from:
- id: vellum-ai/vellum-assistant/geo-audit
  role: base
  license_at_derivation: MIT
  content_hash_at_derivation: 256824ad7cdd84f6623f3712aa9fb83e0484b0fe35ff74d4df75e82aaf01cb7e
targeted_version: audit.py 1.0 (upstream HEAD, fetched 2026-08-10)
last_verified_at: 2026-08-10
---

# GEO Audit — SkillFed domesticated edition

One vendored Python script, six measurements, a numeric verdict in about 30 seconds: the fast operator-side check that a website is legible to AI crawlers before anyone spends a quarter producing content for them. This edition keeps the script and the refusal discipline, corrects the check descriptions to what the code actually measures, and re-weights one stale check out of the score.

## Conditions

### When to use

- A live, publicly reachable domain needs a fast scored read on AI-crawler legibility — before a content program, during triage, or when someone asks why ChatGPT, Perplexity, Gemini or Claude never surfaces the site.
- The user says "run a GEO audit on <url>", "audit <url> for GEO", "how AI-ready is my site" or a close variant: extract the domain and run the script immediately, no clarifying questions.
- You want a keepable artifact: the script writes an HTML report alongside the streamed terminal scorecard.

### When NOT to use

- The site only exists in a repository or on localhost — this skill fetches public URLs; use a repository-reading validator for pre-ship checks.
- Content writing, comparison pages, or GEO strategy and cadence work — this is an audit; it produces no prose and no plan.
- Auth-walled or staging hosts the public internet cannot fetch, and domains behind a WAF that challenges plain scripted user agents — the score would measure the wall, not the site.
- Anything needing a deep multi-page crawl: the script reads the homepage plus a handful of well-known root paths, nothing more.

### Prerequisites

- `python3` on PATH; the script uses only the standard library (no pip installs).
- Outbound HTTPS from the session to the target domain — the script performs about a dozen GET requests.
- The vendored script at `{baseDir}/scripts/audit.py` (sha256 pinned in the frontmatter).

### What breaks first

- DNS failure does not abort the run: the script still prints a scorecard (its robots.txt check hands 18 partial-credit points to a domain that does not exist). The tripwire is the finding "Homepage did not return 200 (0)" — status 0 means the fetch itself errored. Treat that run as failed and produce no score.
- Bot-challenging CDNs: a 403 or 503 to the script's user agent zeroes the rendering and link checks regardless of what real AI crawlers see. Report the block; do not score through it.
- Slow origins: the per-request timeout defaults to 10 seconds; heavy sites can trip it. Re-run with a higher `--timeout` before concluding anything.

## Era

Targeted: the upstream `audit.py` as fetched 2026-08-10 (script version 1.0; hash in the frontmatter). Reviewed 2026-08-10. Three dated facts govern how this edition reads the script's output:

- llms.txt is a proposed convention at roughly 0.015% adoption with no vendor confirmation — no major AI vendor has confirmed reading it. The upstream script still scores it 15/100 and can rank creating one as the top fix; this edition reports the check as informational, gives it zero weight, and never surfaces it as a fix.
- Google retired FAQ rich results for every site on 2026-05-07, and HowTo has been deprecated since Sept 2023. The script's schema check still counts FAQPage among accepted content types; an existing FAQPage block still parses as structure, but never recommend adding FAQPage or HowTo markup as an audit fix.
- The five remaining checks — per-bot robots.txt access, server-side rendering, sitemap, homepage JSON-LD, and crawlable internal links — are load-bearing and current.

## Step 1 — Run the audit

```bash
python3 {baseDir}/scripts/audit.py <domain>
```

Examples:

```bash
python3 {baseDir}/scripts/audit.py vellum.ai
python3 {baseDir}/scripts/audit.py https://stripe.com
python3 {baseDir}/scripts/audit.py example.com --json
```

The script normalizes bare domains, full URLs, and anything in between. Flags: `--json` (machine-readable report), `--no-color` (strip ANSI for logs/CI), `--no-html` (skip the HTML report), `--no-open` (write the HTML but don't launch a browser), `--timeout N` (per-request seconds, default 10).

Failure discipline, carried from the base and binding:

- If the script runs cleanly → stream the output and summarize.
- If the domain is unreachable / DNS fails / times out → report the specific failure plainly, suggest checking the domain or raising `--timeout`, and do not invent a score. The script itself will still print numbers for a dead domain (see What breaks first), so YOU must catch the status-0 finding and refuse.
- If `python3` is unavailable or blocked in this session → say so directly. Do not fabricate a scorecard or paraphrase what the audit "would" find.

### Verify

```bash
python3 {baseDir}/scripts/audit.py <domain> --json --no-html | python3 -c "import json,sys; d=json.load(sys.stdin); assert d['max_score']==100 and len(d['checks'])==6, 'unexpected report shape'; print('ran:', d['score'], '/', d['max_score'], 'on', d['domain'])"
```

A clean run prints the raw score; an exception here means the report is malformed and nothing downstream may be presented. To confirm the dead-domain tripwire is detectable (this is what refusal keys on):

```bash
python3 {baseDir}/scripts/audit.py no-such-host-geoaudit.invalid --json --no-html | grep -c "did not return 200 (0)"
```

A count of 1 or more on an unresolvable name proves the status-0 signal surfaces in the report; when it appears for the user's real domain, there is no score.

## Step 2 — Read the scorecard on the load-bearing scale

What the script actually measures, verified against the vendored code:

1. **AI crawler access via robots.txt (25 pts)** — parses per-agent groups for `GPTBot`, `ChatGPT-User`, `OAI-SearchBot`, `ClaudeBot`, `anthropic-ai`, `PerplexityBot`, `Perplexity-User`, `Google-Extended`, and `CCBot`; −3 per blocked agent; a missing robots.txt yields 18/25 with a flag. `Google-Extended` is Google's Gemini/AI-training opt-out; whether blocking it affects AI Overviews inclusion is unverified (2026-08-10) — blocking `Googlebot` is what verifiably removes a site from AI Overviews along with regular Search.
2. **llms.txt (15 pts in the raw script — informational here)** — existence, a top-level `#` title, curated links, and a 3-link resolution sample. Report presence and shape; never count it, never fix-list it.
3. **Server-side rendering (20 pts)** — visible word count in the pre-JS HTML: 200+ words earns the full word-count credit (8 of the 20), 60–199 words is flagged as likely JS-rendered, and under 60 words is treated as an effectively empty page; plus H1, `<title>`, meta description, and og:title presence. The base described brand-name and CTA detection; the code measures these five signals.
4. **Sitemap (10 pts)** — tries `/sitemap.xml`, `/sitemap_index.xml`, and `/sitemap-index.xml`; scores existence, XML parse with entries, and a `Sitemap:` reference in robots.txt.
5. **Schema markup (15 pts)** — inline JSON-LD including `@graph` nesting: Organization/Corporation/LocalBusiness, WebSite (type presence only — SearchAction is not validated), and one content schema (Product, SoftwareApplication, Article, FAQPage, or ItemList).
6. **Crawlable internal links (15 pts)** — inspects the first 50 internal `<a>` tags found among the first 120 anchors: real href values rather than JS-bound `<div onclick>` substitutes, descriptive anchor text (not "click here" / "learn more"), and a nofollow ratio under 20%.

Present the result as a load-bearing score out of 85: the printed total minus the llms.txt line. Apply the base's bands as ratios of the load-bearing maximum: 85%+ AI-ready — content investment will compound; 65–84% functional but leaking — fix the top issues before scaling content; 40–64% substantial drag — the fixes are urgent; below 40% effectively invisible — content is wasted spend until infrastructure ships.

### Verify

```bash
python3 {baseDir}/scripts/audit.py <domain> --json --no-html | python3 -c "
import json, sys
d = json.load(sys.stdin)
lb = [c for c in d['checks'] if c['name'] != 'llms.txt']
info = [c for c in d['checks'] if c['name'] == 'llms.txt'][0]
print('Load-bearing score:', sum(c['score'] for c in lb), '/', sum(c['max_score'] for c in lb))
print('Informational - llms.txt:', '; '.join(info['findings']))
"
```

The load-bearing denominator must print 85. If it does not, the vendored script changed and this document's re-weighting no longer applies — stop and say so.

## Step 3 — Deliver the report

Return the streamed script output verbatim first — the raw artifact is never edited. Then add the SkillFed reading:

```
Raw script total: 76 / 100 (includes the retired llms.txt weighting)

Load-bearing score: 71 / 85 — functional but leaking
  robots 22/25 · SSR 20/20 · sitemap 8/10 · schema 8/15 · links 13/15
Informational: llms.txt present at the root but unpopulated
  (unscored — no confirmed AI-vendor consumer)

Top fixes (llms.txt item struck — two remain of the script's top 3):
  1. Unblock AI agents in robots.txt: CCBot.
  2. Add JSON-LD to the homepage covering WebSite.
```

Every line of that sample is producible by the pinned script — the per-check scores decompose into its actual scoring components, and the two fix strings are its verbatim output for those scores, in its own priority order.

One bridge on the sample's first fix: a CCBot deduction is training-set coverage, not citation access (CCBot feeds Common Crawl's datasets, not a search-and-cite engine), so whether to unblock it is a business decision — the middle ground the bundle's strategy layer (ai-seo) adjudicates, not this audit.

Rules, tightened from the base:

- Do not silently rewrite, round, or "clean up" the report's verdicts. The numbers are the product. The one adjustment this edition makes — removing llms.txt from the score and the fix list — is always declared in the deliverable, exactly as the sample shows, never applied silently.
- The five load-bearing check scores are never altered.
- If the script's top-3 list contained an llms.txt item, strike it and present the remaining fixes; if fewer than three real fixes remain, say so — do not invent a third.
- If the script didn't run, there is no score — say that, never estimate one.
- The HTML report auto-opens by default and ends with a promotional handoff to the vendor's content tool; for client-facing deliverables run with `--no-html`, or hand over only the terminal scorecard.
- Close with one paragraph of plain-language context: what the load-bearing score means for this site and which fix ships first. Never recommend FAQPage, HowTo, or llms.txt creation in that paragraph.
- A low-scoring result is triage, not diagnosis: when the load-bearing score falls below the functional band, route the site to the bundle's full eight-category live inspection (geo-technical) before anyone starts fixing from this scorecard alone.

### Verify

```bash
python3 {baseDir}/scripts/audit.py <domain> --json --no-html | python3 -c "
import json, sys
d = json.load(sys.stdin)
cand = [c for c in d['checks'] if c.get('fix')]
assert all({'fix_impact', 'fix_effort'} <= set(c) for c in cand), 'script changed: fix ranking fields missing'
cand.sort(key=lambda c: (c['max_score'] - c['score']) * (c['fix_impact'] or 1) / max(c['fix_effort'] or 1, 1), reverse=True)
top3 = cand[:3]
keep = [c['fix'] for c in top3 if c['name'] != 'llms.txt']
print('script top 3:', ', '.join(c['name'] for c in top3))
print('present exactly these (%d struck):' % (len(top3) - len(keep)))
print(*(['  - ' + f for f in keep] or ['  (none — say so; do not invent fixes)']), sep='\n')
"
```

This reproduces the script's own `(missing × impact / effort)` ranking, strikes llms.txt entries, and prints the exact post-strike fix list — your Step 3 deliverable must match it verbatim. The field assertion is the can-fail part: it trips if the vendored script's fix-ranking interface ever changes, the same sentinel role as Step 2's /85 denominator.

## Complete when

- [ ] `audit.py` ran against the requested domain and exited without error, with no status-0 homepage finding
- [ ] The streamed scorecard was returned verbatim, followed by the declared load-bearing /85 reading
- [ ] The presented fix list contains no llms.txt, FAQPage, or HowTo recommendation
- [ ] One paragraph named which fix to ship first
- [ ] If the HTML report was generated, the user was told where it went (and `--no-html` was used for client deliverables)

## Findings

- **Defects fixed**: llms.txt demoted from a 15-point scored check and top-fix candidate to an informational presence note — zero weight, never a fix — because no major AI vendor has confirmed reading it and adoption sits around 0.015%; the presented score becomes load-bearing /85. Check descriptions corrected to the vendored code's actual behavior: the rendering check measures pre-JS word count, H1, title, meta description, and og:title (the base claimed brand-name and CTA detection), and the schema check validates WebSite type presence only, never SearchAction. The unreachable-domain refusal is now operational: the script emits a hollow ~18/100 scorecard for dead domains, so the status-0 finding is named as the mandatory refusal trigger.
- **Security notes (our editorial review, not a scan)**: the script makes about a dozen outbound GETs to the target plus up to three llms.txt-linked URLs, under a user agent identifying the upstream vendor; by default it writes an HTML report to the system temp directory and auto-opens a browser (`--no-html` / `--no-open` for CI); that HTML embeds a promotional vendor handoff — noted for client deliverables.
- **Excised**: the base's value framing of llms.txt and its sample-output block whose #1 ranked fix was creating an llms.txt file (replaced by the corrected sample in Step 3).
- **Grafts**: none.

## Attribution

- Base: `vellum-ai/vellum-assistant/geo-audit` — MIT. This document is a SkillFed derivative of that skill's SKILL.md; the audit mechanics, check catalog, scoring bands, and refusal discipline originate there.
- Vendored file: `scripts/audit.py` from the same repository (MIT), fetched 2026-08-10 at HEAD, shipped byte-identical (sha256 in the frontmatter). The re-weighting in this document happens at the reporting layer only; the script is unmodified.
- This derivative: SkillFed, published under the MIT license.
