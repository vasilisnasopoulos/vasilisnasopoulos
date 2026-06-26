# Unified Proof Structure

This document describes how proofs and model checks connect across the three public repositories.

## Core dependency chain

```text
TypeInvariant
   -> NoFutureAdmission
      -> StrictExactlyOnce
         -> Admission output assumed by Merkle Agreement layer
```

## Detailed flow

1. **`vortex-dse-cslot-proofs` (TLAPS)**
   - `Spec => []TypeInvariant`
   - `Spec => []NoFutureAdmission`
   - `Spec => []StrictExactlyOnce`
   - These are deductive, unbounded safety proofs for the default admission model.

2. **`vortex-dse-cslot-spec` (TLC)**
   - Bounded model-check runs for strict admission variant (`tx.cslot = current_slot`).
   - Used as an executable bounded variant of admission behavior.

3. **`vortex-merkle-agreement` (TLC + Apalache)**
   - Bounded checks for per-slot agreement (`Freeze -> Reconcile -> Commit`).
   - Consumes the conceptual admission output (`processed` / admitted set) as layer input.

## Machine-readable dependency graph

The canonical graph is maintained in:

- [`proof-dependencies.json`](proof-dependencies.json)

It includes:
- theorem/module IDs,
- assumption links,
- inter-repo dependency edges,
- CI checkpoint mapping.
