---
name: audit
description: "Site audit coordinator — dispatches baseline checks, then evaluative lenses in parallel. Coordinator skill."
user_invocable: true
---

# Site Audit — Coordinator Skill

## Purpose

Evaluate a site or portfolio in layers: visual inspection, mechanical baseline checks, then evaluative lenses dispatched in parallel. Reports only — never auto-fixes.

This is a coordinator. It dispatches atomic skills, collects their results, and synthesizes. The atomics do the evaluation. This skill handles the orchestration.

## Quick Reference

```
/audit run                    # Full audit: visual + baseline + all lenses
/audit run baseline           # Baseline checks only (dispatches /baseline)
/audit run [lens]             # Single lens (millman, bierut, appleton, peers, etc.)
/audit check [page]           # All checks scoped to one target
/audit report                 # Show last saved report
```

## Context

### Read
- Project vision document (what the site is trying to be)
- Architecture document (intended IA structure)
- All published pages (frontmatter + body)
- Screenshots (if available — visual lenses need rendered output, not source)
- Reference images (if the project has a visual reference set)

### Invoke
- `/baseline` → mechanical health → pass/fail per check
- `/millman` → personhood → STRONG/HOLDS/WEAK/BROKEN + direction
- `/bierut` → design thinking → STRONG/HOLDS/WEAK/BROKEN + direction
- `/appleton` → living knowledge → STRONG/HOLDS/WEAK/BROKEN + direction
- `/peers` → peer benchmark → STRONG/HOLDS/WEAK/BROKEN + direction
- `/copy-verify` → voice spot-check → pass/fail per item
- `/grip-test` → copy landing → Fingernail/Grip/Lock
- Additional lenses as configured for the project

## Dispatch: `/audit run`

### Layer 0: Visual Evaluation (recommended)

Visual inspection improves evaluation quality. Design lenses cannot fully evaluate from markdown source alone.

**0.1 Screenshots**
Take screenshots of every published page at 3 viewports (375px, 768px, 1440px) using Playwright or equivalent.

**0.2 Visual Assessment**
Read every screenshot as an image. Evaluate: typography hierarchy, whitespace, visual weight, layout coherence across viewports.

**0.3 First Visitor Walkthrough**
1. Read homepage first 3 paragraphs
2. Report: what does a first-time visitor understand in 30 seconds?
3. Navigate 2 more pages as a new visitor would
4. Report the emotional arc: trust, curiosity, or confusion?

### Layer 1: Baseline (sequential — lenses depend on this)

Dispatch `/baseline` atomic skill. Mechanical checks:
- Links resolve
- Images exist
- Cross-references hold
- Attribution chain intact
- Voice violations caught
- SEO metadata present
- Navigation functional

Baseline results inform lens evaluations (e.g., Appleton needs tooltip/linking results, Bierut needs accessibility data).

### Layer 2: Lenses (all in parallel)

After baseline completes, dispatch all configured lenses simultaneously using the Agent tool:

1. `/millman` — Is this person real? (M1-M5)
2. `/bierut` — Does the design think? (B1-B5)
3. `/appleton` — Is the knowledge alive? (A1-A5)
4. `/peers` — Peer benchmark (PB1-PB5)
5. `/copy-verify` — Voice check on sample pages

Add or remove lenses based on the project's needs. The pattern is the same: each lens reads the same material independently and returns its own verdict.

### Layer 3: Synthesis

After all lenses return:

1. Collect verdicts and key findings
2. Cross-reference: do lenses agree or contradict?
3. Generate the report with all verdicts and evidence
4. Save report to a timestamped file
5. Print full report in conversation

## Report Format

```
# Site Audit — [DATE]

## Baseline
[NUMBER] checks passed. [NUMBER] failed.
[List each failure with file path and specific issue]

## Millman — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings — M1-M5 verdicts with evidence]

## Bierut — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings — B1-B5]

## Appleton — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings — A1-A5]

## Peer Benchmark — [STRONG/HOLDS/WEAK/BROKEN]
[Key findings — PB1-PB5]

## Limitations
- Visual evaluation is Claude's reading as a multimodal viewer, not expert design critique
- First-visitor walkthrough is a proxy, not user testing
- Voice checking catches pattern-matchable violations only
- These are Claude's interpretations of the frameworks, not the original authors' evaluations
```

## Customization

The audit coordinator is designed to be extended:
- Add project-specific lenses (identity lenses, domain-specific diagnostics)
- Configure which lenses run for different audit scopes
- Add a rubric file for maker annotations that override default criteria
- Feed audit results into a convergence skill to map agreements and contradictions

## Notes

- Reports only. Never auto-fix.
- Verdicts, not scores. STRONG/HOLDS/WEAK/BROKEN forces judgment.
- Always state limitations.
- The maker's annotations override defaults when a rubric exists.
