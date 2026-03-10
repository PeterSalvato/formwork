---
name: throughline
description: "Single-page narrative evaluation — does this page carry a reader from opening to closing? Read-only diagnostic."
user_invocable: true
---

# Throughline — Atomic Skill

<!-- SKILL DESIGN RATIONALE: Blog posts and project pages were passing voice protocol checks
     (zero em dashes, no fortune-cookie closers, earned negation-affirmation) and landing
     strong openings (confirmed by grip-test), but 4 of 7 blog posts failed as storytelling.
     They read like documentation with good openings bolted on. The technical posts especially
     shifted from narrative to reference material mid-page, and no existing skill caught that.

     Grip-test evaluates the first 2-3 paragraphs. Copy-verify is a mechanical checklist.
     Arc evaluates cross-page coherence. The Walk evaluates example sequence positioning.
     None of them evaluate: does this page, as a self-contained unit, hold a reader's
     attention from opening to closing? That's the gap this skill fills. -->

## Purpose

Evaluate whether a single page carries a reader from opening to closing as a self-contained narrative unit. Identifies where the narrative breaks, where attention drifts, and whether the page works for all three target audiences (creatives, engineers, strangers).

Read-only diagnostic. No file changes.

## Usage

```
/throughline [page-path]       # Evaluate a specific page
/throughline [url-path]        # Evaluate by URL path (e.g., /blog/persona-extraction)
```

## Context

### Read
- Target page content (full body text, not just opening)
- `CONTENT-STRATEGY.md` — narrative arc context (where this page sits in the blog sequence)
- `docs/NARRATIVE-ARCHITECTURE.md` — tier altitude and framing expectations

### Invoke (as needed)
- `/grip-test` → opening diagnostic (if not already run in the same coordinator pass)

### Lens Criteria (embedded)
The six evaluation criteria below (T1-T6) are this skill's diagnostic.

## Evaluate

<!-- WHY 6 CRITERIA: Each maps to a distinct failure mode observed in real blog posts.
     T1 catches listing-not-building (the-system post). T2 catches dead transitions
     (persona-extraction at the M1-M5 boundary). T3 catches documentation blocks mid-story
     (voice-governance 12-item checklist). T4 catches pacing death (persona-extraction
     V1-V5 stretch). T5 catches disconnected endings (why-does-my-brain). T6 catches
     audience-specific bounce points (the-system loses non-engineers). -->

### T1. Does it build?

Read the page section by section. Does each section earn the next? Or does the page list things in sequence without any section depending on or building from what came before?

**Test:** Could you rearrange the middle sections without the reader noticing? If yes, it lists. If rearranging would break the logic, it builds.

**Verdict:** BUILDS / LISTS

### T2. Does it hold past each break?

Identify every section break (heading, horizontal rule, whitespace). At each break, would a stranger keep reading? A strong transition creates a question the reader wants answered, a tension that hasn't resolved, or a promise that hasn't paid off yet. A weak transition is a topic change.

**Test:** Read the last sentence before each break and the first sentence after. Is there a thread connecting them, or does the reader have to re-engage from scratch?

**Verdict:** YES / PARTIAL / NO
**Report:** The weakest transition (quote the last line before and first line after).

### T3. Does technical content stay grounded?

When the page explains something (a process, a system, a methodology), does it stay connected to the narrative frame? Or does it shift register into documentation mode: numbered steps, criteria lists, architecture descriptions, definition blocks?

Technical content mid-story needs a narrative anchor: a specific incident, a before/after, a consequence, a person affected.

<!-- WHY 3 PARAGRAPHS: The threshold is calibrated to the actual failure pattern.
     Two paragraphs of exposition is normal pacing. Three consecutive paragraphs
     without a narrative beat is where readers start skimming in user testing.
     This is a practical threshold, not a theoretical one. -->

**Flag:** Any section longer than 3 paragraphs that contains no specific incident, person, consequence, or before/after. That is a documentation block wearing a blog post's clothes.

**Verdict:** GROUNDED / DRIFTS / DOCUMENTATION

### T4. Is pacing varied?

Do long explanatory stretches alternate with shorter, punchier moments? Three consecutive paragraphs of exposition without a narrative beat (a moment, a quote, a specific detail, a shift in register) is a pacing problem.

**Test:** Mark each paragraph as E (explanatory/expository) or N (narrative/concrete moment). If you see E-E-E-E without an N, that is a dead stretch.

**Verdict:** VARIED / FLAT / DEAD STRETCHES

### T5. Does the opening promise connect to the closing?

What does the opening set up? Does the closing pay it off? The opening raises a question or tension, the middle explores it, and the closing resolves or reframes it. The reader should feel the closing connect back to the opening.

**Test:** Read only the first two paragraphs and the last two paragraphs. Does the closing feel like it belongs to the same piece as the opening? Or could it close a different essay?

**Verdict:** COMPLETE / PARTIAL / OPEN

### T6. Does it work for all three audiences?

<!-- WHY THREE AUDIENCES: These are the three audiences defined in the site's positioning
     strategy. Creatives want to see the thinking. Engineers want to see the system.
     Strangers (via LinkedIn/search) want to feel the problem. A page that serves only
     one loses two-thirds of its potential readers. -->

Peter's three audiences need different things from the same page:
- **Creatives** want to see the thinking, the process, the real decisions
- **Engineers** want to see the system, the architecture, the technical choices
- **Strangers** (via LinkedIn, search) want to feel the problem before they care about the solution

