---
name: arc
description: "Cross-page coherence. Do the three tiers form a coherent argument when read as a sequence? Read-only diagnostic."
user_invocable: true
---

# Arc — Atomic Skill

## Purpose

Evaluates whether the three tiers (Governance / Infrastructure / Output) form a coherent argument when read as a sequence. Does Governance explain the thinking? Does Infrastructure prove it works? Does Output demonstrate it? Does moving through all three build something greater than any individual page?

Individual lenses evaluate pages. `/the-walk` evaluates the room each page builds through its example sequence. This skill evaluates the structure at a higher level — the argument the site makes when its pieces are read together across tiers.

Read-only diagnostic. No file changes.

## Usage

```
/arc                      # Evaluate cross-page coherence
```

## Context

### Read
- All published pages grouped by tier:
  - `_governance/` — Savepoint Protocol, Order of the Aetherwright, Formwork Protocol, and any others
  - `_infrastructure/` — Encore, Sovereign Design Engine, Printshop, and any others
  - `_output/` — Aiden-Jae, Altrueism, New City, MathOnTape, Photogeography, The Deep Cuts, Versagrams, Visual Studies, and any others
- `_data/index.json` — manifesto and route structure (how the tiers are presented)
- `_data/navigation.json` — navigation order (how the tiers are sequenced)
- Homepage content — the manifesto that sets up the arc
- `bio/index.md` — does the person match the work?
- `thinking.md` — the argument page
- `colophon.md` — the recursive proof page

### Invoke (as needed)
None. Reads pages directly.

### Lens Criteria (embedded)
The four coherence dimensions below ARE this skill's criteria.

## Evaluate

### 1. Intra-Tier Coherence

Do the pages within each tier relate to each other?

**Governance:** Savepoint → Aetherwright → Formwork should BUILD, not just coexist. Savepoint introduces the problem (continuity under change). Aetherwright introduces the identity (the practitioner who holds continuity). Formwork introduces the method (the structural approach). Do they actually do this? Or do they repeat each other? Contradict? Feel disconnected?

**Infrastructure:** The maintained platforms and tools. Do they demonstrate the Governance principles in action? Can you see the Formwork methodology in how Encore was built? Does the Sovereign Design Engine connect to the thinking in Savepoint?

**Output:** The delivered work. Does the range (jewelry, music, visual studies, novels) feel like it comes from the same mind? Or does it feel like different portfolios stapled together? The Shaw test at the tier level: do these outputs feel like they all came from the same shop?

### 2. Inter-Tier Coherence

Do the tiers support each other?

- **Governance → Infrastructure:** Does the thinking explain how the tools were built? If you read Formwork and then look at Encore, do you think "ah, this is what that looks like in practice"?
- **Infrastructure → Output:** Do the tools explain the output? If you see the Sovereign Design Engine and then look at Aiden-Jae, does the connection land?
- **Governance → Output:** Does the thinking explain the work? Can you trace a line from Savepoint's philosophy to the actual delivered projects?
- **Output → Governance (reverse):** Does seeing the work make the governance feel earned? Or does the governance feel like theory disconnected from practice?

### 3. The Arc

Does the full sequence — homepage manifesto → Governance → Infrastructure → Output → contact — tell a story?

- **Setup (homepage):** Does the manifesto promise something specific?
- **Thesis (Governance):** Does the thinking deliver on the promise?
- **Proof (Infrastructure):** Do the tools demonstrate the thinking?
- **Evidence (Output):** Does the work prove the whole thing works?
- **Resolution (contact/bio):** Does the ending feel like an invitation, not a dead end?

### 4. The Coherence Through-Line

the site's core claim is "seeing the whole picture and building the structure so coherence holds." Is this visible across pages without being stated on every page?

- Can a visitor who reads 5+ pages articulate what ties them together — without spelling it out?
- Is the through-line in the structure (how pages connect) or just in the copy (what pages say)?
- Does the material vocabulary (holds, breaks, drifts, scaffold, fidelity) accumulate meaning across pages, or stay opaque?

## Output

Print in conversation. No file changes. Format:

```
# Arc — [REINFORCING / COHERENT / FRAGMENTED]

## Intra-Tier Coherence
### Governance — [REINFORCING / COHERENT / FRAGMENTED]
[Do Savepoint → Aetherwright → Formwork build? What connects them. What's missing.]

### Infrastructure — [REINFORCING / COHERENT / FRAGMENTED]
[Do the tools relate? Do they demonstrate the governance? What connects them.]

### Output — [REINFORCING / COHERENT / FRAGMENTED]
[Does the range feel unified? Shaw test at the tier level.]

## Inter-Tier Relationships
- **Governance → Infrastructure:** [connected / implied / disconnected] — [evidence]
- **Infrastructure → Output:** [connected / implied / disconnected] — [evidence]
- **Governance → Output:** [connected / implied / disconnected] — [evidence]
- **Output → Governance (reverse):** [earned / neutral / disconnected] — [evidence]

## The Arc
**Setup:** [what the homepage promises]
**Thesis:** [what governance delivers]
**Proof:** [what infrastructure demonstrates]
**Evidence:** [what output proves]
**Resolution:** [what the ending offers]
**Verdict:** [does the sequence tell a story? where does it break?]

## The Through-Line
- **Visible in structure:** [yes/no — how]
- **Visible in copy:** [yes/no — how]
- **Vocabulary accumulation:** [builds / flat / opaque]
- **5-page test:** [could a visitor articulate the connection after 5 pages?]

## The Gap
[The single most impactful thing that would improve the arc. Not a list of 10 improvements — the ONE change that would most strengthen the argument the site makes.]
```

## Direction (if not all passing)

For each FRAGMENTED dimension:
- What specifically is disconnected (with evidence from the page content)
- What connection is missing (between which pages, about what)
- Which files to modify to create the connection
- What the connection should feel like (not copy to write, but the relationship to establish)

## Called By

- `/steward run` — parallel arm (independent, no data dependencies)
- Standalone — usable anytime
