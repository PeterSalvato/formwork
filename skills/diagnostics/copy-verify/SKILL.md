---
name: copy-verify
description: "Copy verification checklist — 12-item pass/fail check on draft or published copy. Voice rules, grounding, Shaw check. Read-only diagnostic."
user_invocable: true
---

# Copy Verify — Atomic Skill

## Purpose

12-item verification checklist for any copy — draft or published. Catches voice violations, ungrounded claims, missing updates, and Shaw failures. Shared by `/copy edit`, `/copy write`, and `/audit` baseline.

Read-only diagnostic. Reports pass/fail per item, never auto-fixes.

## Usage

```
/copy-verify [page-path]   # Verify a specific page
/copy-verify               # Verify the most recently edited page
```

## Context

### Read
- Draft or published page content + frontmatter
- `_data/index.json` — navigation, manifesto
- `voice/copywriting-protocol.md` — voice rules
- `voice/agent-voice.md` — operating protocol

### Invoke (as needed)
- `/knowledge` → verify claims are grounded in real history → source-attributed results
- `/grip-test` → stranger test on the same copy → Fingernail/Grip/Lock rating

### Lens Criteria (embedded)
The 12-item checklist below IS this skill's criteria.

## Checklist

Run every item. Report pass/fail with specifics on failures.

1. [ ] Does the opener make a stranger feel the problem (not just know about it)?
2. [ ] Does it pass the Fingernail Test at Grip or Lock? (Run `/grip-test` if needed)
3. [ ] Is every specific detail traceable to a verified source?
4. [ ] Zero em dashes?
5. [ ] Zero banned words? (paradigm, leverage, passionate, innovative, synergy, empower, journey, transformative)
6. [ ] No fortune-cookie closer?
7. [ ] Negation-affirmation ("Not X. Y.") only where earned? Each instance must correct a genuine misunderstanding the reader would actually have. If the negation is emphasis or contrast rather than misdirection correction, rewrite it.
8. [ ] No ungrounded metaphors?
9. [ ] No personification of tools/methods? ("does the thinking", "holds itself")
10. [ ] Shaw check: does the copy feel like a room, not a pitch? Do the references and subject matter paint the specific person? If you stripped the name, would this feel wrong on someone else's site?
11. [ ] Does the frontmatter (context/drift/scaffold/fidelity) match the body?
12. [ ] Does the `_data/index.json` entry need updating to match?

## Output

Print in conversation. No file changes. Format:

```
# Copy Verify — [page name]

## Result: [X/12 passed]

1. Opener lands: [PASS/FAIL] — [note]
2. Grip test: [PASS/FAIL] — [Fingernail/Grip/Lock]
3. Details grounded: [PASS/FAIL] — [unverifiable claims if any]
4. Em dashes: [PASS/FAIL] — [count if any]
5. Banned words: [PASS/FAIL] — [words found if any]
6. Fortune-cookie closer: [PASS/FAIL]
7. Negation-affirmation: [PASS/FAIL] — [count, each must correct genuine misunderstanding]
8. Ungrounded metaphors: [PASS/FAIL] — [which ones]
9. Tool personification: [PASS/FAIL] — [instances]
10. Shaw check: [PASS/FAIL] — [note]
11. Frontmatter match: [PASS/FAIL] — [mismatches]
12. Index.json sync: [PASS/FAIL] — [needs update?]
```

## Complementary Check

`/the-walk` evaluates whether the page's example sequence builds the same room as the homepage. Copy-verify catches voice and grounding issues. The Walk catches positioning issues — a page can pass all 12 items and still build the wrong room if its examples position a secondary identity. When called from `/copy edit` or `/copy review`, The Walk runs alongside copy-verify.

## Called By

- `/copy edit` — runs after writing draft (Phase 2, Step 6)
- `/copy write` — runs after writing draft
- `/audit run` — can be called for spot checks on published pages
- Standalone — usable anytime
