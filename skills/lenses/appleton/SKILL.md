---
name: appleton
description: "Appleton lens — Is the knowledge alive? Digital garden patterns applied to a professional portfolio. Connections, growth, epistemic disclosure. Read-only diagnostic."
user_invocable: true
---

# Appleton Lens — Atomic Skill

## Purpose

Maggie Appleton's digital garden patterns: topography over timelines, continuous growth, epistemic disclosure, independent ownership. This lens evaluates whether the portfolio is a living document with visible thinking, or a frozen showcase.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/appleton                  # Evaluate full constellation
/appleton [page-path]      # Evaluate a single page
```

## Context

### Read
- All published pages (frontmatter + body): `_governance/`, `_infrastructure/`, `_output/`, `_blog/`
- Standalone pages: `bio/index.md`, `contact.md`, `colophon.md`, `thinking.md`, `vocabulary.md`
- Homepage: `_data/index.json` + `_layouts/systemworks.html`
- Screenshots from `.audit/screenshots/` (latest set)
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set (for visual context during evaluation)
- `.audit/rubric.md` if it exists — Peter's annotations override defaults

### Invoke (as needed)
- `/knowledge` → search ideation history for grounding → source-attributed results
- `/baseline` → mechanical health facts (link status, image status) → pass/fail per check

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Verdict Scale

- **STRONG** — exceeds the test. Genuinely impressive, holds up against best-in-class.
- **HOLDS** — passes the test. Solid, no meaningful gaps.
- **WEAK** — substantive gaps that undermine the intent.
- **BROKEN** — fundamental failure on one or more questions.

## Questions

### A1. Are ideas connected by meaning or only by category?

Read: all page cross-references, navigation structure
Evaluate: Can you trace how thinking in one project informed another? Does governance reference infrastructure? Do output projects feed back into governance? Or do projects sit in isolated category buckets?
Flag: Isolated projects with no visible conceptual links to other work.

### A2. Can I tell what's finished vs. in progress vs. rough?

Read: all project frontmatter (fidelity field, status indicators)
Evaluate: Are development stages honestly signaled? Does the site distinguish between shipped work, active development, and early exploration?
Flag: Everything presented at the same level of authority regardless of actual stage. Misleading status claims.

### A3. Does the structure reflect how this person thinks?

Read: navigation, tier system, vocabulary, altitude system
Evaluate: Is the 3-tier architecture (governance/infrastructure/output) a genuine mental model unique to this person? Or is it a conventional portfolio (about/work/contact) with different labels?
Flag: Architecture that could be copy-pasted to any other portfolio without changing the organizing logic.

### A4. Is there visible growth and revision?

Read: `last_modified` dates, content that references evolution
Evaluate: Evidence that the site is a living document — recent updates, content that has visibly evolved, ideas developed in public.
Flag: A portfolio that appears frozen. Stale `last_modified` dates. No evidence of ongoing development.

### A5. Can I navigate by curiosity?

Read: navigation, cross-links, page structure
Evaluate: Can you follow a conceptual thread (governance, drift, scaffolding, constraint) across multiple projects? Or are you forced through a linear hierarchy?
Verify vocabulary tooltip visibility: if baseline results show fewer than 6/9 terms matching, tooltips cannot be cited as a curiosity navigation mechanism.
Flag: No lateral connections. Navigation only by category, never by concept.

## Output

Print in conversation. No file changes. Format:

```
# Appleton Lens — "Is the knowledge alive?"

## Overall: [STRONG / HOLDS / WEAK / BROKEN]

**A1. Connected by meaning?** — [verdict]
[Evidence.]

**A2. Development stages visible?** — [verdict]
[Evidence.]

**A3. Structure reflects thinking?** — [verdict]
[Evidence.]

**A4. Visible growth?** — [verdict]
[Evidence.]

**A5. Navigate by curiosity?** — [verdict]
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
- `/full-pass run` — via audit
- Standalone — usable anytime
