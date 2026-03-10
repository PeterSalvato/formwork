---
name: voice-sample
description: "Voice sampling — study how Peter actually talks in conversations (not published pages). Captures rhythm, openings, vocabulary, humor. Accumulates observations over sessions."
user_invocable: true
---

# Voice Sample — Atomic Skill

## Purpose

Before writing copy, you need to know how Peter actually sounds. Not how his published pages sound — how HE sounds when he's explaining something in conversation. This skill searches his conversation history, extracts voice patterns, and accumulates observations over time.

The voice sample is a tuning fork, not a style guide. After writing a draft, read it back and ask: does this sound like the person in those conversations? Not a polished version of him. Him.

## Usage

```
/voice-sample [topic]      # Sample how Peter talks about a specific topic
/voice-sample              # General voice sampling (broader search)
```

## Context

### Read
- Conversation exports: Claude Code JSONL, ChatGPT, Claude.ai, Gemini
- Filter for Peter's messages only (not AI responses)
- Previous observations: `memory/voice-sample.md`

### Invoke (as needed)
N/A — this skill observes, it doesn't evaluate against other skills.

### Lens Criteria (embedded)
N/A — this is an observation tool. It accumulates patterns, not verdicts.

## Sources (Peter's messages only)

Filter for Peter's words, not AI responses. Search in this order:

### 1. Current conversation
How Peter is talking to you right now. This is the freshest, most natural sample.

### 2. Claude Code sessions
Location: `/home/peter/.claude/projects/-home-peter-homelab-projects-active-petersalvato-com/*.jsonl`
Filter: Look for `"role":"human"` entries.
```bash
grep -l "[topic]" /home/peter/.claude/projects/-home-peter-homelab-projects-active-petersalvato-com/*.jsonl
```
Then extract Peter's messages from matching sessions.

### 3. PKB search
```
/pkb search "[topic]"
```
The PKB indexes 52,000+ documents across all sources. If available, use it for broad searches.

### 4. ChatGPT exports
Location: `/home/peter/homelab/knowledge/exports/JSON/conversations.json`
Filter for Peter's messages (the human turns, not the assistant turns).

### 5. Claude.ai / Gemini exports
Location: `/home/peter/homelab/knowledge/exports/consolidated_exports/consolidated_clean/`
These are markdown — harder to filter speaker, but still useful for patterns.

## What to Capture

From conversations, NOT from published pages:

- **Sentence rhythm** — Short bursts or long flowing thoughts? How does he connect ideas?
- **Opening moves** — How does he start explaining something? ("I think...", "so basically...", "the thing is...", "yeah let's...")
- **Vocabulary** — What words does he reach for naturally? What words does he never use?
- **Transitions** — Connectors ("and", "so", "but") or hard breaks?
- **How he describes problems** — Names the feeling first or the situation?
- **How he describes solutions** — Explains the mechanism or the result?
- **Humor and tone** — Dry? Self-deprecating? Matter-of-fact?
- **Phrasing patterns** — Recurring structures, pet phrases, how he qualifies things
- **How he gives direction** — Does he specify exactly or sketch loosely? Does he think out loud?

## Output

Print observations in conversation. Also accumulate in the persistent memory file.

### In conversation:

```
# Voice Sample — [topic or "General"]

## Rhythm
[How he strings sentences together]

## Opening Moves
[How he starts explaining — with examples quoted from conversations]

## Vocabulary
- Reaches for: [words he uses naturally]
- Never uses: [words absent from his speech]

## Tone
[Dry/warm/matter-of-fact/self-deprecating — with examples]

## Patterns
[Recurring structures, pet phrases, qualifiers]

## Example Quotes
[3-5 actual quotes from conversations that capture his voice]
```

### Persistent file:

Append observations to:
`/home/peter/.claude/projects/-home-peter-homelab-projects-active-petersalvato-com/memory/voice-sample.md`

Each session that does copy work should ADD to this file, not replace it. Over time it becomes a detailed fingerprint. Date-stamp each addition.

Format for persistent entries:
```
## [DATE] — [topic or context]
- [observation]
- [observation]
- Quote: "[actual quote]"
```

## Relationship to Voice Protocol

The Millman x Craftsman protocol (in `voice/copywriting-protocol.md`) defines the **register**: personal stakes through action, material vocabulary, no hype.

The voice sample defines the **person** inside that register. Two different writers could follow the same protocol and produce different copy. The voice sample ensures the copy sounds like Peter specifically.

## Called By

- `/copy edit` — Phase 1, Step 2 (while searching ideation history)
- `/copy write` — Step 3
- Standalone — usable anytime to build the fingerprint
