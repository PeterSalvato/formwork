---
name: knowledge
description: "Traverse ideation history across any collection of conversation exports, notes, and documents. Traces concept lineage, finds real moments, studies voice. Uses streaming distillation to handle arbitrarily large corpora without blowing context."
user_invocable: true
---

# Knowledge — Ideation History Traversal

<!-- SKILL DESIGN RATIONALE: Ideation history gets spread across conversation exports
     in multiple formats — ChatGPT, Claude, Gemini, plain notes, dictations. A keyword
     search (grep) misses embryonic mentions — the first time an idea appeared, it
     probably wasn't called by its final name. The streaming distillation algorithm
     solves this: read chronologically, carry understanding forward, catch what grep
     can't. The skill is format-agnostic: point it at a directory, it figures out
     what's there and processes it. -->

## Purpose

Traverse conversation history and notes to find how concepts emerged, evolved, and crystallized. This is not keyword search — it is chronological reading with progressive distillation, so you catch embryonic mentions that no grep would find.

**This skill is directory-driven.** Point it at a directory of exports. It discovers what's there, verifies formats, and traverses. It doesn't assume a fixed corpus, a specific timespan, or a predetermined set of sources.

**This is an atomic skill.** It traverses and returns findings. It does not write copy or make evaluations. Coordinators like `/copy`, `/audit`, and `/grip-test` call this and use the results.

## Quick Reference

```
/knowledge [query]              # Fast search — grep across all sources
/knowledge lineage [topic]      # Full traversal — streaming distillation, beginning to end
/knowledge voice [query]        # Find how the user actually talks about a topic
```

## The Corpus

<!-- WHY DIRECTORY-DRIVEN: The skill shouldn't be married to one specific export
     directory or one person's history. The default paths below are one user's
     current setup, but the skill works the same way on any directory of exports. New sources
     get dropped in, the format verifier identifies them, and they're processed.
     The skill scales with whatever's there — 10 files or 10,000. -->

**Default source directory:** `/home/peter/homelab/knowledge/exports/`
**Additional sources:** Claude Code session directories under `/home/peter/.claude/projects/`

Override with: `/knowledge [query] --dir /path/to/exports`

The skill recursively walks the target directory, identifies every file by probing its structure, and processes accordingly. It doesn't require a predetermined file list.

### Format Registry

<!-- WHY A FORMAT REGISTRY: Each platform exports differently — epoch floats vs ISO
     strings, nested mapping trees vs flat arrays, role labels ("user" vs "human" vs
     "**User:**"). The registry means the agent doesn't have to reverse-engineer the
     structure every time. When a new export type gets dropped in, inspect it once,
     add it here, and it's handled forever.

     WHY VERIFY-THEN-TRUST: The registry is an optimization, not a guarantee.
     Export formats change between platform versions. A ChatGPT export from 2026
     may not match the 2023 structure. If you assume and get it wrong, you silently
     extract nothing — that's worse than being slow. So: probe first, confirm the
     structure matches, THEN use the fast path. If it doesn't match, inspect and adapt. -->

The skill handles every format it encounters. Here are the known formats.

**IMPORTANT: Verify before extracting.** Before processing any source file, probe its structure (read the first record, check key names and nesting) and confirm it matches the registry entry below. If it doesn't, inspect the actual structure and adapt. Never silently extract nothing because the format drifted.

### Format Verification Protocol

For every source file, before using any extraction command:

1. **Probe** — Read the first record/entry and print its top-level keys
2. **Compare** — Do the keys match the registry entry for this format?
3. **Match → proceed** using the registered extraction commands
4. **Mismatch → inspect** the actual structure:
   - What are the keys?
   - Where is the message content? (follow the nesting)
   - Where is the sender/role indicator?
   - Where is the timestamp?
   - Adapt the extraction commands to the actual structure
   - Report the discrepancy so the registry can be updated

**Probe commands by file type:**

