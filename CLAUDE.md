# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

This is the **index repository** for the Vortex DSE public formal verification bundle. It contains no runnable code — only `README.md` and `SLICES.md`, which explain how the public repos relate to each other and to the private production engine.

## Architecture overview

Vortex DSE is a layered deterministic slot engineering protocol:

```
Admission → Freeze → Reconcile → Commit → (loss recovery, cross-slot — private)
```

The public GitHub surface publishes **parts** of this pipeline as separately verified slices, not one composed end-to-end proof:

| Repo | Layer | Verification method |
|------|-------|---------------------|
| `vortex-dse-cslot-proofs` | Default late-tolerant C-slot admission | TLAPS (unbounded deductive proofs) |
| `vortex-dse-cslot-spec` | Strict same-slot admission + adversary model | TLC bounded model checking + JS reference |
| `vortex-merkle-agreement` | Per-slot input-set agreement (Freeze/Reconcile/Commit) | TLC + Apalache |

The repos share vocabulary (`cslot`, `Nodes`, `processed[n]`, network records, per-slot timing) but **no published refinement theorem** formally composes slice A into slice B.

## Two admission models (common confusion point)

| Model | Admission rule | Location |
|-------|----------------|----------|
| **Default** (late-tolerant) | `m.cslot ≤ current_slot` — late messages admitted into their own slot | `vortex-dse-cslot-proofs` |
| **Strict** | `m.cslot = current_slot` — messages from past slots are dropped | `vortex-dse-cslot-spec` |

These are **two variants of the admission layer**, not two separate engines. Compare claims only within the same repo.

## What is intentionally not public

- Loss recovery under bounded packet loss (`AE_Lossy`)
- Cross-slot exactly-once composition
- Composed admission + agreement + crash/rejoin end-to-end theorem
- Production C simulator (`full2`), benchmarks, wire protocol