A page that goes deep into system architecture without narrative framing loses the creatives and strangers. A page that stays purely anecdotal loses the engineers.

**Test:** Read the page as each audience in turn. Where would a creative check out? Where would an engineer check out? Where would a LinkedIn stranger check out? If two or more audiences bounce at the same section, that section is the structural weak point.

**Verdict:** ALL THREE / TWO OF THREE / ONE

## Overall Verdict

<!-- WHY THIS SCALE: Four points, not three. HOLDS and DRIFTS describe two different
     failure severities that require different revision approaches. HOLDS means tighten
     (transitions, pacing). DRIFTS means restructure (the narrative spine is broken).
     The vocabulary uses Peter's material register: carries (load-bearing), holds,
     drifts, stalls. -->

Based on T1-T6, rate the page:

- **CARRIES** — The page carries a reader from opening to closing. Each section earns the next. A stranger who starts reading finishes reading.
- **HOLDS** — The page holds together but has slack. One or two sections where attention could drift. The structure works but pacing or transitions need tightening.
- **DRIFTS** — The page drifts into reference material, documentation, or listing mid-story. The opening promises narrative but the middle delivers something else. A stranger bounces at a specific, identifiable point.
- **STALLS** — The page stalls. No forward motion. Sections feel like separate documents. The opening and closing don't connect. A stranger leaves.

## Output

Print in conversation. No file changes. Format:

```
# Throughline — [page name]

## Verdict: [CARRIES / HOLDS / DRIFTS / STALLS]

## T1. Does it build? — [BUILDS / LISTS]
[Evidence. Name the section sequence and whether each earns the next.]

## T2. Holds past breaks? — [YES / PARTIAL / NO]
**Weakest transition:** [Section A] → [Section B]
[Quote the last line before and first line after. Why it's weak.]

## T3. Technical content grounded? — [GROUNDED / DRIFTS / DOCUMENTATION]
**Drift point:** [section heading or paragraph where it shifts]
[What narrative anchor is missing.]

## T4. Pacing varied? — [VARIED / FLAT / DEAD STRETCHES]
**Longest dead stretch:** [section, paragraph count of consecutive exposition]
[What narrative beat would break it up.]

## T5. Opening-closing circuit? — [COMPLETE / PARTIAL / OPEN]
**Opening promise:** [one sentence]
**Closing delivery:** [one sentence]
[Does the circuit close?]

## T6. Three audiences? — [ALL THREE / TWO OF THREE / ONE]
**Creatives bounce at:** [section or "holds"]
**Engineers bounce at:** [section or "holds"]
**Strangers bounce at:** [section or "holds"]

## The Drift Point
[The single most specific place where a stranger's attention would leave.
Not "the middle." The exact section, the exact transition, the exact paragraph.
This is the surgical target for revision.]
```

## Direction (if not CARRIES)

For the drift point and any non-passing criteria, state:
- What specifically is wrong (with evidence from the text)
- What specifically to change (exact structural revision, not "improve the pacing")
- What the result should accomplish (what the reader should feel at that point)

## Called By

- `/copy edit` — Step 7.25 (after copy-verify, before the-walk)
- `/copy write` — Step 7.5 (after verify)
- `/copy review` — Step 4.5 (after copy-verify per page, added to summary table)
- Standalone — usable anytime to evaluate a page's narrative structure

---

## Rationale — Why This Skill Works This Way

### The Problem

Blog posts and project pages pass voice protocol checks and have strong openings but lose a stranger mid-way because they shift from narrative to reference material. The technical posts especially (persona extraction, voice governance, the integrated system) have the same pattern: a compelling opening (confirmed by grip-test at Grip or Lock), then a documentation block (criteria lists, architecture diagrams, numbered steps) that breaks the narrative spell. No existing skill evaluates the narrative spine of a single page.

### Why This Approach

Six criteria, each mapping to a distinct failure mode observed in real posts. The criteria are sequenced from macro (does it build?) to micro (does pacing vary?), ending with the audience check (does it work for everyone?). The Drift Point output forces a single surgical finding rather than a laundry list, because revision is more effective when you know exactly where to cut.

### Key Tradeoffs

- **6 criteria, not more.** T6 (audience check) could be split into three separate checks, but that would make the output unwieldy for a fast diagnostic. One question that names all three audiences is more useful than three separate audience evaluations.
- **4-point scale, not 3.** HOLDS and DRIFTS describe two different failure severities. HOLDS means tighten (adjust transitions, vary pacing). DRIFTS means restructure (the narrative spine is broken and needs a different architecture). Collapsing those into one verdict would lose actionable information.
- **No emotional arc evaluation.** The skill evaluates structural hold (does the reader keep reading?) but not emotional arc (does the reader feel progressively more?). Emotional evaluation is subjective and harder to make actionable. Structural hold is the more urgent gap.

### What Could Improve

- Emotional arc could become a future extension or separate skill if needed.
- The 3-paragraph threshold for T3 is calibrated to blog posts. Longer-form pages (project writeups, governance docs) might need a different threshold. Could add a `--long-form` flag if this becomes an issue.
- Could integrate with `/speed-tiers` to evaluate whether the throughline works at different reading speeds (10-second scan vs. 2-minute read vs. full read).
