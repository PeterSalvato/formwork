---
name: interview
description: "Context-aware story extraction. Loads the maker's full context — identity, expertise, voice, published work — then reads the narrative architecture to understand the story being told and what's missing. Interviews the maker to fill gaps with real moments. Modular: works with any project."
user_invocable: true
---

# Interview — Context-Aware Story Extraction

## Purpose

Extract real moments from a maker's lived experience to fill specific gaps in a narrative architecture. Before asking a single question, the skill loads full context — who the maker is, what they've built, how they talk, what the story needs — so every question is informed by the depth of the work and aimed at a specific gap in the narrative.

## The Load Sequence

**This is mandatory. The skill does not interview without completing this sequence first.**

Before any interview begins, the skill loads context in this order:

### Step 1: Read the architecture file

The project's narrative architecture defines the story, its structure, and its gaps. The architecture file's **Context Sources** section points to everything else the skill needs to load.

### Step 2: Load the context sources

The architecture file lists the sources that give the skill depth. Load ALL of them before proceeding. Typical sources:

| Source | What it gives the skill |
|--------|------------------------|
| **Identity document** | Who the maker is — aesthetic DNA, cultural roots, values, the genre. The skill interviews a PERSON, not a role. |
| **Core insight / thesis** | The governing ideas — what the work is actually about at the deepest level. Without this, the skill asks surface questions. |
| **Voice samples** | How the maker actually talks — rhythm, openings, vocabulary, humor. The skill recognizes the maker's real language when it hears it. |
| **Published work** | What's already been said publicly. The skill doesn't ask for material that already exists — it reads the work and builds from it. |
| **Domains of expertise** | The maker's full skill set, career history, the rooms they've been in. The skill needs to understand the RANGE to ask questions that surface connections across domains. |
| **Conversation history** | Prior sessions, ideation history. The skill knows what the maker has already articulated so it doesn't re-extract — it goes deeper. |

The exact files and paths are listed in the architecture file's Context Sources section. Different projects point to different sources. The skill reads whatever the manifest tells it to read.

### Step 3: Internalize the story

After loading, the skill should be able to answer:
- What is this project's story in one paragraph?
- What are the maker's domains of expertise and how do they connect?
- What is the governing line / thesis?
- What has already been captured and published?
- What are the open gaps, in priority order?
- What voice does the maker use — and what language would they NEVER use?

If the skill can't answer all of these, it hasn't loaded enough context. Go back to Step 2.

### Step 4: Assess gaps and present

Now — and only now — the skill presents:
- The number of open gaps across the full structure
- Which gaps are highest priority (foundations before details, movements in order)
- A recommendation for where to start, with reasoning from the story's needs
- What the skill already knows from context that's relevant to each gap

The maker chooses where to begin. The skill follows.

---

## The Architecture File Format

Every project that uses this skill needs an architecture file. The format:

```markdown
# [Project Name] — Narrative Architecture

## Context Sources
- Identity: [path to identity/persona document]
- Core insight: [path to thesis/insight document]
- Voice: [path to voice sample accumulation]
- Published work: [paths to published pages/posts]
- Domains: [path to career/expertise summary, or inline]
- History: [path to conversation exports or session logs]

## The Story
[One paragraph: what does the finished work communicate?]

## The Governing Line
[The single sentence that anchors every piece]

## The Core Operation
[What the maker actually DOES — the skill or method underneath the work]

## The Maker's Domains
[List of domains with depth notes — not just names but what the maker
actually did in each domain and how long. This is what lets the skill
ask questions that surface cross-domain connections.]

## Voice
[Key voice principles — what language to use, what to avoid,
what imagery to reach for]

## Structure

### [Movement/Chapter/Section Name]
**Purpose:** [What this part teaches or communicates]
**Needs:** [What kind of material fills this part]
**Site pages / deliverables serving this movement:** [list]

#### [Specific gap]
- **Status:** OPEN | CAPTURED | DEEP
- **What's needed:** [Specific description]
- **Why this matters to the story:** [How this gap connects to the thesis]
- **Seed:** [When captured: room, moment, body, read, transfer, maker's words]
- **Placement:** [Which deliverable this feeds]

### [Next section]
...

## Cross-Structure Evidence
[How the same projects/stories appear across multiple movements —
the skill uses this to recognize when a tangent fills a gap in
a different movement than the one being discussed]

## Captured Material
[Running ledger of what's been extracted, with dates and references]
```

