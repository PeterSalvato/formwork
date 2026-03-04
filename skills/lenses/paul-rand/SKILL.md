---
name: paul-rand
description: "Paul Rand lens — Concept. Does the design communicate an idea? Is there wit and simplicity behind the form? Read-only diagnostic."
user_invocable: true
---

# Paul Rand Lens — Atomic Skill

## Purpose

Paul Rand's standard: design is the method of putting form and content together. Not arrangement. Not decoration. An idea. The best design communicates a concept so simply that wit and clarity become the same thing. This lens evaluates whether the visual design has a concept behind it, or whether it is merely organized elements.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/paul-rand                 # Evaluate full site screenshots
/paul-rand [page-name]     # Evaluate a specific page's screenshot
```

## Context

### Read
- Screenshots from `.audit/screenshots/` (latest set) — REQUIRED. Never evaluate from source code alone.
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set relevant to this lens's domain
- `.audit/rubric.md` if it exists

### Invoke (as needed)
- `/print-craft` → material quality baseline → PRESSED/ADEQUATE/DIGITAL (for texture-related questions)

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Evaluate

### Step 0: Read Screenshots (Mandatory)

Before evaluating ANY question below, use the Read tool to view the screenshot images provided in your prompt. Claude can read PNG files — the Read tool returns visual content.

Read each screenshot path provided. Base ALL evaluations on what you SEE in the screenshots, not on source code, CSS, or documentation. If no screenshot paths were provided, state "NO SCREENSHOTS PROVIDED — cannot evaluate" and stop.

Do NOT fall back to reading SCSS, CSS, or HTML files. The evaluation is of the RENDERED output, not the source.

---

For each screenshot (or the set as a whole), ask:

### R1. Is there a concept behind the design, or is it just arrangement?

Look at the overall composition. Is the layout driven by an idea — a visual argument, a structural metaphor, a deliberate tension — or is it elements placed according to convention? Rand's IBM posters weren't "nicely arranged" — each one communicated a single idea through form. Does this design do the same?

### R2. Does the visual communicate an idea on first contact?

Before reading any text, what does the design itself say? Is there a message in the composition, the hierarchy, the relationship between elements? Or does the design only become meaningful once you read the words? The form should carry meaning independent of the content it holds.

### R3. Is there wit or cleverness that serves clarity, not decoration?

Rand's rebus logos, his playful geometry — the wit always made the idea clearer, never competed with it. Look for moments where the design does something unexpected that makes the communication sharper. Flag cleverness that exists for its own sake or decoration that masquerades as concept.

### R4. Does simplicity carry complexity?

The mark of Rand's work: what looks simple is actually holding together something complex. A single symbol that contains an entire corporate identity. A poster that reduces a message to its irreducible form. Does this design achieve that compression — complexity made simple through design — or is it simple because it is merely thin?

## Output

Print in conversation. No file changes. Format:

```
# Paul Rand Lens — "Concept."

## Overall: [CONCEPTUAL / FUNCTIONAL / EMPTY]

**R1. Concept or arrangement?** — [verdict]
[Evidence from screenshots.]

**R2. Idea on first contact?** — [verdict]
[Evidence from screenshots.]

**R3. Wit serving clarity?** — [verdict]
[Evidence from screenshots.]

**R4. Simplicity carrying complexity?** — [verdict]
[Evidence from screenshots.]

## The Idea
[One sentence: what concept, if any, is the design communicating?]
```

### Verdict Scale

- **CONCEPTUAL** — the design communicates an idea. Form and content are unified. Wit and simplicity serve the concept.
- **FUNCTIONAL** — the design works but lacks a driving concept. Elements are well-organized without being idea-driven.
- **EMPTY** — the design is arrangement without concept. Decoration without wit. Simplicity without depth.

## Direction (if not all passing)

For each non-passing question, state:
- What specifically is wrong (with evidence from screenshots)
- What specifically to change (exact CSS/SCSS/HTML change, not "improve X")
- Which files to modify
- What the result should look like after the change

## Limitations

Claude's visual assessment, not expert critique. Useful as structured feedback, not authoritative judgment.

## Called By

- `/design-review` coordinator — runs in parallel with other visual lenses
- Standalone — usable anytime
