---
name: baseline
description: "Baseline checks — mechanical health of the constellation. Links, images, cross-refs, attribution, voice violations, SEO, tooltips. Read-only diagnostic."
user_invocable: true
---

# Baseline Checks — Atomic Skill

## Purpose

Mechanical health checks for the constellation. No judgment, just facts. Pass/fail on every check with specifics on failures.

This covers everything that can be verified by reading files and checking references. It does not evaluate design quality, voice effectiveness, or positioning — those are lens skills.

Read-only diagnostic. Reports pass/fail, never auto-fixes.

## Usage

```
/baseline                  # Run all baseline checks
/baseline [check-name]     # Run a single check (links, images, crossrefs, attribution, voice, seo, tooltips)
```

## Context

### Read
- All published pages (frontmatter + body): `_governance/`, `_infrastructure/`, `_output/`, `_blog/`
- Standalone pages: `bio/index.md`, `contact.md`, `colophon.md`, `thinking.md`, `vocabulary.md`
- Homepage: `_data/index.json` + `_layouts/systemworks.html`
- Screenshots from `.audit/screenshots/` (latest set)
- `docs/visual-reference-index.md` → active reference set
- Reference images from active set (for visual context during evaluation)
- `.audit/rubric.md` if it exists — Peter's annotations override defaults

### Invoke (as needed)
N/A — this IS the mechanical check. Other skills invoke this one.

### Lens Criteria (embedded)
The evaluation questions below ARE this lens's criteria.

## Checks

### 1.1 Links Resolve

- Grep all published markdown files for internal links: `{{ '...' | relative_url }}` patterns and `[...](/path)` patterns
- For each link, verify the target file exists (map URL paths to collection files)
- Also check `_data/index.json` artifact `link` values
- Also check `_data/navigation.json` `url` values
- **Fail** = link target doesn't exist or points to unpublished page

### 1.2 Images Exist

- Grep all published markdown files for image references: `![...](...)` patterns
- For each reference, verify the file exists in `assets/img/`
- **Fail** = referenced image not on disk

### 1.3 Cross-References Hold

- Search all published page body text for mentions of other project names
- If a page mentions a project by name, that project should either (a) be published, or (b) the reference should be generic enough not to imply a link
- **Fail** = reference to unpublished/pulled project

### 1.4 Attribution Chain

- For each spoke repo (has CNAME), check:
  - `index.html` exists with JSON-LD containing `creator` pointing to `petersalvato.com`
  - `README.md` links back to hub
- On the hub, check `_includes/head.html`:
  - Person schema `sameAs` array lists ONLY domains that are actually live (not parked)
- **Fail** = broken attribution link or parked domain in sameAs

### 1.5 Voice Violations

- Read every published page's body content
- Check against banned words: paradigm, leverage, passionate, innovative, synergy, empower, journey, transformative
- Check against banned formulas: "does the thinking", "holds itself", "zero-willpower"
- Check for flame/windbreak metaphor without full setup
- Check for fortune-cookie closing sentences (short declarative sentences that summarize without adding)
- Count em dashes per page: **Fail** if any found. Zero em dashes is the rule.
- Count negation-affirmation patterns per page: **Fail** if more than 1 on any single page.
- **Fail** = any match found (report file and line)

### 1.6 SEO Metadata

- Every published collection page must have: `description`, `seo_keywords`, `last_modified`
- `description` must be unique (no duplicates across pages)
- `last_modified` should be within 90 days (flag if stale, don't fail)
- **Fail** = missing required field or duplicate description

### 1.7 Vocabulary Tooltips Functional

- Build the site (`bundle exec jekyll build`)
- For each vocabulary term in `_data/vocabulary.json`:
  - Search `_site/` HTML for the term appearing as visible text inside scanned containers
  - Count how many pages would show a tooltip for this term
- Report: "X of Y terms appear on at least one page"
- **Fail** = fewer than 6 of 9 terms have at least one matchable occurrence

## Output

Print in conversation. No file changes. Format:

```
# Baseline — [DATE]

## Summary
[NUMBER] checks passed. [NUMBER] failed.

### 1.1 Links — [PASS/FAIL]
[Details on failures if any]

### 1.2 Images — [PASS/FAIL]
[Details]

### 1.3 Cross-References — [PASS/FAIL]
[Details]

### 1.4 Attribution — [PASS/FAIL]
[Details]

### 1.5 Voice — [PASS/FAIL]
[Details: file, line, violation type]

### 1.6 SEO — [PASS/FAIL]
[Details: missing fields, duplicates, stale dates]

### 1.7 Tooltips — [PASS/FAIL]
[X of Y terms matched]
```

## Direction (if not all STRONG)

For each non-passing question, state:
- What specifically is wrong (with evidence from the evaluation)
- What specifically to change (exact change, not "improve X")
- Which files/pages to modify
- What the result should look like after the change

## Called By

- `/audit run` — runs before lenses (lenses depend on baseline results for context)
- Standalone — usable anytime for quick health check
