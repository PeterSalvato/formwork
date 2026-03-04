---
name: lubalin
description: "Lubalin lens — Typography as idea. Is the type doing something, not just labeling? Irreverence with purpose. Read-only diagnostic."
user_invocable: true
---

# Lubalin Lens — Atomic Skill

## Purpose

Herb Lubalin's standard: type is not a vehicle for words — type IS the idea. Lubalin made letterforms think, joke, argue, and provoke. The ampersand in Mother & Child is pregnant. The word "Families" tears itself apart. This lens evaluates whether typography is being used conceptually — carrying meaning beyond its literal content — or merely setting words in a typeface.

Read-only diagnostic. Evaluates screenshots. No file changes.

## Usage

```
/lubalin                           # Evaluate all screenshots
/lubalin [screenshot-path]         # Evaluate a single screenshot
```

## Context

### Read
- Screenshots from `.audit/screenshots/` (latest set) — REQUIRED. Never evaluate from source code alone.
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set relevant to this lens's domain
- `.audit/rubric.md` if it exists

### Invoke (as needed)
- `/print-craft` → material quality baseline → PRESSED/ADEQUATE/DIGITAL (for texture-related questions)
- `/spiekermann` → type craft baseline → is the conceptual type also well-crafted?

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Evaluate

### Step 0: Read Screenshots (Mandatory)

Before evaluating ANY question below, use the Read tool to view the screenshot images provided in your prompt. Claude can read PNG files — the Read tool returns visual content.

Read each screenshot path provided. Base ALL evaluations on what you SEE in the screenshots, not on source code, CSS, or documentation. If no screenshot paths were provided, state "NO SCREENSHOTS PROVIDED — cannot evaluate" and stop.

Do NOT fall back to reading SCSS, CSS, or HTML files. The evaluation is of the RENDERED output, not the source.

---

"Typography as idea. Is the type doing something innovative, not just labeling? Irreverence with purpose."

For each screenshot, ask:

### L1. Is typography being used conceptually or just functionally?

Functional typography sets words so they can be read. Conceptual typography makes the setting itself carry meaning — through scale, position, breakage, overlap, negative space, or relationship between letterforms. Not every page needs conceptual type, but a design portfolio should show evidence that the designer sees type as a medium, not just a tool.
Flag: Every typographic choice is safe and functional with no moment where type carries meaning beyond legibility. Headings that are just larger body text. Type that serves only as a label for content rather than participating in the communication.

### L2. Does the type communicate beyond its literal content?

Does the way the type is set tell you something the words alone don't? Speed, tension, calm, authority, intimacy, playfulness — these can all live in the typography before a single word is read. Lubalin's layouts communicated feeling before meaning.
Flag: Typography that is emotionally neutral — correctly set but conveying nothing beyond the words. Every page feels the same typographically regardless of content. No variation in typographic tone to match subject matter.

### L3. Is there wit in the letterforms or layout?

Wit does not mean humor — it means intelligence made visible. A clever relationship between word and form. A layout that makes you see the content differently because of how it's arranged. Lubalin found wit in ligatures, in negative space, in the way letters could become images.
Flag: This is a high bar. Most professional design is competent without being witty. The absence of wit is not a failure — but its presence is a significant strength. Note: wit forced or applied as decoration is worse than no wit at all.

### L4. Does irreverence serve the concept?

Lubalin broke typographic rules constantly — but always in service of an idea. Breaking convention without purpose is just sloppiness. Breaking convention because the idea demands it is design thinking. This question asks whether any rule-breaking in the typography is purposeful.
Flag: Conventional typography where a conceptual moment was available but missed. Rule-breaking that's decorative rather than communicative (stretched type, distorted letterforms, or unusual settings that don't serve meaning). Safe typography on content that's about boldness or experimentation.

## Output

Print in conversation. No file changes. Format:

```
# Lubalin Lens — "Typography as idea"

## Overall: [INVENTIVE / FUNCTIONAL / DECORATIVE]

**L1. Conceptual or functional?** — [observation]
[Evidence from screenshots. Where type carries meaning, or doesn't.]

**L2. Communicates beyond words?** — [observation]
[Evidence. Typographic tone and whether it adds to content.]

**L3. Wit in letterforms or layout?** — [observation]
[Evidence. Specific moments of intelligence, or their absence.]

**L4. Irreverence serves concept?** — [observation]
[Evidence. Rule-breaking assessed for purpose or lack thereof.]
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