For JSON files (ChatGPT exports):
```bash
# Probe first record's top-level keys
python3 -c "
import json, sys
with open('FILE_PATH') as f:
    data = json.load(f)
if isinstance(data, list) and data:
    print('Array of', len(data), 'items')
    print('Keys:', list(data[0].keys()))
    # Check for message structure
    for k in ['mapping', 'chat_messages', 'messages']:
        if k in data[0]:
            print(f'Message field: .{k}')
            # Probe first message
            if isinstance(data[0][k], list) and data[0][k]:
                print(f'First message keys: {list(data[0][k][0].keys())}')
            elif isinstance(data[0][k], dict):
                first_key = next(iter(data[0][k]))
                print(f'First mapping entry keys: {list(data[0][k][first_key].keys())}')
elif isinstance(data, dict):
    print('Object with keys:', list(data.keys()))
"
```

For JSONL files (Claude Code sessions):
```bash
# Probe first few lines for record types
head -5 FILE_PATH | python3 -c "
import json, sys
for line in sys.stdin:
    obj = json.loads(line.strip())
    print(obj.get('type', 'no-type'), '|', list(obj.keys())[:6])
"
```

For Markdown files (Claude.ai, Gemini, notes):
```bash
# Probe structure markers
head -20 FILE_PATH
# Check for conversation separators and role markers
grep -c '^\*\*User:\*\*\|^\*\*Assistant:\*\*\|^## Conversation' FILE_PATH
```

---

### Known Formats

<!-- Each format entry documents the SIGNATURE (how to identify it) and the
     STRUCTURE (how to extract content). Signatures are what the verification
     protocol checks against. Locations are examples from the default install. -->

#### ChatGPT — Old Format
**Signature:** JSON array where first element has keys including `title`, `create_time`, `mapping`
**Filename pattern:** `conversations.json` (but verify by structure, not name)
**Structure:** JSON array. Each conversation has:
- `.title` — conversation title (string)
- `.create_time` — epoch timestamp (float)
- `.mapping` — object where values contain `.message` objects
- `.message.author.role` — "user", "assistant", "system"
- `.message.content.parts[]` — array, text items are strings
- `.message.create_time` — epoch timestamp per message

**Extract user messages chronologically:**
```bash
cat > /tmp/jq_extract.jq << 'JQEOF'
.[] | select(.title == "TITLE") |
  .mapping | to_entries | map(.value) |
  map(select(.message != null)) |
  sort_by(.message.create_time // 0) |
  .[] | select(.message.author.role == "user") |
  select(.message.content.parts != null) |
  "\(.message.create_time | todate) | \(.message.content.parts | map(select(type == "string")) | join(" "))"
JQEOF
jq -r -f /tmp/jq_extract.jq FILE_PATH
```

#### ChatGPT — New Format
**Signature:** JSON array where first element has keys including `uuid`, `name`, `chat_messages`
**Filename pattern:** `conversations.json` (same name as old format — must verify by structure)
**Structure:** JSON array. Each conversation has:
- `.name` — conversation title (string)
- `.created_at` — ISO timestamp (string)
- `.chat_messages[]` — flat array (not a mapping tree)
- `.chat_messages[].sender` — "human" or "assistant"
- `.chat_messages[].content[]` — array of content objects
- `.chat_messages[].content[].text` — the actual text
- `.chat_messages[].created_at` — ISO timestamp per message

**Extract user messages:**
```bash
cat > /tmp/jq_new_chatgpt.jq << 'JQEOF'
.[] | select(.name == "TITLE") |
  .chat_messages[] | select(.sender == "human") |
  "\(.created_at) | \([.content[] | select(.type == "text") | .text] | join(" "))"
JQEOF
jq -r -f /tmp/jq_new_chatgpt.jq FILE_PATH
```

#### Claude.ai — Individual Markdown
**Signature:** `.md` file starting with `# Title` followed by `*Created: ISO_TIMESTAMP*`
**Structure:** Markdown with conversation headers:
- First line: `# Title`
- `*Created: ISO_TIMESTAMP*`
- `**User:**` / `**Assistant:**` / `**System:**` markers
- Plain text content between markers

**Timestamp extraction:** Parse the `*Created:*` line for ISO date.

#### Claude.ai — Consolidated Markdown
**Signature:** `.md` file containing `## Conversation N/N` separators with `*Created:*` timestamps
**Structure:** Same as individual but concatenated. Can be very large.
**Note:** Use individual files when possible — consolidated files can be 16MB+ each.

