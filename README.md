# Vasilis Nasopoulos

Formal methods and systems research around **Vortex DSE** — deterministic slot engineering for distributed admission, ordering, and agreement.

## Unified verification infrastructure

![TLAPS](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-proofs.yml/badge.svg)
![TLC](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-tlc.yml/badge.svg)
![Apalache](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-apalache.yml/badge.svg)

This hub now hosts a single formal verification entry point across all three public repositories.

### Start here

- [ARCHITECTURE.md](ARCHITECTURE.md) — unified system map and CI topology
- [PROOF_STRUCTURE.md](PROOF_STRUCTURE.md) — proof and model-check dependency flow
- [REPRODUCTION.md](REPRODUCTION.md) — canonical local reproduction commands
- [proof-dependencies.json](proof-dependencies.json) — machine-readable dependency graph

## Public formal surface

Production C and benchmarks are **private**. These public repositories are the reviewable evidence layer — **parts of one machine**, each checked on its own:

| Repo | Role | Best for |
|------|------|----------|
| [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) | Default late-tolerant C-slot model — **TLAPS** proofs | Readers who want the strongest deductive safety story |
| [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) | **Strict** admission variant — TLC + JS reference | Readers who want an executable, bounded-checkable spec |
| [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) | Per-slot **Merkle agreement** on the admitted input set | Readers who want the agreement layer after admission |

> **Start here:** `vortex-dse-cslot-proofs`
>
> If you want the strict same-slot variant first, go to `vortex-dse-cslot-spec`.

## What to expect

- Machine-checked and model-checked **parts** only — not a full public engine.
- The repositories are intentionally modular: admission, agreement, and variants are checked separately.
- Loss-under-reconcile and cross-slot composition are **not** public yet.
- Each repo explains its own scope, assumptions, and reproduce steps.

## Recommended reading order

1. [ARCHITECTURE.md](ARCHITECTURE.md)
2. [PROOF_STRUCTURE.md](PROOF_STRUCTURE.md)
3. [REPRODUCTION.md](REPRODUCTION.md)
4. [SLICES.md](SLICES.md)
5. [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs)
6. [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec)
7. [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement)

## Topics

`formal-methods` · `tla+` · `distributed-systems` · `consensus`
