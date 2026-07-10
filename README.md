# Vasilis Nasopoulos

I work on **formal methods**, **TLA+**, **machine-checked proofs**, and **correctness-first distributed systems**.
This profile repository is the public hub for my Vortex DSE portfolio: a coherent chain from whitepaper to specification to proofs, with executable reference scenarios and agreement models.

## Focus

- Formal specification in **TLA+**
- Model checking with **TLC** and **Apalache**
- Machine-checked proofs with **TLAPS**
- Consensus protocols, deterministic admission, and agreement in distributed systems

## Portfolio map

| Step | Repository | What it shows | Description copy |
|---|---|---|---|
| 1. Whitepaper | [vortex-dse-whitepaper](https://github.com/vasilisnasopoulos-stack/vortex-dse-whitepaper) | Research paper, figures, and a small public demo that introduce Vortex DSE | Whitepaper and public demo for Vortex DSE: correctness-first distributed consensus research at the physical lower bound. |
| 2. Specification | [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) | Executable **TLA+** spec for strict C-slot admission, plus TLC configurations and JavaScript reference scenarios | TLA+ specification, TLC models, and JavaScript reference scenarios for the Vortex DSE strict C-slot admission rule. |
| 3. Proofs | [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) | **TLAPS** machine-checked safety proofs for the late-tolerant admission model | TLAPS machine-checked safety proofs for the Vortex DSE late-tolerant C-slot admission model. |
| 4. Agreement layer | [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) | **TLA+** model of per-slot Merkle agreement after admission | TLA+ model of the Vortex DSE Merkle agreement layer, checked with TLC and Apalache. |
| Hub | [vasilisnasopoulos-stack](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack) | Profile README and cross-repo navigation for the full public portfolio | Formal methods portfolio hub for Vasilis Nasopoulos: whitepaper, TLA+ specs, TLAPS proofs, and distributed agreement models. |

## Recommended reading path

1. Start with [vortex-dse-whitepaper](https://github.com/vasilisnasopoulos-stack/vortex-dse-whitepaper) for the problem statement, terminology, and high-level protocol motivation.
2. Continue to [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) for the executable admission specification and reference scenarios.
3. Read [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) for machine-checked TLAPS safety proofs of the admission model.
4. Finish with [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) for the agreement layer that follows admission.

## Verification infrastructure

![TLAPS](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-proofs.yml/badge.svg)
![TLC](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-tlc.yml/badge.svg)
![Apalache](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-apalache.yml/badge.svg)

### Start here

- [ARCHITECTURE.md](ARCHITECTURE.md) — cross-repository system map and CI topology
- [PROOF_STRUCTURE.md](PROOF_STRUCTURE.md) — proof and model-check dependency flow
- [REPRODUCTION.md](REPRODUCTION.md) — canonical local reproduction commands
- [SLICES.md](SLICES.md) — public verification slices and boundaries
- [proof-dependencies.json](proof-dependencies.json) — machine-readable dependency graph

## Scope notes

- These repositories are the **public formal artifacts** for the work; they are not a full public engine.
- The portfolio is intentionally modular: whitepaper, specification, proofs, and agreement are exposed as separate reviewable artifacts.
- Production C, benchmark internals, and some end-to-end composition details remain private.
- Each repository documents its own assumptions, guarantees, and reproduction steps.

## Topics

`formal-methods` · `tla+` · `tlc` · `tlaps` · `distributed-systems` · `consensus`
