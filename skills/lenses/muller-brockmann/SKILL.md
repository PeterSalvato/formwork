---
name: muller-brockmann
description: "Muller-Brockmann lens — The grid. Is the system visible? Does structure create order from complexity? Read-only diagnostic."
user_invocable: true
---

# Muller-Brockmann Lens — Atomic Skill

## Purpose

Josef Muller-Brockmann's standard: the grid is not a straitjacket but a framework for bringing order to complexity. Mathematical precision in service of communication. Every element positioned with reason, every relationship intentional. This lens evaluates whether the visual design operates on a visible system, or whether its order is arbitrary.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/muller-brockmann            # Evaluate full site screenshots
/muller-brockmann [page-name] # Evaluate a specific page's screenshot
```

## Context

### Read
- Screenshots from `.audit/screenshots/` (latest set) — REQUIRED. Never evaluate from source code alone.
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set relevant to this lens's domain
- `.audit/rubric.md` if it exists

### Invoke (as needed)
- `/print-craft` → material quality baseline → PRESSED/ADEQUATE/DIGITAL (for texture-related questions)
- `/vignelli` → restraint context → are grid decisions serving clarity?

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Evaluate

### Step 0: Read Screenshots (Mandatory)

Before evaluating ANY question below, use the Read tool to view the screenshot images provided in your prompt. Claude can read PNG files — the Read tool returns visual content.

Read each screenshot path provided. Base ALL evaluations on what you SEE in the screenshots, not on source code, CSS, or documentation. If no screenshot paths were provided, state "NO SCREENSHOTS PROVIDED — cannot evaluate" and stop.

Do NOT fall back to reading SCSS, CSS, or HTML files. The evaluation is of the RENDERED output, not the source.

---

For each screenshot (or the set as a whole), ask:

### M1. Is there a visible grid system?

Look at the underlying structure. Can you see — or infer — a grid governing the placement of elements? Are columns consistent? Do margins and gutters repeat? Muller-Brockmann's concert posters used the grid to organize chaos into clarity. Does this design show evidence of a governing spatial system, or are elements placed by eye?

### M2. Do elements align to a consistent baseline?

Check text blocks, images, headings, and spacing. Do they share a common rhythmic structure — a baseline grid, a modular scale, repeating vertical intervals? Or does the vertical rhythm drift, with spacing that feels improvised rather than measured?

### M3. Does the structure handle complex content gracefully?

The grid earns its value when content is dense or varied. Look at pages with mixed content types — text, images, lists, headings, metadata. Does the structure absorb this complexity and make it legible? Or does the system break down when content becomes challenging?

### M4. Is the order mathematical or arbitrary?

Muller-Brockmann's layouts were proportional, often based on geometric ratios. Look at the relationships between elements: are widths, heights, and spacing related by proportion, or do they feel like round numbers chosen for convenience? Mathematical order reveals itself in the harmony between parts.

## Output

Print in conversation. No file changes. Format:

```
# Muller-Brockmann Lens — "The grid."

## Overall: [SYSTEMATIC / ADEQUATE / ARBITRARY]

**M1. Visible grid system?** — [verdict]
[Evidence from screenshots.]

**M2. Consistent baseline?** — [verdict]
[Evidence from screenshots.]

**M3. Complex content handled?** — [verdict]
[Evidence from screenshots.]

**M4. Mathematical or arbitrary?** — [verdict]
[Evidence from screenshots.]

## The System
[One sentence: describe the grid logic observed, or its absence.]
```

### Verdict Scale

- **SYSTEMATIC** — a visible, consistent grid governs the layout. Proportional relationships are evident. The structure creates order from complexity.
- **ADEQUATE** — alignment and spacing are generally consistent but the system is not rigorous. Order exists without mathematical precision.
- **ARBITRARY** — no discernible grid system. Element placement feels improvised. Spacing and alignment are inconsistent.

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
