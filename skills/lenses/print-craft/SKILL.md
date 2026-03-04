---
name: print-craft
description: "Print Craft lens — Does it feel printed? Scored against the maker's actual print work as the benchmark. Read-only diagnostic."
user_invocable: true
---

# Print Craft Lens — Atomic Skill

## Purpose

The print-craft lens evaluates whether the site achieves the material qualities of a printed artifact — not by abstract principles, but by direct comparison to the maker's actual print work. Each question maps to a specific reference image from the visual reference index.

The benchmark isn't "does this look like print" in general. It's "does this achieve the specific character visible in the Stoicism series, New City posters, P mark, and Aetherwright sigil?" Those pieces define what "printed" means for this site.

Read-only diagnostic. Reports a verdict, never auto-fixes.

## Usage

```
/print-craft                 # Evaluate full site screenshots
/print-craft [page-name]     # Evaluate a specific page's screenshot
```

## Context

### Read
- Screenshots from `.audit/screenshots/` (latest set) — REQUIRED
- `docs/visual-reference-index.md` → active reference set
- All reference images from active set (this lens compares against every dimension)
- `.audit/rubric.md` if it exists

### Invoke (as needed)
- `/texture-verify` → texture quality check after generation → PRESSED/OVERWORKED/INVISIBLE/COSTUME
- Reference images are queried per question (each P1-P7 maps to a specific reference)

### Lens Criteria (embedded)
The P1-P7 questions below ARE this lens's criteria. Each maps to a specific reference image.

## Evaluate

### Step 0: Read Screenshots (Mandatory)

Before evaluating ANY question below, use the Read tool to view the screenshot images provided in your prompt. Claude can read PNG files — the Read tool returns visual content.

Read each screenshot path provided. Base ALL evaluations on what you SEE in the screenshots, not on source code, CSS, or documentation. If no screenshot paths were provided, state "NO SCREENSHOTS PROVIDED — cannot evaluate" and stop.

Do NOT fall back to reading SCSS, CSS, or HTML files. The evaluation is of the RENDERED output, not the source.

---

For each screenshot (or the set as a whole), ask:

### P1. Paper substrate — Does the background feel like uncoated stock?

**Reference:** `docs/references/print-artifact/EchoAndBone_MementoMori.jpg` — the warm, fibrous paper behind the skull.

Compare the site background against the reference. The background should have:
- Warm tone (not bright white, not gray)
- Micro-texture from the grain overlay (felt as warmth, not seen as pattern)
- The character of French Paper uncoated stock, not laser printer paper

Score: Does the site surface feel like it has material presence, or does it feel like a CSS color value?

### P2. Ink edges — Do rules and borders feel printed?

**Reference:** `docs/references/print-artifact/aetherwright_sigil.svg` — the circle rim with micro-irregular line weight.

Compare the `.dossier-rule` and other structural lines against the reference. Printed rules should have:
- Micro-variation in edge quality (not mathematically perfect)
- Ink pool spots at stress points
- Conviction without perfection

Score: Do the site's horizontal rules feel like ink on paper, or like CSS `border: 1px solid`?

### P3. Press consistency — Same press run across pages?

**Reference:** All reference images share a consistent material quality within their respective bodies of work.

View 4+ pages. Every page should feel like it came off the same press:
- Same grain character on every background
- Same border treatment on every rule
- Same typographic weight and texture
- No page feels like it belongs to a different print job

Score: Could you shuffle these pages and they'd all feel like the same publication?

### P4. Distress authenticity — Earned or applied?

**Reference:** `docs/references/print-artifact/New_City_01_web.jpg` — the barcode elements with silk-screened edge character.

If the site has distressed or irregular elements, compare against the reference. Authentic distress:
- Is irregular (not evenly distributed)
- Is contextual (appears where physical printing would naturally create it)
- Is purposeful (serves composition, not decoration)

Score: Does the distress feel like it came off a press, or like a Photoshop filter was applied?

