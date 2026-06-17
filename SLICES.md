# Vortex DSE — public formal slices

Vortex DSE is a layered protocol stack (admission → agreement → recovery).
The GitHub repositories under this account publish **formal slices**: each repo
checks **one layer in isolation**, with its own assumptions and verification
method. They are **not** a single composed end-to-end proof and **not** the
production C engine.

## Mental model

```text
Full Vortex DSE (private implementation + unpublished formal layers)
═══════════════════════════════════════════════════════════════════

  [Admission]  →  [Freeze]  →  [Reconcile]  →  [Commit]  →  (later layers…)
       │              │              │             │
       │              └──────────────┴─────────────┘
       │                    agreement family
       │
       └── crash/rejoin, cross-slot memory, loss, wire protocol …

Public GitHub today = separate checked SLICES along that stack
(not one connected theorem)
```

## Public slice map

| Slice | Question it answers | Public repo | Verification |
|-------|---------------------|-------------|--------------|
| Default C-slot admission | Can a node admit a future-dated message? (default model) | [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) | **TLAPS** (deductive, unbounded over parameters) |
| Strict C-slot + adversary | How does strict same-slot admission behave? Clock skew / spoofing? | [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) | **TLC** + JS reference (bounded instances) |
| Baseline per-slot agreement | After admission, do nodes commit the same input set per slot? (ideal network) | [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) | **TLC** + Apalache (bounded instances) |

## Not public (do not infer from the repos above)

| Layer | Status |
|-------|--------|
| Agreement under bounded packet loss (`AE_Lossy`) | Private staging — not on GitHub |
| Cross-slot exactly-once composition | Private staging — not on GitHub |
| Composed admission + agreement + crash/rejoin | Future formal work |
| Multi-round Bloom/Merkle wire reconciliation | Abstracted in public AE; not unfolded |
| Production C simulator (`full2`), benchmarks, demos | Intentionally private |

## What reviewers can and cannot conclude

**Can conclude (from a given repo):** the properties listed in that repo’s
claims matrix hold **inside that slice’s model and assumptions**.

**Cannot conclude:** the full running system is verified end-to-end; that
unpublished layers are proved here; or that the strict spec repo equals the
default production admission rule (see [proofs vs spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs#declared-limits)).

## Suggested reading order

1. This file (slice boundaries).
2. [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) — default admission + what is deductively proved.
3. [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) — per-slot agreement slice.
4. [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) — strict variant + adversarial extension (different admission rule).

## Two admission models (common confusion)

| Model | Rule | Where |
|-------|------|-------|
| **Default** (late-tolerant) | `m.cslot ≤ current_slot` | proofs repo + matches private C default |
| **Strict** | `m.cslot = current_slot` | spec repo only — pedagogical / TLC slice |

They are **different slices on purpose**. Compare each claim only to its own repo.