#### Claude Code — JSONL Sessions
**Signature:** `.jsonl` file where lines parse as JSON with a `type` field (values: "user", "assistant", "file-history-snapshot", etc.)
**Default location:** `~/.claude/projects/*/*.jsonl`
**Structure:** One JSON object per line. Relevant types:
- `{type: "user", message: {role: "user", content: "..."}}` — user messages
- `{type: "assistant", message: {role: "assistant", content: [...]}}` — assistant responses
- Other types (file-history-snapshot, etc.) — skip these

<!-- LIMITATION: Claude Code JSONL has no per-message timestamps. This is the weakest
     source for precise chronology. We use file mod date to place the SESSION in the
     timeline, but can't pinpoint when within a session something was said. Line order
     is the only intra-session sequencing we have. -->
**No per-message timestamps in JSONL.** Use file modification date as session timestamp. Messages within a session are in chronological order by line position.

#### Gemini — Markdown
**Signature:** `.md` file with Gemini-style conversation markers. Identified by content patterns during probing.

#### NotebookLM — Markdown
**Signature:** `.md` file with NotebookLM-style content. Identified by content patterns during probing.

#### Plain Text / Notes / Dictations
**Any `.txt` or `.md` file** dropped into the exports directory or subdirectories.
**Timestamp:** Use file modification time. Look for date patterns in content (ISO dates, "January 2024", etc.).

### Source Priority for Lineage

<!-- WHY TIMESTAMPS ARE THE SPINE: The same idea might appear in ChatGPT on Tuesday
     and Claude.ai on Thursday of the same week. Those are two data points in ONE
     thread of thinking. If you search per-source you see two disconnected hits.
     If you sort by timestamp you see a thought developing across 48 hours.
     This is why everything normalizes to ISO 8601 before interleaving. -->

When building a chronological lineage, normalize ALL timestamps to ISO 8601 and interleave across sources. The lineage doesn't care which tool was in use — it follows the idea through time.

---

## Commands

### 1. `/knowledge [query]` — Fast Search

<!-- WHY THREE MODES: Most callers (copy, audit, grip-test) need a few strong hits,
     not a complete history. Fast search serves 80% of use cases in seconds. Lineage
     is the expensive deep operation — minutes, not seconds — reserved for when you
     need the full evolutionary arc. Voice is a specialized lens on the same data.
     Three modes means you pick the right cost for the job. -->

Quick grep across all sources. For when you need material fast, not a full traversal.

**Algorithm:**

