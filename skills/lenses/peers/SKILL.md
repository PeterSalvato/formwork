---
name: peers
description: "Peer Benchmark lens — Where does this stand? Compares portfolio against established practitioners across 5 dimensions. Read-only diagnostic."
user_invocable: true
---

# Peer Benchmark Lens — Atomic Skill

## Purpose

External comparison against established practitioners at a comparable career stage (20+ years, cross-domain, public presence). Most senior professionals have LinkedIn only (~35%) or nothing (~30%). A custom site with case studies puts you in the top ~5%. This lens compares against the top ~1%.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/peers                     # Evaluate full constellation against peer set
```

## Context

### Read
- All published pages (frontmatter + body): `_governance/`, `_infrastructure/`, `_output/`, `_blog/`
- Standalone pages: `bio/index.md`, `contact.md`, `colophon.md`, `thinking.md`, `vocabulary.md`
- Homepage: `_data/index.json` + `_layouts/systemworks.html`
- Screenshots from `.audit/screenshots/` (latest set)
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set (for visual context during evaluation)
- `.audit/rubric.md` if it exists — maker's annotations override defaults

### Invoke (as needed)
- `/knowledge` → search ideation history for grounding → source-attributed results
- `/baseline` → mechanical health facts (link status, image status) → pass/fail per check
- `/discoverability` → SEO and presence signals → STRONG/ADEQUATE/WEAK (for PB5 distribution)

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Comparison Set

| Peer | Site | Known For |
|------|------|-----------|
| Brad Frost | bradfrost.com | Atomic Design methodology, blog, courses |
| Dan Abramov | overreacted.io | React core team, pure technical blog |
| Sara Soueidan | sarasoueidan.com | Accessibility, blog, 8K+ newsletter |
| Maggie Appleton | maggieappleton.com | Digital garden, cross-linking, content maturity markers |
| Frank Chimero | frankchimero.com | The Shape of Design, essays, named clients |
| Jessica Hische | jessicahische.is | Visual portfolio organized by type, commercial clients |
| Ethan Marcotte | ethanmarcotte.com | Responsive Web Design, journal, colophon, books |
| Will Larson | lethain.com | StaffEng, 15+ years of engineering leadership blog |

## Verdict Scale

- **STRONG** — has elements no one in comparison set has
- **HOLDS** — comparable to the best in comparison set
- **WEAK** — missing elements most peers have
- **BROKEN** — below the baseline of a professional site

## Dimensions

### PB1. Structural Completeness

Evaluate against comparison set: case studies, taxonomy, structured data (JSON-LD), cross-linking, vocabulary/glossary system, metadata framework.

### PB2. Visual Evidence

Evaluate: screenshots, diagrams, work samples, before/afters relative to claims made on the site. Compare against Jessica Hische (image-rich portfolio), Brad Frost (book covers, speaking photos), Frank Chimero (project imagery).

### PB3. Public Output

Evaluate: blog post count and cadence, sustained public thinking over time. Compare against Dan Abramov (hundreds of posts), Will Larson (15+ years), Brad Frost (decade+ of blogging), Sara Soueidan (newsletter + blog).

### PB4. Social Proof

Evaluate: testimonials, named clients, audience metrics (newsletter subscribers, social following), speaking engagements. Compare against Frank Chimero (named clients: NPR, Wikipedia), Jessica Hische (commercial client logos), Sara Soueidan (8,300+ subscribers).

### PB5. Distribution Reach

Evaluate: external properties (spoke domains, syndication), newsletter, content on third-party platforms (Dev.to, LinkedIn articles, Are.na), GitHub presence as distribution channel. Compare against Brad Frost (course platform, book site), Ethan Marcotte (multiple book sites), Maggie Appleton (newsletter, Are.na).

**Weighting**: Structural completeness and visual evidence highest (what a visitor sees), then social proof and public output (credibility signals), then distribution (growth channel).

## Output

Print in conversation. No file changes. Format:

```
# Peer Benchmark — "Where does this stand?"

## Overall: [STRONG / HOLDS / WEAK / BROKEN]

**PB1. Structural Completeness** — [verdict]
[What the site has that peers don't. What peers have that the site doesn't.]

**PB2. Visual Evidence** — [verdict]
[Evidence.]

**PB3. Public Output** — [verdict]
[Evidence.]

**PB4. Social Proof** — [verdict]
[Evidence.]

**PB5. Distribution Reach** — [verdict]
[Evidence.]
```

## Direction (if not all STRONG)

For each non-passing question, state:
- What specifically is wrong (with evidence from the evaluation)
- What specifically to change (exact change, not "improve X")
- Which files/pages to modify
- What the result should look like after the change

## Called By

- `/audit run` — runs in parallel with other lenses
- `/steward run` — via audit
- Standalone — usable anytime
