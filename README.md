# 👋 Vasilis Nasopoulos — Vortex DSE

I work on **formal methods** (TLA+, TLAPS) and **distributed systems**: where coordination is needed, how much of it, and how to
build systems that keep working with no central server. The measurements come from **Vortex**, my own leaderless engine.

[![TLAPS checks](https://github.com/vasilisnasopoulos/vasilisnasopoulos/actions/workflows/verify-proofs.yml/badge.svg)](https://github.com/vasilisnasopoulos/vasilisnasopoulos/actions/workflows/verify-proofs.yml)
[![TLC checks](https://github.com/vasilisnasopoulos/vasilisnasopoulos/actions/workflows/verify-tlc.yml/badge.svg)](https://github.com/vasilisnasopoulos/vasilisnasopoulos/actions/workflows/verify-tlc.yml)
[![Apalache checks](https://github.com/vasilisnasopoulos/vasilisnasopoulos/actions/workflows/verify-apalache.yml/badge.svg)](https://github.com/vasilisnasopoulos/vasilisnasopoulos/actions/workflows/verify-apalache.yml)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Topics](https://img.shields.io/badge/topics-formal--methods%20%C2%B7%20tla%2B%20%C2%B7%20consensus-6f42c1)](#-topics)
[![Release notes](https://img.shields.io/badge/release-v1.0.0-orange)](RELEASE_NOTES.md)

## ⭐ Start here — The Silence Theorem

**[where-coordination-goes](https://github.com/vasilisnasopoulos/where-coordination-goes)** — in Hellerstein's *Complete CALM* framework,
the least coordination a commitment needs is a **transversal of silences**: deciding, before they act, that certain participants'
future actions will not count — and exactly how many (τ, in the worst case, for specifications where a refused action leaves no trace).
Paper proofs plus TLAPS-checked cores; what is *not* ours (Berge, coteries/quorums, Hamsaz, …) is stated in the repository.

## 🧭 Repositories

| Repository | What you will find |
|---|---|
| [where-coordination-goes](https://github.com/vasilisnasopoulos/where-coordination-goes) | The Silence Theorem: definitions, proofs (TLAPS), counterexamples, prior art |
| [vortex-dse-formal](https://github.com/vasilisnasopoulos/vortex-dse-formal) | Formal models of the engine: C-slot admission spec, TLAPS proofs (325 obligations), Merkle agreement layer (TLC + Apalache) |
| [vortex-tesla-demo](https://github.com/vasilisnasopoulos/vortex-tesla-demo) | Three cars, one ledger, no server — Tesla fleet-telemetry data across three continents |
| [vortex-festival-demo](https://github.com/vasilisnasopoulos/vortex-festival-demo) | Festival payments with no payment server: registers fail at peak and the rest keep going |
| [vortex-dss-demo](https://github.com/vasilisnasopoulos/vortex-dss-demo) | Drone airspace deconfliction (ASTM F3548 DSS rule) with no leader |
| [vortex-testnet-status](https://github.com/vasilisnasopoulos/vortex-testnet-status) | Live status of the three-node testnet (Frankfurt · Tokyo · Los Angeles) |
| [vortex-dse-whitepaper](https://github.com/vasilisnasopoulos/vortex-dse-whitepaper) | Early whitepaper (August 2026) — background and vocabulary |
| [pick-the-order](https://github.com/vasilisnasopoulos/pick-the-order) · [recovery-safety-property](https://github.com/vasilisnasopoulos/recovery-safety-property) | An open ordering challenge · a recovery-safety property for durable runtimes |

> **Scope:** the public repositories are separate evidence slices — models, proofs, demos — not a proof of the complete production
> engine. See [CLAIMS_AND_SCOPE.md](CLAIMS_AND_SCOPE.md) and [SLICES.md](SLICES.md).

## 🧪 Verify the formal models

```sh
git clone https://github.com/vasilisnasopoulos/vortex-dse-formal && cd vortex-dse-formal/cslot-proofs/specs
tlapm --toolbox 0 0 Vortex_DSE_CSlot_Proofs.tla
tlapm --toolbox 0 0 Vortex_DSE_CSlot_ExactlyOnce_Proof.tla
```
Full commands: [REPRODUCTION.md](REPRODUCTION.md).

## 🗂️ Core resources in this hub repo

- [CLAIMS_AND_SCOPE.md](CLAIMS_AND_SCOPE.md) — canonical claim/evidence/scope matrix for reviewers
- [ARCHITECTURE.md](ARCHITECTURE.md) — cross-repository system map and CI topology
- [PROOF_STRUCTURE.md](PROOF_STRUCTURE.md) — proof/model-check dependency flow
- [REPRODUCTION.md](REPRODUCTION.md) — canonical local reproduction commands
- [SLICES.md](SLICES.md) — public verification slices and boundaries
- [proof-dependencies.json](proof-dependencies.json) — machine-readable dependency graph
- [REPOSITORY_DESCRIPTIONS.md](REPOSITORY_DESCRIPTIONS.md) — suggested one-line GitHub descriptions
- [RELEASE_NOTES.md](RELEASE_NOTES.md) — draft `v1.0.0` release notes for the public formal baseline
- [CONTRIBUTING.md](CONTRIBUTING.md) — contributor onboarding and review expectations
- [README_BLUEPRINTS.md](README_BLUEPRINTS.md) — consistent README section blueprint for all related repos

## 🧾 Scope notes

- These repositories are public formal artifacts; they are not the complete production engine.
- Production C internals, benchmark internals, and some end-to-end composition details remain private.
- Each repository documents assumptions, guarantees, and reproducibility commands for its scope.

## 🔖 Topics

`formal-methods` · `tla+` · `tlaps` · `tlc` · `apalache` · `distributed-systems` · `coordination` · `calm`
