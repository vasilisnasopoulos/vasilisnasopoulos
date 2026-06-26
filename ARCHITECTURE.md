# Unified Vortex DSE Formal Architecture

This hub repository unifies the three public formal repositories into one verification surface.

## Repository topology

```text
vasilisnasopoulos-stack (hub)
├── formal/vortex-dse-cslot-proofs     (TLAPS deductive proofs)
├── formal/vortex-dse-cslot-spec       (TLC strict-admission bounded checks)
└── formal/vortex-merkle-agreement     (TLC + Apalache agreement checks)
```

## End-to-end architecture (public formal slices)

```text
                   PUBLIC VORTEX DSE FORMAL STACK

  +---------------------------------------------------------------+
  | Layer 1: Admission (default, late-tolerant)                  |
  | Repo: vortex-dse-cslot-proofs                                |
  | Method: TLAPS                                                |
  | Guarantees: TypeInvariant, NoFutureAdmission, StrictExactlyOnce |
  +-----------------------------+---------------------------------+
                                |
                                | admitted message ids / processed sets
                                v
  +---------------------------------------------------------------+
  | Layer 2: Admission Variant (strict same-slot)                |
  | Repo: vortex-dse-cslot-spec                                  |
  | Method: TLC                                                  |
  | Purpose: bounded executable strict-admission model           |
  +-----------------------------+---------------------------------+
                                |
                                | compatibility and comparative analysis
                                v
  +---------------------------------------------------------------+
  | Layer 3: Per-slot Agreement                                  |
  | Repo: vortex-merkle-agreement                                |
  | Method: TLC + Apalache                                       |
  | Guarantees: per-slot committed set agreement under assumptions |
  +---------------------------------------------------------------+
```

## CI architecture

```text
PR / push
  ├─ verify-proofs.yml     -> TLAPS checks in formal/vortex-dse-cslot-proofs
  ├─ verify-tlc.yml        -> TLC checks in strict + merkle repositories
  └─ verify-apalache.yml   -> Apalache bounded check in merkle repository

Any failing workflow blocks merge and signals proof regression.
```

## Source of truth

- Dependency graph: [`proof-dependencies.json`](proof-dependencies.json)
- Flow-level explanation: [`PROOF_STRUCTURE.md`](PROOF_STRUCTURE.md)
- Reproduction commands: [`REPRODUCTION.md`](REPRODUCTION.md)
