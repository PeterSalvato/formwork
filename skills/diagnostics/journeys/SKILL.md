---
name: journeys
description: "Visitor path evaluation. Traces 3 specific paths through the site and evaluates whether coherence holds across the sequence. Read-only diagnostic."
user_invocable: true
---

# Journeys — Atomic Skill

## Purpose

Traces 3 specific visitor paths through the site and evaluates whether coherence holds across the sequence. Not "is each page good" but "does the experience build." A page can be individually strong and still break the journey if it doesn't connect to what came before or after.

Read-only diagnostic. No file changes.

## Usage

```
/journeys                # Evaluate all 3 visitor paths
```

## Context

### Read
- All published pages (frontmatter + body) — following the actual navigation flow
- `_data/navigation.json` — sidebar structure that determines click paths
- `_data/index.json` — homepage content, manifesto, routes, featured artifacts
- `contact.md` — terminal page
- `bio/index.md` — bio page
- `thinking.md` — argument page
- `colophon.md` — recursive proof page
- Blog posts in `_blog/` (if any exist)

### Invoke (as needed)
None. Reads pages directly.

### Lens Criteria (embedded)
The three journeys below ARE this skill's criteria.

## Evaluate

### Journey 1: Discovery Path (the stranger)

**Route:** Homepage → one featured project (first artifact in first route) → tier index → second project → contact

The stranger's path. They found the site via search, a link, or LinkedIn. They know nothing. Does the site earn their next click at every step?

**Check at each transition:**
- Does the current page create motivation to click deeper?
- Does the next page deliver on what the previous page promised?
- Does voice/tone stay consistent across the sequence?
- Is there a clear "what do I do next?" at each step (even if subtle)?

### Journey 2: Deep Dive Path (the curious person)

**Route:** Blog post (if exists, else homepage) → related project → Governance rabbit hole (Savepoint → Aetherwright → Formwork) → Colophon

The curious person's path. They liked what they saw and want to understand how this person thinks. Does the depth reward them?

**Check at each transition:**
- Does the Governance trilogy build when read in sequence? (Savepoint → Aetherwright → Formwork should escalate, not repeat)
- Does the Colophon feel like a destination — the reward for going deep?
- Does vocabulary introduced early (drift, scaffold, fidelity) pay off later?
- Is the rabbit hole compelling or does it feel like homework?

### Journey 3: Peer Evaluation Path (the hiring manager / collaborator)

**Route:** Homepage → Bio → Encore (flagship) → Formwork (methodology) → Thinking

The professional's path. They're evaluating whether Peter is someone they want to work with. They need evidence, not vibes.

**Check at each transition:**
- Does the Bio establish credibility quickly?
- Does Encore prove the range and depth?
- Does Formwork show how Peter thinks about work?
- Does Thinking make the case for the practice?
- Would this sequence make someone want to reach out?

### Cross-Journey Check

- Do all three journeys feel like the same site? (Consistent voice, visual identity, vocabulary)
- Are there pages that appear in multiple journeys? Do they serve both paths well?
- Is there a page that SHOULD be in a journey but isn't reachable via natural navigation?
- **Walk test:** Does each journey arrive at the same world? `/the-walk` evaluates per-page rooms. Journeys evaluates whether the SEQUENCE of rooms across a path builds coherently. A visitor clicking Homepage → Savepoint → Formwork should feel like they're going deeper into one world, not walking through different shops.

## Output

Print in conversation. No file changes. Format:

```
# Journeys — [GUIDED / COHERENT / DISJOINTED]

## Discovery Path — [GUIDED / COHERENT / DISJOINTED]
**Route:** [actual pages traversed]
**Verdict:** [does the experience build?]
**Weakest transition:** [Page A → Page B] — [why it breaks]
**Friction points:** [where a stranger would bounce]

## Deep Dive Path — [GUIDED / COHERENT / DISJOINTED]
**Route:** [actual pages traversed]
**Verdict:** [does the depth reward?]
**Weakest transition:** [Page A → Page B] — [why it breaks]
**Friction points:** [where curiosity stalls]

## Peer Evaluation Path — [GUIDED / COHERENT / DISJOINTED]
**Route:** [actual pages traversed]
**Verdict:** [does the evidence convince?]
**Weakest transition:** [Page A → Page B] — [why it breaks]
**Friction points:** [where a professional loses confidence]

## Cross-Journey
- **Consistency:** [do all three journeys feel like the same site?]
- **Shared pages:** [pages in multiple journeys — do they serve both?]
- **Navigation gaps:** [pages that should be reachable but aren't]
```

## Direction (if not all passing)

For each DISJOINTED or COHERENT journey:
- Which specific transition is weakest (with evidence from the page content)
- What's missing at the transition point (a hook, a connection, a tonal bridge)
- Which file(s) to modify to fix the transition
- What the transition should feel like after the fix

## Called By

- `/full-pass run` — parallel arm (independent, no data dependencies)
- Standalone — usable anytime
