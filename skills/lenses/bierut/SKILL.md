---
name: bierut
description: "Bierut lens — Does the design think? Form follows content, not style. Problem-solving over decoration. Read-only diagnostic."
user_invocable: true
---

# Bierut Lens — Atomic Skill

## Purpose

Michael Bierut's standard: "I don't like doing design for designers — I like problem-solving." This lens evaluates whether the site's design serves the content and audience, or performs for a design-literate crowd.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/bierut                    # Evaluate full constellation
/bierut [page-path]        # Evaluate a single page
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

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Verdict Scale

- **STRONG** — exceeds the test. Genuinely impressive, holds up against best-in-class.
- **HOLDS** — passes the test. Solid, no meaningful gaps.
- **WEAK** — substantive gaps that undermine the intent.
- **BROKEN** — fundamental failure on one or more questions.

## Questions

### B1. Is design serving content or performing for designers?

Read: site structure, CSS approach (can assess structure, cannot assess visual quality)
Evaluate: Does the site's organization make the work accessible to the intended audience? Or does it signal sophistication to a design-literate audience at the expense of clarity?
Flag: Structure or terminology that requires design-world literacy to parse.

### B2. Can I see the problem, not just the solution?

Read: every project page's opening and frontmatter (context, drift fields)
Evaluate: Are constraint, context, and difficulty visible — or just polished deliverables? Does the reader understand what was hard before seeing what was built?
Flag: Pages that jump to the solution. Missing context/drift.

### B3. Does this show curiosity beyond design?

Read: all project pages
Evaluate: Evidence that the maker engaged deeply with each project's actual domain (jewelry, recruiting, music, narrative, household systems) rather than applying a visual style to interchangeable subjects.
Flag: Projects that feel like design applied TO a subject rather than design emerging FROM understanding the subject.

### B4. Would a non-designer understand and care?

Read: manifesto, bio, project pages
Evaluate: Is the narrative accessible to someone outside design/engineering? Could a founder, a hiring manager, a potential client follow the story?
Flag: Jargon, insider terminology, unexplained concepts. Note: verify vocabulary tooltips produce visible output — check baseline results. A tooltip mechanism with no visible matches is not sufficient.

### B5. Strip the visual treatment — is there still a point of view?

Read: all page content as pure text
Evaluate: Would the ideas survive without the CSS? Is there an editorial point of view, a structural argument, a way of seeing — or is this content that only works because it looks good?
Flag: Pages that are thin on ideas. Content that describes rather than argues.

## Output

Print in conversation. No file changes. Format:

```
# Bierut Lens — "Does the design think?"

## Overall: [STRONG / HOLDS / WEAK / BROKEN]

**B1. Design serving content?** — [verdict]
[Evidence.]

**B2. Problem visible?** — [verdict]
[Evidence.]

**B3. Curiosity beyond design?** — [verdict]
[Evidence.]

**B4. Non-designer accessibility?** — [verdict]
[Evidence.]

**B5. Point of view without visuals?** — [verdict]
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
