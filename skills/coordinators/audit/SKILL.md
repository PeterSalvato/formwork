---
name: audit
description: "Evaluate the IP constellation — dispatches baseline checks, then 9 lenses in parallel (Millman, Bierut, Appleton, Shaw, Peers, Victore, The Walk, The Walls). Coordinator skill."
user_invocable: true
---

# Constellation Audit — Coordinator Skill

## Purpose

Evaluate Peter's IP constellation (hub site + spoke repos) in layers: visual inspection, mechanical baseline checks, then nine lenses dispatched in parallel. Reports only — never auto-fixes.

## Quick Reference

```
/audit run                    # Full audit: visual + baseline + all 9 lenses
/audit run baseline           # Baseline checks only (dispatches /baseline)
/audit run [lens]             # Single lens (millman, bierut, appleton, shaw, peers, victore, the-walk, the-walls)
/audit check [page-or-repo]   # All checks scoped to one target
/audit rubric                 # Show/create rubric file
/audit report                 # Show last saved report
```

## Discovering the Constellation

- **Hub**: The current project (petersalvato.com)
- **Published pages**: All files in `_governance/`, `_infrastructure/`, `_output/` WITHOUT `published: false`
- **Blog posts**: All files in `_blog/` WITHOUT `published: false`
- **Standalone pages**: `bio/index.md`, `contact.md`, `colophon.md`, `thinking.md`, `vocabulary.md`
- **Homepage**: `_data/index.json` + `_layouts/systemworks.html`
- **Spokes**: Scan `~/homelab/projects/active/` for repos containing a `CNAME` file
- **Navigation**: `_data/navigation.json`

## Context

### Read
- `NORTHSTAR.md` — master vision ("the site is a world, not a résumé"). The audit evaluates against this intent.
- `docs/ARCHITECTURE.md` — intended IA structure (three tiers, user journeys). Baseline checks mechanical health against this.
- `docs/aetherwright-identity-decisions.md` — persona layer (who Peter is)
- All published pages (frontmatter + body)
- Screenshots from `.audit/screenshots/[today's date]/` — if full-pass passed a SCREENSHOT_DIR, use that path
- `docs/visual-reference-index.md` → active reference set
- `.audit/rubric.md` if it exists

### Invoke
- `/baseline` → mechanical health → pass/fail per check
- `/millman` → personhood → STRONG/HOLDS/WEAK/BROKEN + direction
- `/bierut` → design thinking → STRONG/HOLDS/WEAK/BROKEN + direction
- `/appleton` → living knowledge → STRONG/HOLDS/WEAK/BROKEN + direction
- `/shaw` → world feel → STRONG/HOLDS/WEAK/BROKEN + direction
- `/peers` → peer benchmark → STRONG/HOLDS/WEAK/BROKEN + direction
- `/victore` → bravery → Brave/Safe/Performed/Sanitized + direction
- `/the-walk` → example positioning → ONE WORLD/HOLDS/SPLIT/WRONG ROOM + direction
- `/the-walls` → ambient frame → COHERENT/HOLDS/SPLIT/NOISE + direction
- `/copy-verify` → voice spot-check → pass/fail per item
- `/knowledge` → ideation grounding → source-attributed search results

### Lens Criteria (summary)
**M1-M5:** Real person, vulnerability, voice, life-arc, courage
**B1-B5:** Form/content, problem-solving, meaning, content-driven, intellectual
**A1-A5:** Connections, growth, epistemic disclosure, contextual, evolving
**S1-S5:** World immersion, total environment, stranger orientation
**PB1-PB5:** Structure, visual evidence, public output, social proof, distribution
**Victore:** Fierce self vs performing
**W1-W5:** Room per page, sidebar entry, secondary identity leading, governance examples, one world
**F1-F5:** Persistent frame identity, marginalia signal, frame/content agreement, stranger/initiate gradient, ambient density distribution

## Dispatch: `/audit run`

### Layer 0: Visual Evaluation (MANDATORY)

Visual inspection is required. The audit cannot evaluate design lenses by reading markdown source alone.

**0.0 Start Dev Server**
1. Check if `localhost:4000` is reachable
2. If not: `bundle exec jekyll serve --host 0.0.0.0 &`
3. Poll until 200 response
4. If server can't start, note the error and proceed with source-only evaluation — flag as limitation

**0.1 Screenshots**
Take screenshots of every published page at 3 viewports (375px, 768px, 1440px) using Playwright or equivalent. Save to `.audit/screenshots/YYYY-MM-DD/`. Capture all pages, not a sample.

**0.2 Visual Assessment**
Read every screenshot as an image. Evaluate: typography hierarchy, whitespace, visual weight, layout coherence across viewports, visual-content alignment. Note ALL user-facing elements (images, codex strings, glyphs, altitude markers, faculty dots). Compare against previous screenshots if available.

