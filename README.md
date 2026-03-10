# Formwork

The accommodation design process for AI-assisted creative and engineering work. Every tool in this repo started with the same question: what does the system actually need to do the job?

The theory is [Accommodation Design](https://github.com/PeterSalvato/accommodation-design). Formwork is the process that implements it. In concrete construction, formwork is the temporary structure you pour into. It shapes the work while things are fluid. Once the concrete sets, the form comes off.

**Framework:** [Accommodation Design](https://github.com/PeterSalvato/accommodation-design) (whitepaper)
**Process:** [Formwork](https://petersalvato.com/governance/formwork-protocol/)
**Blog:** [What I Built This Year](https://petersalvato.com/essays/what-i-built-this-year/)

## What this is

A toolkit of [Claude Code skills](https://docs.anthropic.com/en/docs/claude-code/skills) — structured prompts that accommodate specific processing constraints in AI-assisted work. Each tool addresses a real constraint: context window limits, attention degradation, compound evaluation flattening, voice drift, knowledge loss between sessions.

The tools implement two patterns:

**Atomic skills** are single-purpose. One objective, one output. A lens asks five questions and returns a verdict. A diagnostic checks one dimension and reports pass/fail. This is the accommodation move: instead of giving a model twelve objectives at once (which it flattens into mush), you decompose into single-objective tasks that the model can actually do well.

**Coordinators** dispatch atomic skills in parallel, collect results, and synthesize. The audit coordinator runs baseline checks, then dispatches all configured lenses simultaneously. Each lens evaluates the same material from a different perspective. Where they agree, you have a strong signal. Where they disagree, you have a decision to make.

## The toolkit

### Context Preservation

| Tool | Constraint | Solution |
|------|-----------|----------|
| **savepoint** | Context disappears between sessions | Structured semantic markers that capture cognitive turning points in the moment they happen |

### Evaluation Lenses

Each lens extracts an evaluative framework from a specific practitioner's body of work. The criteria are testable — they produce verdicts (STRONG / HOLDS / WEAK / BROKEN), not feelings.

| Lens | Source | Tests |
|------|--------|-------|
| **millman** | Debbie Millman | Is this person real? Differentiation, vulnerability, life-arc coherence |
| **bierut** | Michael Bierut | Does the design think? Problem-solving over decoration |
| **appleton** | Maggie Appleton | Is the knowledge alive? Digital garden patterns, growth, connections |
| **peers** | Peer comparison set | Where does this stand against established practitioners? |
| **vignelli** | Massimo Vignelli | Is the restraint producing clarity? Type, grid, color economy |
| **spiekermann** | Erik Spiekermann | Typography craft. Spacing, hierarchy, micro-details |
| **rams** | Dieter Rams | Economy. Is everything earning its place? |
| **muller-brockmann** | Josef Muller-Brockmann | The grid. Is the system visible? |
| **paul-rand** | Paul Rand | Concept. Does the design communicate an idea? |
| **draplin** | Aaron Draplin | Personality-in-craft. Does this feel human? |
| **lubalin** | Herb Lubalin | Typography as idea. Is the type doing something? |
| **materialist** | Ando/Kahn/Scarpa/Breuer | Is this built or decorated? Structural honesty |
| **print-craft** | Print production standards | Does it feel printed? Material qualities of a pressed artifact |

### Copy and Structure Diagnostics

| Tool | Constraint | Solution |
|------|-----------|----------|
| **grip-test** | Can't tell if copy lands until a stranger reads it | Stranger test with Fingernail / Grip / Lock rating |
| **copy-verify** | Voice drifts without mechanical checks | 13-item pass/fail checklist for published copy |
| **baseline** | Mechanical health degrades silently | Links, images, cross-refs, voice violations, SEO |
| **convergence** | Single-lens evaluation misses the picture | Maps where lenses agree and disagree |
| **speed-tiers** | Different visitors read at different depths | What registers in 10 seconds, 2 minutes, 20 minutes |
| **forwarding** | Work that isn't remarkable doesn't spread | Per-page forwardability rating |
| **arc** | Cross-page coherence breaks without tracking | Does the through-line hold across the full site? |
| **journeys** | The author's path isn't the visitor's path | Three visitor paths evaluated for coherence |

### Coordinators

| Coordinator | Purpose |
|-------------|---------|
| **audit** | Dispatches baseline + all lenses in parallel, synthesizes results |

## How to use

1. Clone this repo
2. Symlink skills into your Claude Code skills directory: `ln -s /path/to/formwork/skills/lenses/millman ~/.claude/skills/millman`
3. Or copy individual SKILL.md files into your project's `.claude/skills/` directory
4. Run any skill by name: `/millman`, `/grip-test`, `/baseline`, etc.

## The extraction method

The lenses weren't generated by asking Claude to "act as Vignelli." They were built by:

1. Studying the practitioner's actual output across their career
2. Extracting the framework — what questions do they consistently ask? What do they never tolerate?
3. Codifying as testable criteria that produce verdicts against real work
4. Validating against work the practitioner produced or praised

This is the difference between "act as" (which produces caricature) and extraction (which produces diagnostic tools). The [Lens Extraction](https://petersalvato.com/essays/lens-extraction/) essay explains the method in detail.

## The accommodation pattern

Every tool in this repo follows the same pattern:

1. **Identify the processing constraint.** What does the model struggle with? (Compound evaluation, voice consistency, context loss, knowledge degradation)
2. **Design the accommodation.** What does the model need to do the job well? (Decomposed objectives, voice samples, semantic markers, traversal protocols)
3. **Build the scaffold.** Structure the input so the model's processing profile works for you instead of against you.

This is the same move a special education teacher makes when designing an IEP. You don't fight the student's processing profile. You design the task to meet it. The [whitepaper](https://github.com/PeterSalvato/accommodation-design) documents the full framework.

## What's not included

This repo contains the transferable toolkit — frameworks anyone can apply to their own work. Personal calibrations (voice governance derived from my conversation patterns, identity-specific lenses, site-specific positioning tools) are private. The toolkit transfers. The calibration is yours to build.

## Author

**[Peter Salvato](https://petersalvato.com)** — Design engineer.

## License

MIT

## Context

Formwork is the process layer of [Accommodation Design](https://github.com/PeterSalvato/accommodation-design). The [System Vocabulary](https://petersalvato.com/vocabulary/) defines terms like [formwork](https://petersalvato.com/vocabulary/#formwork), [drift](https://petersalvato.com/vocabulary/#drift), [scaffold](https://petersalvato.com/vocabulary/#scaffold), and [accommodation design](https://petersalvato.com/vocabulary/#accommodation-design).

Full methodology: [petersalvato.com/governance/formwork-protocol/](https://petersalvato.com/governance/formwork-protocol/)
