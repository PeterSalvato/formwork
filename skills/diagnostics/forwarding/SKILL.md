---
name: forwarding
description: "Would someone send this? Per-page forwardability — is the work remarkable enough to share? Read-only diagnostic."
user_invocable: true
---

# Forwarding — Atomic Skill

## Purpose

For each published page, asks: would someone who found this send it to a specific person? Not "is it good" but "is it remarkable" — literally, worth remarking on. Then asks: who would they send it to, and what would they say?

This is the word-of-mouth diagnostic. The site's positioning strategy ("desirable because interesting and unavailable") depends on people sharing it voluntarily. If no page is forwardable, the site only reaches people who find it themselves.

Read-only diagnostic. No file changes.

## Usage

```
/forwarding               # Evaluate all published pages
```

## Context

### Read
- All published pages across all collections (`_governance/`, `_infrastructure/`, `_output/`)
- Standalone pages (`bio/index.md`, `thinking.md`, `colophon.md`, `contact.md`)
- Blog posts in `_blog/` (if any exist)
- `_data/index.json` — manifesto and route structure
- Homepage content

### Invoke (as needed)
None. Reads pages directly.

### Lens Criteria (embedded)
The forwardability criteria below ARE this skill's evaluation framework.

## Calibration

The positioning strategy is "desirable because interesting and unavailable." Forwarding is the primary distribution mechanism for this strategy. Someone discovers the site, finds something remarkable, and sends it to a specific person with a specific sentence. That sentence IS the positioning — it's how the maker's reputation travels.

The forwardable pages don't need to be the "best" pages. They need to be the pages where someone thinks of a specific person and a specific reason to share.

## Evaluate

For each published page, evaluate against these forwardability criteria:

### What Makes Something Forwardable

1. **A specific insight the reader hasn't seen before** — not a common take restated well, but a genuinely new frame. ("I never thought about it that way")
2. **Work that's visually striking enough to share** — the design or imagery makes someone screenshot or copy the URL. ("You have to see this")
3. **A framing that makes the reader think of someone they know** — the page maps onto a problem or interest that triggers "my friend/colleague would love this." ("This is exactly what you were talking about")
4. **Evidence of rigor that earns "you have to see this"** — depth, craft, or thoroughness that's rare enough to be noteworthy. ("This person really takes this seriously")

### Per-Page Evaluation

For each page:
- Would someone forward this? To whom? (Be specific about the audience: "a design director," "a friend who builds tools," "someone interested in systems thinking")
- What would they say when sharing? (The forwarding sentence — the one-line pitch that isn't marketing copy but genuine enthusiasm)
- What's the forwardable element? (The specific thing — a phrase, an image, a concept, a piece of evidence)
- Is the forwardable element easy to find? (Above the fold? Buried in paragraph 4?)

### Dead Weight Check

Pages that are appreciated privately but never shared aren't failures — they serve other purposes (navigation, reference, credibility). But if the MAJORITY of pages are private, the site has a distribution problem.

## Output

Print in conversation. No file changes. Format:

```
# Forwarding — [CONTAGIOUS / SHAREABLE / PRIVATE]

## Most Forwardable
[Top 3-5 pages, ranked by forwardability]

For each:
- **Page:** [name]
- **Verdict:** [CONTAGIOUS / SHAREABLE / PRIVATE]
- **Forwarding sentence:** "[what someone would say when sharing]"
- **To whom:** [specific audience]
- **The element:** [what makes it forwardable]
- **Findability:** [is the element easy to find on the page?]

## Dead Weight
[Pages that serve a purpose but will never be shared. This isn't criticism — it's classification.]
- [page] — [why it won't be shared] — [what purpose it serves instead]

## Distribution Assessment
- **Forwardable pages:** [count] / [total published]
- **Primary forwarding audience:** [who would most pages be sent to?]
- **Distribution gap:** [if the ratio is low, what kind of page is missing?]

## The Forwarding Sentence Test
[For the homepage specifically: if someone had to describe the site in one sentence to a friend, what would they say? Is that sentence interesting enough to make the friend visit?]
```

## Direction (if not all passing)

For each page rated PRIVATE that SHOULD be forwardable (based on its strategic role):
- What's currently there (the content that's appreciated but not shared)
- What would make it forwardable (a specific insight, visual element, or framing)
- Which files to modify
- What the forwarding sentence should sound like after the change

## Called By

- `/steward run` — parallel arm (independent, no data dependencies)
- Standalone — usable anytime
