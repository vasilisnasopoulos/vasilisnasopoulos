# Release Notes

## v1.0.0 — Public formal baseline

This milestone packages the public Vortex DSE formal-methods artifacts into a clearer newcomer path.

### Highlights

- Unified hub README with architecture, quick-start flow, and reproducibility links
- Cross-repository verification workflows for TLAPS, TLC, and Apalache
- Public architecture and proof-dependency documentation
- Contributor guide and GitHub Pages landing page for broader discoverability

### Included repositories

- `vasilisnasopoulos-stack` — hub, navigation, architecture, reproduction, badges
- `vortex-dse-whitepaper` — motivation, terminology, research framing
- `vortex-dse-cslot-spec` — executable strict-admission model
- `vortex-dse-cslot-proofs` — machine-checked admission safety proofs
- `vortex-merkle-agreement` — per-slot agreement model

### Why mark `v1.0.0`

- It establishes a stable public starting point for researchers, reviewers, and new contributors
- It groups the currently published formal artifacts into a coherent reference release
- It provides a reusable summary for a GitHub Release or milestone announcement

### Suggested GitHub release title

`v1.0.0 — Vortex DSE public formal baseline`

### Suggested GitHub release body

```markdown
This release marks the first unified public baseline for the Vortex DSE formal stack.

Included in this milestone:

- whitepaper and research framing
- executable TLA+ strict-admission model
- TLAPS machine-checked admission safety proofs
- Merkle agreement checks with TLC and Apalache
- hub documentation for architecture, reproduction, and onboarding

Recommended reading path:

1. whitepaper
2. cslot-spec
3. cslot-proofs
4. merkle-agreement
```
