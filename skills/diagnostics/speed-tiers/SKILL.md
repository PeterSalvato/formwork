---
name: speed-tiers
description: "Time-based evaluation. What registers in 10 seconds, 2 minutes, 20 minutes? Read-only diagnostic."
user_invocable: true
---

# Speed Tiers — Atomic Skill

## Purpose

Evaluates the site at three speeds. What registers in 10 seconds (a glance at the homepage)? What lands in 2 minutes (a browse through one tier)? What rewards 20 minutes (reading the full Governance trilogy)? Most visitors give you 10 seconds. A few give you 2 minutes. Almost nobody gives you 20. The site needs to work at all three speeds — and pull visitors from one tier into the next.

Read-only diagnostic. No file changes.

## Usage

```
/speed-tiers              # Evaluate all 3 time tiers
```

## Context

### Read
- Homepage (`index.md` or systemworks layout output) — above the fold is the 10-second test
- `_data/index.json` — manifesto and route structure
- 1 project page per tier (first listed artifact in each route) — the 2-minute test
- Full Governance trilogy (Savepoint, Aetherwright, Formwork) OR full Output section — the 20-minute test
- Screenshots from `.audit/screenshots/` if available (the 10-second test is best done visually)
- `DESIGN-SYSTEM.md` if it exists — visual intent context

### Invoke (as needed)
None. Reads pages directly.

### Lens Criteria (embedded)
The three speed tiers below ARE this skill's criteria.

## Evaluate

### Tier 1: 10 Seconds (the glance)

Evaluate the homepage above the fold. A stranger has arrived. They will decide in 10 seconds whether to stay.

- **Identity:** Do they know who this person is? (Name, what they do — even vaguely)
- **Hook:** Is there something that makes them want to scroll or click? (A striking phrase, an interesting visual, an unexpected element)
- **Differentiation:** Does this look like "another portfolio" or does it feel distinct? (See `/the-walk` — what room does the homepage content build? See `/the-walls` — what room does the ambient frame build? At 10 seconds, the frame registers before the content.)
- **Navigation clarity:** Can they tell where to go next?
- **Visual first impression:** Does the design itself communicate something? (Craft, care, personality — or generic template)

### Tier 2: 2 Minutes (the browse)

Evaluate the homepage plus one click-through (a project page or tier index).

- **Manifesto landing:** Does the homepage manifesto communicate the practice clearly enough to earn the click?
- **Project page delivery:** Does the first project page they visit deliver on the homepage's promise?
- **Voice consistency:** Same person speaking on both pages?
- **Depth signal:** After 2 minutes, does the visitor sense there's more worth exploring? Or did they get the gist and that's enough?
- **Range signal:** Do they understand this person works across domains? Or do they think it's a single-discipline portfolio?

### Tier 3: 20 Minutes (the deep read)

Evaluate the full Governance trilogy or the full Output section as a sustained reading experience.

- **Vocabulary payoff:** Does the material vocabulary (holds, breaks, drifts, scaffold, fidelity) make more sense by the end? Or is it still opaque?
- **Intellectual reward:** Does the depth feel rewarding? Does the reader think "this person really thinks about this" or "this is over-engineered"?
- **Through-line:** Does the sustained reading reveal a coherent practice, or disconnected projects?
- **The Aetherwright payoff:** For someone who reads the whole Governance section — does the symbolic system (sigils, altitude, the Order) feel earned by the end? Or still alienating?
- **Return signal:** After 20 minutes, does the visitor want to come back? Bookmark? Share?

### Transition Hooks

The most important thing this skill evaluates: what pulls a visitor from one tier to the next?

- **10s → 2min:** What on the homepage makes someone click deeper? Is it the manifesto? A project name? A visual element?
- **2min → 20min:** What on the first project page makes someone want to read more? Is there a trail of breadcrumbs?
- If either transition hook is missing, the site is effectively only the tier above it.

## Output

Print in conversation. No file changes. Format:

```
# Speed Tiers — [COMPELLING / ADEQUATE / BRITTLE]

## 10 Seconds — [COMPELLING / ADEQUATE / BRITTLE]
**What registers:** [what a stranger absorbs in a glance]
**What's invisible:** [what they'd never know from 10 seconds]
**Hook to stay:** [what pulls them into 2 minutes — or nothing]

## 2 Minutes — [COMPELLING / ADEQUATE / BRITTLE]
**What lands:** [what a browser understands after homepage + one click]
**What's invisible:** [what requires more time]
**Hook to go deeper:** [what pulls them into 20 minutes — or nothing]

## 20 Minutes — [COMPELLING / ADEQUATE / BRITTLE]
**What rewards:** [what the deep reader gets that nobody else does]
**What's still opaque:** [what doesn't land even after 20 minutes]
**Return signal:** [would they come back?]

## Transition Hooks
- **10s → 2min:** [present / weak / missing] — [what it is or what's needed]
- **2min → 20min:** [present / weak / missing] — [what it is or what's needed]

## Brittleness Risk
[If the site only works at one speed, which speed? What breaks at the other speeds?]
```

## Direction (if not all passing)

For each BRITTLE or ADEQUATE tier:
- What specifically doesn't register at that speed (with evidence)
- What would need to change to make it register (specific content or design change)
- Which files to modify
- What the result should feel like after the change

For missing transition hooks:
- What's currently at the transition point
- What kind of hook is needed (content, visual, navigational)
- Where it should live (which page, which section)

## Called By

- `/full-pass run` — parallel arm (independent, no data dependencies)
- Standalone — usable anytime
