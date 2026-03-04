---
name: convergence
description: "Where lenses agree and disagree. Maps consensus vs. contradiction across audit results. Read-only diagnostic."
user_invocable: true
---

# Convergence — Atomic Skill

## Purpose

Takes audit results (all 9 content lens verdicts + findings, including The Walk and The Walls) and maps consensus vs. contradiction. Where 5+ lenses flag the same page or element, that's high-confidence signal. Where 2 lenses disagree on the same element, that's a decision point the maker needs to see.

This is a meta-evaluation. It doesn't look at the site directly — it looks at how the lenses see the site. No individual lens catches cross-lens patterns. This one does.

Read-only diagnostic. No file changes.

## Usage

```
/convergence                # Requires audit results as input
```

## Context

### Read
- Audit results from `/audit run` — all 9 content lens verdicts (baseline, millman, bierut, appleton, shaw, peers, victore, the-walk, the-walls) with their per-page findings and evidence
- If running inside `/steward run`, receive audit results from the steward's parallel dispatch output

### Invoke (as needed)
None. This skill reads audit output — it doesn't re-run lenses.

### Lens Criteria (embedded)
Not a lens itself. Evaluates the agreement/disagreement patterns across lens outputs.

## Evaluate

For each published page, collect all lens findings that reference that page. Then:

1. **Consensus check:** Where do 5+ lenses agree? (e.g., 5 lenses flag Colophon as underperforming → high-confidence signal that Colophon needs work)
2. **Contradiction check:** Where do 2+ lenses disagree on the same element? (e.g., Millman says the personal voice is STRONG on a page but Shaw says the world-feel is WEAK → the personality is there but the room isn't built)
3. **Invisible pages:** Pages that no lens flagged positively or negatively — they're invisible to evaluation, which usually means they're invisible to visitors too
4. **Verdict clustering:** Which pages cluster around the same verdict level? Are all Governance pages STRONG while all Output pages are HOLDS? That's a tier-level pattern.
5. **Decision points:** For each contradiction, articulate what's at stake. When Victore says "be braver" and Peers says "this is already strong," the maker needs to decide which lens to favor for that specific element.

## Output

Print in conversation. No file changes. Format:

```
# Convergence — [CONVERGENT / MIXED / CONTRADICTORY]

## High-Confidence Signals (5+ lenses agree)
[Per-page or per-element: what the lenses agree on, and what that means]

## Decision Points (lenses disagree)
For each contradiction:
- **Page/Element:** [what]
- **Lens A says:** [verdict + reasoning]
- **Lens B says:** [verdict + reasoning]
- **What's at stake:** [what the maker loses by favoring A vs. B]

## Invisible Pages
[Pages with no strong signal in any direction — evaluation blind spots]

## Tier Patterns
[Do verdicts cluster by tier? By page type? Any systemic patterns?]

## Verdict Map
| Page | Millman | Bierut | Appleton | Shaw | Peers | Victore | Walk | Walls | Consensus |
|------|---------|--------|----------|------|-------|---------|------|-------|-----------|
| [page] | [verdict] | ... | ... | ... | ... | ... | ... | ... | [agree/split/silent] |
```

## Direction (if not all passing)

For each decision point:
- What specifically is in tension (with evidence from both lenses)
- What the maker gains by favoring Lens A (and what he loses)
- What the maker gains by favoring Lens B (and what he loses)
- A recommendation IF one lens clearly aligns with the positioning intent ("desirable because interesting and unavailable")

## Called By

- `/steward run` — Step 3.5, runs sequentially AFTER audit returns (needs audit output as input)
- Standalone — if audit results are available from a recent report in `.audit/reports/`
