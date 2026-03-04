---
name: spiekermann
description: "Spiekermann lens — Typography craft. Spacing, hierarchy, micro-details, font pairing. Read-only diagnostic."
user_invocable: true
---

# Spiekermann Lens — Atomic Skill

## Purpose

Erik Spiekermann's standard: "Typography is two-dimensional architecture, based on experience and imagination." This lens evaluates the craft of typography — not what the type says, but how it's set. Spacing, rhythm, pairing, hierarchy, and the micro-details that separate professional typography from default settings.

Read-only diagnostic. Evaluates screenshots. No file changes.

## Usage

```
/spiekermann                       # Evaluate all screenshots
/spiekermann [screenshot-path]     # Evaluate a single screenshot
```

## Context

### Read
- Screenshots from `.audit/screenshots/` (latest set) — REQUIRED. Never evaluate from source code alone.
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set relevant to this lens's domain
- `.audit/rubric.md` if it exists

### Invoke (as needed)
- `/print-craft` → material quality baseline → PRESSED/ADEQUATE/DIGITAL (for texture-related questions)
- `/vignelli` → restraint context → DISCIPLINED/ADEQUATE/UNDISCIPLINED

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Evaluate

### Step 0: Read Screenshots (Mandatory)

Before evaluating ANY question below, use the Read tool to view the screenshot images provided in your prompt. Claude can read PNG files — the Read tool returns visual content.

Read each screenshot path provided. Base ALL evaluations on what you SEE in the screenshots, not on source code, CSS, or documentation. If no screenshot paths were provided, state "NO SCREENSHOTS PROVIDED — cannot evaluate" and stop.

Do NOT fall back to reading SCSS, CSS, or HTML files. The evaluation is of the RENDERED output, not the source.

---

"Typography craft. Is the spacing right? Is the hierarchy clear? Do the details sing?"

For each screenshot, ask:

### S1. Letter-spacing consistency

Is letter-spacing intentional and consistent? Headings, body text, and captions each demand different tracking. Default letter-spacing is almost never correct — especially at display sizes.
Flag: Display type with default tracking (usually too tight or too loose at large sizes). Inconsistent spacing between similar elements. ALL-CAPS text without opened tracking.

### S2. Line-height comfort

Does the line-height support comfortable reading? Body text needs air; display type can be tighter. The test is whether you can read a full paragraph without losing your place or feeling cramped.
Flag: Body text with line-height below 1.4 or above 1.8 (both impair reading). Display type with body-text line-height (looks loose and disconnected). Inconsistent line-height across similar text blocks.

### S3. Font pairing harmony

If multiple typefaces are used, do they complement each other? Good pairing creates contrast with coherence — different enough to distinguish roles, similar enough to feel like one design.
Flag: Fonts that clash in personality (geometric sans with an ornate serif, for example, without conceptual justification). More than two or three typefaces. Pairings that are too similar to justify using two fonts.

### S4. Typographic hierarchy readability

Can you instantly tell what to read first, second, third? The hierarchy should be scannable — a reader who glances at the page for two seconds should understand the information architecture.
Flag: Competing elements at the same visual weight. Hierarchy achieved only through size (no weight, spacing, or position variation). Hierarchy that requires reading to understand rather than being visually immediate.

### S5. Micro-typography details

The details that separate craft from default: hanging punctuation, optical alignment (where mathematically centered text looks off-center), proper quote marks versus straight quotes, em-dashes versus hyphens, oldstyle figures versus lining figures in context.
Flag: Straight quotes where curly quotes belong. Hyphens used as dashes. Text that looks mathematically aligned but optically wrong. Missing attention to typographic niceties that indicate care.

## Output

Print in conversation. No file changes. Format:

```
# Spiekermann Lens — "Typography craft"

## Overall: [CRAFTED / ADEQUATE / ROUGH]

**S1. Letter-spacing** — [observation]
[Evidence from screenshots. Specific elements noted.]

**S2. Line-height** — [observation]
[Evidence. Reading comfort assessment.]

**S3. Font pairing** — [observation]
[Evidence. Fonts identified, relationship evaluated.]

**S4. Hierarchy readability** — [observation]
[Evidence. Scannability assessment.]

**S5. Micro-typography** — [observation]
[Evidence. Specific details observed or missing.]
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
