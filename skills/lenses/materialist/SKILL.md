---
name: materialist
description: "Materialist lens — Is this built or decorated? Is the structure honest? Do details reveal construction? Ando/Kahn/Scarpa/Breuer composite. Read-only diagnostic."
user_invocable: true
---

# Materialist Lens — Atomic Skill

## Purpose

A composite lens drawn from Tadao Ando, Louis Kahn, Carlo Scarpa, and Marcel Breuer. Four architects who shared a conviction: materials should be honest, structure should be visible, and form should emerge from the demands of what is being built — not imposed upon it.

Ando's concrete reveals every pour line. Kahn asked what the building wants to be. Scarpa's joints are the ornament. Breuer let the material dictate the form. Together they define a test: is this design built, or is it decorated?

Applied to screen design: are the borders, rules, spacing, type choices, and color structural — expressing the content's real organization — or are they applied surface treatment?

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/materialist                 # Evaluate full site screenshots
/materialist [page-name]     # Evaluate a specific page's screenshot
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

### T1. Does the design reveal its structure or hide it?

Ando's buildings show the construction. Kahn's concrete reveals the formwork. Look at the page: can you see how it is built? Are the layout mechanics — the grid, the hierarchy, the sectioning — visible and honest? Or is the structure concealed behind seamless surfaces and smooth gradients that hide the joints?

### T2. Are borders, rules, and spacing structural or decorative?

Scarpa's metalwork was both joint and ornament — the connection between materials became the detail. Look at every visual element that separates, contains, or organizes content. Is each one doing structural work (dividing real sections, establishing real hierarchy) or is it decorative (adding visual interest where no structural need exists)?

### T3. Do the materials feel honest?

The materials of screen design are type, color, and space. Breuer chose materials for their inherent properties, not for what they could be made to imitate. Does the typography feel chosen for its structural qualities (legibility, weight, texture) or for stylistic effect? Does the color serve information or mood? Does the whitespace create breathing room, or is it filling a void?

### T4. Is the form derived from the content's needs, or imposed on it?

Kahn's question: "What does the building want to be?" Applied here: does the layout emerge from what the content requires — its hierarchy, its density, its rhythm — or was a visual template applied regardless of what the content actually demands? Look for moments where the design bends to serve the content versus moments where the content was shaped to fit the design.

## Output

Print in conversation. No file changes. Format:

```
# Materialist Lens — "Is this built or decorated?"

## Overall: [STRUCTURAL / ADEQUATE / DECORATED]

**T1. Structure revealed?** — [verdict]
[Evidence from screenshots.]

**T2. Borders/rules structural?** — [verdict]
[Evidence from screenshots.]

**T3. Honest materials?** — [verdict]
[Evidence from screenshots.]

**T4. Form from content?** — [verdict]
[Evidence from screenshots.]

## The Construction
[One sentence: what is the design's structural logic, or what is it hiding?]
```

### Verdict Scale

- **STRUCTURAL** — the design reveals its construction. Every element does structural work. Materials are honest. Form follows the content's needs.
- **ADEQUATE** — the design is mostly honest but includes decorative elements that don't serve structure. Some imposed form, some earned form.
- **DECORATED** — the design hides its structure behind applied surface treatment. Borders and rules are ornamental. Form is imposed on content rather than derived from it.

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