1. **Discover sources** — recursively walk the source directory, identify all parseable files by extension and structure probe
2. **Title/metadata scan** (instant) — for each JSON source identified as ChatGPT old format, scan titles:
```bash
cat > /tmp/jq_title_search.jq << 'JQEOF'
[.[] | select(.title | type == "string") |
  select(.title | test("QUERY"; "i")) |
  {title: .title, date: (.create_time | todate)}
] | sort_by(.date) | reverse | .[:20]
JQEOF
jq -r -f /tmp/jq_title_search.jq FILE_PATH
```
3. **Grep all text-based sources** (markdown, plain text, JSONL) for the query:
```bash
grep -rl "QUERY" $SOURCE_DIR/
```
4. **Deep JSON search** (only if title scan wasn't enough — can be slow on large files):
```bash
cat > /tmp/jq_deep_search.jq << 'JQEOF'
[.[] |
  {title: .title, date: (.create_time | todate),
   matches: [.mapping[].message | select(. != null) |
     select(.content.parts // [] | map(select(type == "string")) | join(" ") |
       test("QUERY"; "i")) |
     (.content.parts // [] | map(select(type == "string")) | join(" "))[:200]]} |
  select(.matches | length > 0) |
  {title, date, match_count: (.matches | length), preview: .matches[0]}
] | sort_by(.date) | reverse | .[:15]
JQEOF
jq -f /tmp/jq_deep_search.jq FILE_PATH
```

**Return format:** Source, date, context, why it matters. Most recent first. Stop early if you have strong material.

---

### 2. `/knowledge lineage [topic]` — Streaming Distillation

This is the core operation. A full chronological traversal that traces how a concept emerged, evolved, and crystallized across all sources over months or years.

**This is an agent-scale operation.** It runs as a background agent by default. For interactive mode, the user says `/knowledge lineage [topic] --interactive`.

#### The Algorithm: Streaming Distillation

<!-- THE CORE INSIGHT: Think of this as "bubble sort for context." You can't
     load 300MB into a context window. But you CAN read it in order, keep the gold,
     and let the silt wash through. Each pass through a batch PROMOTES valuable findings
     into the lineage document and DROPS the raw text. The lineage document is the only
     thing that survives between phases — it's the rolling summary that accumulates
     fidelity on one subject while the raw material is consumed and released.

     This is a streaming reduce operation, not a search. The difference matters:
     search returns snippets, distillation returns understanding. -->

The corpus is too large to load into context. Instead, you read it chronologically in batches, distill what matters, and carry only the distilled understanding forward.

```
┌─────────────────────────────────────────────────┐
│  PHASE 0: BUILD THE MANIFEST                    │
│  Scan all sources → identify candidate convos   │
│  Sort candidates chronologically by timestamp   │
│  Output: ordered list of sources to read        │
│  Token cost: minimal                            │
└────────────────────┬────────────────────────────┘
                     │
          ┌──────────▼──────────┐
          │  PHASE 1..N: READ   │◄──────────────┐
          │  Take next batch    │               │
          │  Read full content  │               │
          │  Extract relevant   │               │
          │  material + dates   │               │
          └──────────┬──────────┘               │
                     │                          │
          ┌──────────▼──────────┐               │
          │  DISTILL            │               │
          │  Add findings to    │               │
          │  running lineage    │               │
          │  document           │               │
          └──────────┬──────────┘               │
                     │                          │
          ┌──────────▼──────────┐               │
          │  CONTEXT CHECK      │               │
          │  If > 60% full:     │               │
          │  compress lineage   │               │
          │  doc, purge raw     │               │
          │  text, continue     │──────────────►│
          └──────────┬──────────┘     more
                     │                batches
                     │ done
          ┌──────────▼──────────┐
          │  FINAL SYNTHESIS    │
          │  Clean up lineage   │
          │  doc → return       │
          └─────────────────────┘
```

#### Phase 0: Build the Manifest

Before reading any content, build a lightweight index of what to traverse.

**Step 0 (first run only): Verify all source formats.**

Before the first search/traversal of a session, probe each source file using the Format Verification Protocol above. Confirm structures match the registry. If any source has drifted, adapt extraction commands before proceeding. This only needs to happen once per session — after verification, trust the registry for the remainder.

**Step 1: Identify candidate conversations across all sources.**

Walk every file discovered during format verification. For each, use the appropriate search method:

**JSON files (ChatGPT old format)** — title scan first, then deep scan:
```bash
# Title scan (instant)
cat > /tmp/jq_manifest_titles.jq << 'JQEOF'
[.[] | select(.title | type == "string") |
  select(.title | test("QUERY"; "i")) |
  {source: "chatgpt-old", title: .title, date: (.create_time | todate), id: .conversation_id}
] | sort_by(.date)
JQEOF
jq -f /tmp/jq_manifest_titles.jq FILE_PATH

# Deep content scan (slow — use only if title scan misses expected results)
cat > /tmp/jq_manifest_deep.jq << 'JQEOF'
[.[] |
  select(.mapping | to_entries | map(.value.message) | map(select(. != null)) |
    map(.content.parts // [] | map(select(type == "string")) | join(" ")) |
    join(" ") | test("QUERY"; "i")) |
  {source: "chatgpt-old", title: .title, date: (.create_time | todate), id: .conversation_id}
] | sort_by(.date)
JQEOF
jq -f /tmp/jq_manifest_deep.jq FILE_PATH
```

**JSON files (ChatGPT new format):**
```bash
cat > /tmp/jq_manifest_new.jq << 'JQEOF'
[.[] |
  select((.name | test("QUERY"; "i")) or
    (.chat_messages | map([.content[] | select(.type == "text") | .text] | join(" ")) |
      join(" ") | test("QUERY"; "i"))) |
  {source: "chatgpt-new", title: .name, date: .created_at, id: .uuid}
] | sort_by(.date)
JQEOF
jq -f /tmp/jq_manifest_new.jq FILE_PATH
```

**Markdown files (Claude.ai, Gemini, notes)** — grep + extract timestamps:
```bash
grep -rl "QUERY" $SOURCE_DIR/ | while read f; do
  date=$(grep -m1 'Created:' "$f" | sed 's/.*Created: //' | sed 's/\*.*//')
  title=$(head -1 "$f" | sed 's/^# //')
  echo "{\"source\":\"markdown\",\"title\":\"$title\",\"date\":\"$date\",\"file\":\"$f\"}"
done
```

**JSONL files (Claude Code sessions):**
```bash
for f in $(grep -rl "QUERY" $JSONL_DIR/*.jsonl 2>/dev/null); do
  date=$(stat -c %y "$f" | cut -d. -f1)
  echo "{\"source\":\"claude-code\",\"file\":\"$f\",\"date\":\"$date\"}"
done
```

**Step 2: Merge all candidates into one chronological list, sorted by date.**

This is the manifest. It tells you what to read and in what order.

**Step 3: Estimate scope.** Report to user: "Found N conversations mentioning [topic] across [sources], spanning [earliest date] to [latest date]. Beginning traversal."

#### Phases 1–N: Traverse and Distill

Work through the manifest chronologically, oldest first.

**For each conversation/document in the manifest:**

1. **Extract the full content** using the appropriate format handler (see Format Registry above)
2. **Read it** — not just grep hits, but enough surrounding context to understand what was being discussed
3. **Extract what matters for the lineage:**
   - Date of this mention
   - What was the user thinking/saying about the topic at this point?
   - What's new here vs. what you already know from earlier in the traversal?
   - Any decisions made, directions changed, realizations had?
   - Any concrete details (names, numbers, specific incidents)?
   - The user's exact words when they're vivid or revealing
4. **Add findings to the running lineage document** (see format below)

**Context management — the promote/purge cycle:**

<!-- WHY THESE THRESHOLDS: 60% is the "comfortable" line — you have room to keep
     reading without risk. 80% is the danger zone — one more large conversation
     could push you into degraded output quality. The hard distillation at 80%
     (write to disk, read back in) is the escape valve. It's expensive (disk I/O +
     re-reading) but it means you NEVER hit the wall. The lineage document is
     the promoted state — everything else is disposable.

     The 60/80 numbers are conservative. If context windows grow, these can relax.
     If they shrink (e.g., running on a smaller model), tighten to 40/60. -->

