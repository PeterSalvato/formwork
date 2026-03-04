# Formwork Manifest

Dependency map for all skills in this repository.

## Skill Types

- **Atomic**: Single-purpose, self-contained. Takes input, returns verdict.
- **Coordinator**: Dispatches atomics, collects results, synthesizes.
- **Protocol**: Structured data format or process definition.

## Dependency Map

### Coordinators

| Skill | Dispatches | Sequential Dependencies |
|-------|-----------|----------------------|
| `audit` | `baseline`, then all configured lenses in parallel | Lenses depend on baseline results |

### Lenses (all atomic, all independent)

| Skill | May Invoke | Purpose |
|-------|-----------|---------|
| `millman` | `knowledge`, `baseline` | Authenticity diagnostic |
| `bierut` | `knowledge`, `baseline` | Design-thinking diagnostic |
| `appleton` | `knowledge`, `baseline` | Digital garden patterns |
| `peers` | `baseline`, `discoverability` | Peer benchmark |
| `vignelli` | — | Restraint and clarity |
| `spiekermann` | — | Typography craft |
| `rams` | — | Economy |
| `muller-brockmann` | — | Grid and system |
| `paul-rand` | — | Concept and communication |
| `draplin` | — | Personality-in-craft |
| `lubalin` | — | Typography as idea |
| `materialist` | — | Structural honesty |
| `print-craft` | `texture-verify` | Print artifact quality |

### Diagnostics (all atomic)

| Skill | May Invoke | Purpose |
|-------|-----------|---------|
| `grip-test` | `knowledge` | Copy landing diagnostic |
| `baseline` | — | Mechanical health checks |
| `copy-verify` | — | 12-item copy checklist |
| `convergence` | — | Consensus/contradiction mapping |
| `speed-tiers` | — | Time-based evaluation |
| `forwarding` | — | Forwardability assessment |
| `arc` | — | Cross-page coherence |
| `journeys` | — | Visitor path evaluation |

### Protocols

| Skill | Purpose |
|-------|---------|
| `savepoint` | Decision moment capture |

## Data Flow

```
audit (coordinator)
  ├── baseline (sequential — must complete first)
  │   └── returns: pass/fail per mechanical check
  │
  └── lenses (parallel — all at once after baseline)
      ├── millman → STRONG/HOLDS/WEAK/BROKEN + findings
      ├── bierut → STRONG/HOLDS/WEAK/BROKEN + findings
      ├── appleton → STRONG/HOLDS/WEAK/BROKEN + findings
      ├── peers → STRONG/HOLDS/WEAK/BROKEN + findings
      ├── [additional lenses as configured]
      │
      └── convergence (sequential — needs all lens results)
          └── returns: agreements, contradictions, decision points
```

## Extending

To add a lens:
1. Create `skills/lenses/[name]/SKILL.md`
2. Follow the atomic skill pattern: Purpose, Context, Questions (5), Verdict Scale, Output Format
3. Add to the audit coordinator's dispatch list
4. Update this manifest