### P5. Paper grain — Felt, not seen?

**Reference:** `docs/references/print-artifact/EchoAndBone_MementoMori.jpg` — the paper is there but doesn't compete with the illustration.

Evaluate the grain overlay specifically:
- At normal reading distance, is the grain invisible? (correct)
- Does removing the grain mentally make the surface feel colder? (correct)
- Can you see a tiling pattern? (wrong)
- Does the grain create visual noise that competes with content? (wrong)

Score: Is the grain like ambient temperature — unnoticed until it's gone?

### P6. CMYK misregistration — Subtle shift or glitch art?

**Reference:** `docs/references/print-artifact/Printshop_cmyk.png` — the P mark with visible but controlled plate misalignment.

If the site uses any color separation or misregistration effects (currently in the ink-press SVG filter on display type):
- Is the shift subtle (1-2px maximum)?
- Does it read as "multi-plate printing" rather than "broken monitor"?
- Is it applied to display-size type only (where it's visible and intentional)?

If no misregistration effects exist, note this as a gap (the P mark's most distinctive quality is its crosshatch + CMYK shift).

Score: Does any color misregistration feel like a printing process artifact, or like a glitch effect?

### P7. Registration marks — Compositional or decorative?

**Reference:** `docs/references/print-artifact/New_City_03_web.jpg` — barcodes and registration targets placed compositionally.

Evaluate the `.printer-exhaust` elements and any crop marks / registration targets:
- Are they placed where a printer would actually put them? (bottom of page, margins)
- Do they serve a compositional purpose? (anchoring, visual weight)
- Do they feel integral to the page, or pasted on?

Score: Do the registration marks feel like they were on the press plate, or like clip art?

## Output

Print in conversation. No file changes. Format:

```
# Print Craft Lens — "Does it feel printed?"

## Overall: [PRESSED / ADEQUATE / DIGITAL]

**P1. Paper substrate?** — [verdict]
[Evidence from screenshots, compared against Stoicism reference]

**P2. Ink edges?** — [verdict]
[Evidence from screenshots, compared against sigil rim reference]

**P3. Press consistency?** — [verdict]
[Cross-page comparison evidence]

**P4. Distress authenticity?** — [verdict]
[Evidence from screenshots, compared against New City reference]

**P5. Paper grain?** — [verdict]
[Grain overlay assessment]

**P6. CMYK misregistration?** — [verdict]
[Display type treatment assessment, compared against P mark reference]

**P7. Registration marks?** — [verdict]
[Printer-exhaust assessment, compared against New City reference]

## The Impression
[One sentence: does this feel like it came off a press, or like it wishes it had?]

## Gaps
[Specific elements that are still DIGITAL and what they need]
```

### Verdict Scale

- **PRESSED** — The site embodies print craft at the level of the maker's actual work. Textures match the reference character. Consistency is mechanical. Material quality is felt, not seen. The site doesn't reference print — it is a print artifact rendered on screen.
- **ADEQUATE** — Print-inspired qualities are present but some elements don't match the reference character. Some textures feel applied rather than inherent. Some inconsistencies between pages. Moving in the right direction but not there yet.
- **DIGITAL** — The site references print culture superficially or not at all. Comparison against the reference images reveals significant gaps. The material character of the maker's actual work is absent. It feels like a website, not a pressed artifact.

## Direction (if not all passing)

For each non-passing question, state:
- What specifically is wrong (with evidence from screenshots)
- What specifically to change (exact CSS/SCSS/HTML change, not "improve X")
- Which files to modify
- What the result should look like after the change

## Limitations

Claude's visual assessment, not expert critique. Useful as structured feedback against specific references, not authoritative judgment. the maker's eye is the final arbiter.

## Called By

- `/design-review` coordinator — runs in parallel with other visual lenses
- `/texture audit` — provides the baseline verdict
- `/texture pass` — Phase 1 (before) and Phase 4 (after) comparison
- Standalone — usable anytime