After processing each batch of conversations, assess your context usage:
- **Below 60%:** Continue reading. You have room.
- **60-80%:** Compress the lineage document. Merge redundant entries. Keep dates, decisions, and direct quotes. Drop paraphrased summaries where the original is already captured. Purge all raw conversation text from context.
- **Above 80%:** STOP. Perform a hard distillation — the lineage document is now your ONLY carried state. Everything else is purged. Write the lineage document to `/tmp/knowledge_lineage_[topic].md`, then continue from where you left off, reading the lineage doc back in as your starting context for the next phase.

**The lineage document format:**

```markdown
# [Topic] — Lineage

## Timeline

### [ISO Date] — [Source: ChatGPT/Claude.ai/etc] — "[Conversation Title]"
**What was happening:** [1-2 sentences of context]
**Key moment:** [The actual finding — a decision, a shift, a realization]
**User's words:** "[Direct quote if available]"
**What changed:** [How this differs from the previous entry]

### [Next date] — ...
...

## Observations
- [Pattern noticed across the timeline]
- [When the concept crystallized vs. when it was still fuzzy]
- [Related concepts that kept appearing alongside this one]
```

#### Final Synthesis

After traversing the entire manifest:

1. Read back the full lineage document
2. Clean up: remove redundant entries, ensure chronological order, fill in "what changed" gaps now that you can see the full arc
3. Add a summary section at the top: "This concept first appeared as [X] in [date], evolved through [Y], and crystallized into [Z] by [date]."
4. Return the lineage document to the user

---

### 3. `/knowledge voice [query]` — Voice Sampling

Find how the user actually talks about a topic — their real words, not published copy.