---

## The Interview

### Principles

1. **One question at a time.** Never a battery. Ask, listen, follow.
2. **Questions informed by context.** Don't ask "tell me about your teaching." Ask "you taught at Kingsborough — there must have been a specific student where you saw what the curriculum was missing. Who was that?"
3. **Somatic over cognitive.** "What did it feel like?" before "what did you think?" The body knows first.
4. **Concrete over abstract.** Specific rooms, specific people, specific moments.
5. **Capture real language.** The maker's exact phrasing IS the voice. Quote back, don't paraphrase.
6. **Follow the body.** When the maker mentions a physical sensation — go there.
7. **Follow tangents as transfer.** "That reminds me of..." is a cross-domain connection happening in real time. Capture it and check: does this fill another gap?
8. **Know when to stop.** A specific moment + a physical detail + what it meant = a complete seed.
9. **Respect executive function.** If the maker stalls, move to a different gap. Don't push.
10. **Never interrupt flow.** When the maker is connecting across domains unprompted, let it run. Capture everything.

### What Makes a Good Seed

- **Specific:** A particular night, a particular student, a particular project moment
- **Physical:** What the room looked like, what the body did, what could be heard or felt
- **A read:** What the maker saw or sensed that others in the room didn't
- **A person:** Someone specific on the receiving end of the experience
- **A cost:** What was at stake if the read was wrong

A good seed has a room you can see, a moment you can feel, and a read that only this maker would have made.

### Seed Capture Format

When the maker gives you a moment:

```markdown
## Seed: [gap reference from architecture]

**The room:** [physical/environmental detail]
**The moment:** [what happened]
**The body:** [somatic detail — what the maker or the person on the receiving end physically felt]
**The read:** [what the maker saw that others missed]
**The transfer:** [connections to other domains/movements the maker surfaced]
**Maker's words:** "[direct quotes from the conversation]"
**Movement/Section:** [where this lives in the architecture]
**Status:** CAPTURED
```

---

## Modes

### `/interview`
Load architecture, load all context sources, assess gaps, recommend where to start. The full startup sequence.

### `/interview [movement/section]`
Target a specific part of the architecture. Still loads full context, but focuses the gap assessment on the named section.

### `/interview batch`
Rapid-fire seeding. Present each OPEN gap as a single line, capture one-sentence seeds. Fast. For when the maker has limited time or energy and you need maximum extraction per minute.

---

## After the Interview

### Update the architecture file
- Mark filled gaps as CAPTURED with seed reference
- Note new gaps that surfaced during conversation
- Note cross-movement connections discovered through tangents
- Update the Captured Material ledger

### Feed downstream skills
- Seeds go to `/copy` for drafting
- Drafts go to `/grip-test` and `/copy-verify` for evaluation
- The architecture file is the single source of truth for what's been produced and what's still needed

---

## Integration

- **`/knowledge`** finds material in conversation history. Interview elicits NEW material.
- **`/voice-sample`** captures how the maker talks. Interview creates the occasion for talking.
- **`/copy`** drafts from seeds. Interview produces the seeds.
- **`/grip-test`** evaluates finished copy. Interview precedes writing.
- **`/formwork`** evaluates across independent layers. The architecture file is a parallel structure — independent movements that register into a whole.

The interview is the first move in the production chain. The architecture file is the map that keeps all of it coherent.
