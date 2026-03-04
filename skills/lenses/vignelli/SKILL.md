---
name: vignelli
description: "Vignelli lens — Restraint as clarity. Type discipline, grid consistency, color economy, systematic limitation. Read-only diagnostic."
user_invocable: true
---

# Vignelli Lens — Atomic Skill

## Purpose

Massimo Vignelli's standard: "The life of a designer is a life of fight — fight against the ugliness." Ugliness, for Vignelli, meant excess. Too many typefaces. Arbitrary grids. Color without reason. This lens evaluates whether the design achieves clarity through disciplined limitation, or whether it mistakes variety for richness.

Read-only diagnostic. Evaluates screenshots. No file changes.

## Usage

```
/vignelli                          # Evaluate all screenshots
/vignelli [screenshot-path]        # Evaluate a single screenshot
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

"Restraint. How many type sizes? Is the grid mathematical? Does limitation produce clarity?"

For each screenshot, ask:

### V1. Type discipline — how many sizes?

Look at the screenshot and count distinct type sizes visible on the page. Vignelli used a maximum of three sizes in most work. More than four is almost always a sign of indecision.
Flag: More than four distinct type sizes. Sizes that differ by trivially small amounts (suggesting no intentional scale). Display type competing with body type for attention.

### V2. Grid consistency

Does the layout follow a visible mathematical structure? Are elements aligned to a consistent grid, or do they feel arbitrarily placed? Vignelli's grids were simple and unbreakable.
Flag: Elements that break alignment without conceptual justification. Inconsistent margins or gutters. Layout that shifts logic between sections.

### V3. Color restraint

How many colors are in use? Are they systematic or decorative? Vignelli treated color as information, not ornament — each color carried meaning.
Flag: More than three or four colors without clear semantic purpose. Color used for decoration rather than hierarchy or meaning. Gradients or effects that add complexity without communication.

### V4. Systematic hierarchy

Is there a clear, repeatable system for how information is ranked? Headings, subheadings, body, captions — each level should be immediately distinguishable and consistent across the entire design.
Flag: Hierarchy that changes between pages or sections. Levels that are ambiguous (is this a heading or a subheading?). Decorative treatments that obscure the information order.

### V5. Does limitation produce clarity or feel forced?

This is the crucial test. Restraint is not the same as poverty. A Vignelli design feels inevitable — as if nothing else was possible. A merely minimal design feels like something is missing.
Flag: Restraint that reads as emptiness rather than intention. Limitation that produces confusion (too few visual cues to navigate). Austerity that feels performative rather than purposeful.

## Output

Print in conversation. No file changes. Format:

```
# Vignelli Lens — "Restraint as clarity"

## Overall: [DISCIPLINED / ADEQUATE / UNDISCIPLINED]

**V1. Type discipline** — [observation]
[Evidence from screenshots. Specific count of sizes observed.]

**V2. Grid consistency** — [observation]
[Evidence. What aligns, what breaks.]

**V3. Color restraint** — [observation]
[Evidence. Colors identified, their apparent purpose.]

**V4. Systematic hierarchy** — [observation]
[Evidence. How information levels are distinguished.]

**V5. Limitation produces clarity?** — [observation]
[Evidence. Whether the restraint feels purposeful or impoverished.]
```

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
