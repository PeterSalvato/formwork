---
name: grip-test
description: "Ben's Grip Test — diagnostic for whether copy lands with a stranger. Stranger Test + Fingernail/Grip/Lock rating. Read-only, no file changes."
user_invocable: true
---

# Grip Test — Atomic Skill

## Purpose

Quick diagnostic: does this copy land with someone who hasn't lived through the problem? Named after a friend named Ben, who said he could only get "a fingernail hold" on Savepoint. That's the standard.

This is a read-only diagnostic. It rates what exists. It doesn't rewrite.

## Usage

```
/grip-test [page-path]     # Rate a specific page
/grip-test [url-path]      # Rate by URL path (e.g., /governance/savepoint-protocol)
```

## Input

The page body text — specifically the first 2-3 paragraphs (the opening), plus enough of the rest to understand the arc.

## Context

### Read
- Target page content (the page being tested)
- `voice/copywriting-protocol.md` — Millman x Craftsman voice rules
- `docs/visual-reference-index.md` → active reference set (for visual context)

### Invoke (as needed)
- `/knowledge` → search for real moments behind this content → source-attributed results
- `- Voice sample skill (if available) → speaking patterns → rhythm, vocabulary observations

### Lens Criteria (embedded)
The Stranger Test + Fingernail/Grip/Lock diagnostic below ARE this skill's criteria.

## The Stranger Test

Read the first two paragraphs as if you've never heard of this person or project. Answer:

1. **What does a stranger feel after reading this?** Not "what do they know" — what do they *feel*? Do they feel the problem in their gut, or are they being informed about it?

2. **When does the page become undeniable?** Find the sentence where even a skeptic would stop and pay attention. How far into the page is it? If it's past paragraph 2, the opening isn't doing its job.

3. **What's the "in"?** What shared human experience does this connect to? Losing something you can't get back? Building something nobody asked for? The gap between what you know and what you can prove? Name it.

## Fingernail / Grip / Lock

Rate the page:

- **Fingernail** = the reader can see it's *something* but can't feel why it matters to them
- **Grip** = the reader feels the problem even if they haven't lived it
- **Lock** = the reader recognizes their own experience in what they're reading

## Current Angle

Name the story the page is currently telling in one sentence. Then name 1-2 alternative angles that might land harder for a stranger.

Use the Angle Library for reference (not a formula — a prompt when stuck):

- **The Loss** — opens with what was lost or broken. Works when the project exists because something failed.
- **The Reflex** — opens with the behavior that existed before the system. Works when the maker was already doing the thing informally.
- **The Gap** — opens with what the stranger already knows vs. what they're missing. Works when the problem is invisible until you name it.
- **The Craft Detail** — opens with a specific technical fact that reveals depth. Works when the reader is a peer.
- **The Contradiction** — opens with two things that should work together but don't. Works when the problem is structural.

## Output

Print in conversation. No file changes. Format:

```
# Grip Test — [page name]

## Stranger Test
1. **Feel:** [answer]
2. **Undeniable moment:** [quote the sentence, note how far in]
3. **The "in":** [name the shared experience]

## Rating: [Fingernail / Grip / Lock]
[Why — 1-2 sentences]

## Current Angle
[One sentence: the story this page tells now]

## Alternative Angles
- [Angle 1 — type + what it would open with]
- [Angle 2 — type + what it would open with]
```

## Called By

- `/copy check` — runs grip-test as its first step
- `/copy edit` — runs grip-test during Phase 1 story discovery
- Standalone — usable anytime to diagnose a page
