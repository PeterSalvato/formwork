---
name: draplin
description: "Draplin lens — Personality-in-craft. Does this feel like a human with opinions made it? Is the brand the person? Read-only diagnostic."
user_invocable: true
---

# Draplin Lens — Atomic Skill

## Purpose

Aaron Draplin's standard: "I'm just a regular dude from the Midwest who likes thick lines and bold type." Draplin's work is inseparable from Draplin the person. The brand is the human — not a strategy, not a persona, but the actual person showing up with actual opinions. This lens evaluates whether the design has genuine personality or is wearing someone else's taste.

Read-only diagnostic. Evaluates screenshots. No file changes.

## Usage

```
/draplin                           # Evaluate all screenshots
/draplin [screenshot-path]         # Evaluate a single screenshot
```

## Context

### Read
- Screenshots from `.audit/screenshots/` (latest set) — REQUIRED. Never evaluate from source code alone.
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set relevant to this lens's domain
- `.audit/rubric.md` if it exists

### Invoke (as needed)
- `/print-craft` → material quality baseline → PRESSED/ADEQUATE/DIGITAL (for texture-related questions)
- `/millman` → personhood context → does the personality in design match content personality?

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Evaluate

### Step 0: Read Screenshots (Mandatory)

Before evaluating ANY question below, use the Read tool to view the screenshot images provided in your prompt. Claude can read PNG files — the Read tool returns visual content.

Read each screenshot path provided. Base ALL evaluations on what you SEE in the screenshots, not on source code, CSS, or documentation. If no screenshot paths were provided, state "NO SCREENSHOTS PROVIDED — cannot evaluate" and stop.

Do NOT fall back to reading SCSS, CSS, or HTML files. The evaluation is of the RENDERED output, not the source.

---

"Personality-in-craft. Does this feel like a human with opinions made it? Is the brand the person?"

For each screenshot, ask:

### D1. Does the design have personality or is it generic?

Could this be any designer's portfolio, or does it look like one specific person made it? Personality shows in choices — the typeface, the color, the density, the things that are intentionally NOT here. A Draplin piece is identifiable at a glance. A template is identifiable as a template.
Flag: Design that follows current trends without adding anything personal. Layout, color, and type choices that could be swapped onto a different person's site without anyone noticing. "Best practices" followed so obediently that the person disappears.

### D2. Does it feel handmade or templated?

Handmade does not mean rough or amateurish. It means someone made specific decisions rather than accepting defaults. You can feel the hand even in a clean, professional design — through idiosyncratic spacing, a color that's slightly off from the expected palette, a layout choice that reveals preference over convention.
Flag: Pixel-perfect adherence to a framework grid with no personal adjustments. Stock photo aesthetic. Design decisions that are correct but never surprising.

### D3. Is the brand inseparable from the person?

If you removed the name, would you still know whose site this is? The design itself should carry identity — not just through a logo, but through the accumulated weight of every visual choice reflecting one person's taste.
Flag: Design that depends entirely on the name or bio to establish identity. Visual language that is professional but anonymous. A site where the "brand" lives in the words, not in the design.

### D4. Does craft reinforce character?

The execution should amplify the personality, not contradict it. If the person is meticulous, the craft should be precise. If the person is bold, the craft should be muscular. Craft and character should be the same thing — not a style applied to content, but content and form emerging from the same sensibility.
Flag: Disconnect between what the site says about the person and how the design feels. Careful, polished execution on content that claims to be bold and experimental. Rough, casual execution on content that claims methodological rigor.

## Output

Print in conversation. No file changes. Format:

```
# Draplin Lens — "Personality-in-craft"

## Overall: [BRANDED / ADEQUATE / GENERIC]

**D1. Personality or generic?** — [observation]
[Evidence from screenshots. What feels personal, what feels default.]

**D2. Handmade or templated?** — [observation]
[Evidence. Specific choices that show a hand, or lack thereof.]

**D3. Brand inseparable from person?** — [observation]
[Evidence. Whether identity lives in the design or only the words.]

**D4. Craft reinforces character?** — [observation]
[Evidence. Alignment or disconnect between personality and execution.]
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
