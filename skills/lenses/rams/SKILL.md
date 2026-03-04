---
name: rams
description: "Rams lens — Economy. Is everything earning its place? As little design as possible. Read-only diagnostic."
user_invocable: true
---

# Rams Lens — Atomic Skill

## Purpose

Dieter Rams's standard: "Good design is as little design as possible." Not minimalism as aesthetic — economy as principle. Every element must justify its existence. If it can be removed without loss, it should be removed. This lens evaluates whether the design is honest about what it is and whether everything visible is earning its place.

Read-only diagnostic. Evaluates screenshots. No file changes.

## Usage

```
/rams                              # Evaluate all screenshots
/rams [screenshot-path]            # Evaluate a single screenshot
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

"Economy. Is everything earning its place? Is it as little design as possible?"

For each screenshot, ask:

### R1. Does every element serve a purpose?

Walk through each visible element — headings, images, decorative lines, icons, whitespace blocks, navigation items, labels. For each one: what does it do? If the answer is "it looks nice" without a functional or communicative role, it's suspect.
Flag: Decorative elements that carry no information. Redundant labels (an icon AND a label AND a tooltip all saying the same thing). Visual elements present because the layout "needed something there."

### R2. Could anything be removed without loss?

The subtraction test. Mentally remove each element and ask: does the page lose anything meaningful? A well-designed page has nothing left to take away. Rams called this "back to purity, back to simplicity."
Flag: Elements that survive the subtraction test — meaning the page works fine without them. Hover effects, animations, or transitions that add motion without meaning. Footer content that no one reads.

### R3. Is there visual noise?

Noise is anything that competes for attention without earning it. Borders around things that don't need containing. Drop shadows on elements that don't need depth. Background textures that don't serve legibility. Color variations that don't carry meaning.
Flag: Borders, shadows, or effects used as default styling rather than intentional communication. Multiple competing visual patterns. Inconsistent use of decorative elements (some sections have them, some don't, for no clear reason).

### R4. Is it honest about what it is?

Rams's principle of honesty: "Good design does not make a product more innovative, powerful, or valuable than it really is." Applied to a portfolio: does the design represent the work accurately? Does it inflate, obscure, or misrepresent? The visual treatment should match the substance.
Flag: Design polish that exceeds the content's maturity. Impressive visual treatment on thin content. Effects or interactions that suggest more depth than exists. Conversely: raw or unfinished presentation of mature, substantial work.

## Output

Print in conversation. No file changes. Format:

```
# Rams Lens — "As little design as possible"

## Overall: [ESSENTIAL / ADEQUATE / EXCESSIVE]

**R1. Every element earns its place?** — [observation]
[Evidence from screenshots. Elements identified, purpose assessed.]

**R2. Subtraction test** — [observation]
[Evidence. What could be removed, what's essential.]

**R3. Visual noise** — [observation]
[Evidence. Specific noise identified or absence noted.]

**R4. Honest about what it is?** — [observation]
[Evidence. Whether design treatment matches substance.]
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