**Algorithm:**

1. Run `/knowledge [query]` (fast search) to identify relevant conversations
2. For the top 5-10 results, extract ONLY user messages (user/human role)
3. Capture:
   - Sentence rhythm (short bursts or long flowing thoughts?)
   - Opening moves ("I think...", "so basically...", "the thing is...")
   - Natural vocabulary (what words he reaches for)
   - How he frames problems vs. solutions
   - Humor, tone, qualifying phrases, dialect or idiolect
4. Present raw excerpts with observations about patterns

**Where to look for voice:**
- `"role":"human"` in Claude Code JSONL
- `"author":{"role":"user"}` in ChatGPT old format
- `"sender":"human"` in ChatGPT new format
- `**User:**` blocks in Claude.ai markdown
- The current conversation (how he's talking to you right now)

**Accumulate observations** in the project's memory directory (e.g., `memory/voice-sample.md`). Each session that does voice work should ADD to this file, not replace it.

---

## What to Look For

Across all sources, the most valuable finds are:

- **The real situation** that prompted the work — not the polished version
- **Specific decisions** and what drove them — the fork in the road
- **Iterations** — what was tried and abandoned, what stuck
- **The user's own language** — especially when they're excited or frustrated
- **Concrete details** — names, numbers, durations, specific incidents
- **Crystallization points** — fuzzy thinking becoming a locked-in decision
- **Contradictions** — where he said one thing early and the opposite later (evolution)

## Notes

- **Read-only skill.** Searches and returns. Never writes copy or evaluates.
- **Always write jq filters to temp files** (`/tmp/jq_*.jq`) to avoid shell escaping issues.
- **Lineage is the expensive operation.** Fast search is cheap. Don't run lineage when search would suffice.
- **The ChatGPT deep scan takes 30-60 seconds** on 292MB. Title scan is instant. Always title-scan first.
- **New source formats:** If you encounter a file format not in the registry, inspect its structure, extract timestamps and content, and proceed. Report the new format so it can be added to the registry.
- **Results feed into** `/copy`, `/audit`, `/grip-test`, and any skill that needs grounded material.

---

## Rationale — Why This Skill Works This Way

### The Problem
Ideation history accumulates across platforms — ChatGPT, Claude, Gemini, notes, dictations — over months or years. A concept might be born in one brainstorm, refined in a different tool a week later, built in a third a month after that. No single search can find the full story because the story is spread across formats and time.

### Why Not Just Grep
Grep finds keywords. But the first mention of a concept probably didn't use its final name. "What if I could just... mark where I am" in a conversation titled "site redesign brainstorm" becomes a protocol with a proper name months later. Grep for the final name finds nothing. Chronological reading finds the embryo.

### Why Streaming Distillation
The corpus doesn't fit in a context window. The naive approach (search → return snippets) loses the connective tissue between mentions. Streaming distillation preserves it: you READ the conversations in order, so you see the concept develop the way the user experienced it. The promote/purge cycle is borrowed from how garbage collectors work in programming languages — keep what's referenced, release what's not.

### Why Timestamps Are The Spine
People don't think in platforms. They think in time. "Last March I was working on X" spans ChatGPT, Claude.ai, and handwritten notes from the same week. The only thing that unifies them is when they happened. ISO 8601 normalization makes every source interleave into one timeline.

### Why Three Modes
Different callers need different depths. A coordinator checking "did X ever come up" needs a 10-second grep, not a 20-minute traversal. Tracing the origin story of a concept needs the full lineage. Voice sampling needs the same data but filtered to only user messages, with attention to rhythm and vocabulary. One skill, three costs.

### What Could Improve
- **PKB integration:** A pre-indexed search layer would make Phase 0 (manifest building) instant instead of 30-60 seconds. Not built yet.
- **Incremental lineage cache:** Once you've traced a concept's lineage, cache it. Next time, only traverse conversations newer than the cache.
- **Semantic search:** The manifest currently uses keyword matching. Embeddings would catch more embryonic mentions where the vocabulary hadn't crystallized yet.
- **Claude Code timestamps:** JSONL sessions lack per-message timestamps, making them the weakest chronological source. If the format adds timestamps later, update the Format Registry.