**0.3 First Visitor Walkthrough**
1. Read homepage manifesto first 3 paragraphs
2. Report: what does a first-time visitor understand in 30 seconds? What confuses them?
3. Navigate 2 more pages as a new visitor would
4. Report the emotional arc: trust, curiosity, or confusion?

### Layer 1: Baseline (sequential — lenses depend on this)

Dispatch `/baseline` atomic skill. This runs all mechanical checks:
- 1.1 Links resolve
- 1.2 Images exist
- 1.3 Cross-references hold
- 1.4 Attribution chain
- 1.5 Voice violations
- 1.6 SEO metadata
- 1.7 Vocabulary tooltips functional

Baseline results inform lens evaluations (e.g., Appleton A5 needs tooltip results, Bierut B4 needs vocabulary visibility).

### Layer 1.5: Ideation History Verification

Use `/knowledge` skill to verify copy grounding:
- Search each project by name against ideation history
- Flag projects with no ideation history as potentially ungrounded
- Compare Peter's conversational voice to published voice (for voice source check)

### Layer 2: Lenses (all 9 in parallel)

After baseline completes, dispatch all 9 lenses simultaneously using the Agent tool:

1. `/millman` — Is this person real? (M1-M5)
2. `/bierut` — Does the design think? (B1-B5)
3. `/appleton` — Is the knowledge alive? (A1-A5)
4. `/shaw` — Does this feel like a world? (S1-S5)
5. `/peers` — Peer benchmark (PB1-PB5)
6. `/victore` — Is Peter being fiercely himself?
7. `/the-walk` — Front door to tattoo chair (W1-W5)
8. `/the-walls` — What room does the frame build? (F1-F5)
9. `/copy-verify` — Spot-check voice on a sample of published pages (optional)

Each lens reads the same published material and the rubric independently. Each returns its own verdict: STRONG / HOLDS / WEAK / BROKEN (except Victore which returns Brave / Safe / Performed / Sanitized).

**Screenshot forwarding:** If a SCREENSHOT_DIR was provided (from full-pass), include screenshot paths in the `/shaw` and `/the-walls` agent prompts. Shaw evaluates content and visual world-feel. The Walls evaluates whether ambient frame elements (sidebar, glyphs, codex, typography) build the right room — screenshots are essential for this. Example paths to include: `SCREENSHOT_DIR/laptop/index.png`, `SCREENSHOT_DIR/laptop/encore.png`, `SCREENSHOT_DIR/mobile/index.png`.

### Layer 3: Synthesis

After all lenses return:

1. Collect verdicts and key findings
2. Cross-reference: do lenses agree or contradict?
3. Generate the report with all verdicts and evidence
4. Save to `.audit/reports/YYYY-MM-DD.md`
5. Print full report in conversation

## Report Format

```
# Constellation Audit — [DATE]

## Baseline
[NUMBER] checks passed. [NUMBER] failed.
[List each failure with file path and specific issue]

## Millman — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings from /millman — M1-M5 verdicts with evidence]

## Bierut — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings from /bierut — B1-B5]

## Appleton — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings from /appleton — A1-A5]

## Shaw — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings from /shaw — S1-S5]

## Peer Benchmark — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings from /peers — PB1-PB5]

## Victore — [Brave/Safe/Performed/Sanitized]
[Findings from /victore]

## The Walk — [ONE WORLD/HOLDS/SPLIT/WRONG ROOM]
[Key findings from /the-walk — W1-W5: room per page, sidebar entry, secondary identities, governance examples, one world]

## The Walls — [COHERENT/HOLDS/SPLIT/NOISE]
[Key findings from /the-walls — F1-F5: persistent frame, marginalia signal, frame/content agreement, stranger/initiate gradient, ambient density]

## Limitations
- Visual evaluation is Claude's reading as a multimodal viewer, not expert design critique
- First-visitor walkthrough is a proxy, not user testing
- Voice checking catches pattern-matchable violations only
- These are Claude's interpretations of the frameworks, not the original authors' evaluations
- Peer benchmark is based on publicly visible content, not private work or reputation
```

## `/audit run [lens]`

Dispatches a single lens directly. No baseline, no synthesis — just the lens output.

## `/audit check [target]`

Same checks, scoped to one page or spoke repo. Target can be:
- A file path: `_output/aiden-jae.md`
- A spoke name: `Savepoint.Protocol`
- A URL path: `/infrastructure/encore`

## `/audit rubric`

Read and display `.audit/rubric.md`. If it doesn't exist, create it with starter content. Peter's rubric annotations override default evaluation criteria.

## `/audit report`

Read the most recent file from `.audit/reports/`. If no reports exist, say so.

## Notes

- Reports only. Never auto-fix.
- The rubric is Peter's. His annotations override defaults.
- Verdicts, not scores. STRONG/HOLDS/WEAK/BROKEN forces judgment.
- Always state limitations.
