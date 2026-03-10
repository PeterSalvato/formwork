---
name: millman
description: "Millman lens — Is this person real? Deliberate differentiation, vulnerability matching authority, life-arc coherence. Read-only diagnostic."
user_invocable: true
---

# Millman Lens — Atomic Skill

## Purpose

Debbie Millman's core test: "If you're not creating something that's different from everything else, why do you need it?" This lens evaluates whether the portfolio reveals a real person with real stakes, or a professional template with a name on it.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/millman                   # Evaluate full constellation
/millman [page-path]       # Evaluate a single page
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
- `/voice-sample` → Peter's actual speaking patterns → rhythm, vocabulary, humor observations

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Verdict Scale

- **STRONG** — exceeds the test. Genuinely impressive, holds up against best-in-class.
- **HOLDS** — passes the test. Solid, no meaningful gaps.
- **WEAK** — substantive gaps that undermine the intent.
- **BROKEN** — fundamental failure on one or more questions.

## Questions

### M1. What can only this person do?

Read: manifesto (`_data/index.json`), bio, all project pages
Evaluate: Is the positioning genuinely distinct? Could you swap in twenty other names? Look for specifics that anchor the identity to this person's actual history.
Flag: Generic claims. Positioning that describes a category, not a person.

### M2. Does the vulnerability match the authority?

Read: all project pages, bio
Evaluate: Are failures, struggles, and what broke shown alongside what worked? Is difficulty shown through what it took (iterations, what broke) rather than claimed?
Flag: Pages that present only polished success. Claims of difficulty without evidence.

### M3. Best-day self or a character?

Read: manifesto, bio, voice across all pages
Evaluate: Does the voice sound like a real person with real stakes, or like a brand strategy document? Is there a gap between the stated philosophy and how the site actually reads?
Flag: Corporate voice. Philosophy that sounds scripted rather than believed.

### M4. Does the constellation tell a life-arc story?

Read: all published pages in order (governance → infrastructure → output), bio, blog posts
Evaluate: Can you see one person's specific obsessions producing all of this? Is there a throughline from the earliest work to the most recent?
Flag: Projects that feel disconnected from the central identity. Gaps in the narrative.

### M5. Where is the courage?

Read: all project pages, output section especially
Evaluate: Evidence of risk-taking — projects started before knowing they'd succeed, work made public while still developing, unconventional approaches.
Flag: A portfolio that only shows safe, completed, validated work.

## Output

Print in conversation. No file changes. Format:

```
# Millman Lens — "Is this person real?"

## Overall: [STRONG / HOLDS / WEAK / BROKEN]

**M1. What can only this person do?** — [verdict]
[Evidence. Specific pages cited.]

**M2. Vulnerability matches authority?** — [verdict]
[Evidence.]

**M3. Best-day self or a character?** — [verdict]
[Evidence.]

**M4. Life-arc story?** — [verdict]
[Evidence.]

**M5. Where is the courage?** — [verdict]
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
