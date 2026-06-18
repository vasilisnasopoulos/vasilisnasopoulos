# Vortex DSE — public formal slices

Vortex DSE is **one machine**: a layered protocol stack (admission → agreement →
recovery). The public GitHub repos are **parts of that same machine** — not
separate projects. Each repo publishes one layer, formally checked on its own.

What we do **not** publish today: the whole machine at once (production C, every
layer, and one composed end-to-end theorem wiring all parts together).

## The distinction that matters

| | Meaning |
|---|--------|
| **Part of the machine** | Yes. Admission feeds agreement; agreement assumes admitted ids; all repos share cslot, nodes, and per-slot timing. |
| **The whole machine** | No. Loss recovery, cross-slot memory, wire protocol, and private C are outside the public bundle. |
| **Checked in isolation** | Yes. Each repo has its own TLA+ `Spec` and its own proof or model-check run. |
| **Formally composed together on GitHub** | Not yet. No published refinement imports slice A into slice B under one theorem. |

**Analogy:** you are publishing inspected **components** of one engine (gearbox,
valve, coupling) — not claiming the full assembled engine is proved in one go,
but also **not** claiming the components belong to different engines.

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

Public GitHub today = checked **parts** of this one machine (along the arrow)
Each part verified separately; the assembly proof is future work
```

## How the parts connect

The repos are **layers of the same per-slot pipeline**, not unrelated specs:

```text
                    INTENDED RUNTIME STACK
                    ══════════════════════

  proofs repo          merkle repo              (private, not public)
  admission gate  ──►  AE: Freeze/Reconcile/Commit  ──►  loss / exactly-once …
  (default model)      (baseline, ideal net)

       │                        │
       │   shared vocabulary:   │
       │   cslot, Nodes,        │
       │   processed[n],        │
       │   network records      │
       └───────────┬────────────┘
                   │
         same slot timeline (assumption A1)
```

| Link | Connected in **design**? | Connected in **formal proof** on GitHub? |
|------|--------------------------|------------------------------------------|
| Admission → agreement | Yes — AE runs on locally admitted ids (`processed`) | **No** — no published refinement/composition theorem imports one `Spec` into the next |
| proofs repo ↔ spec repo | Same layer (admission), **two variants** | **No** — different admission rules; not two steps of one pipeline |
| Agreement → loss recovery | Yes — intended next layer | **No** — `AE_Lossy` not public; no composed proof |
| Any slice → production C | Empirical target (private) | **No** — code↔spec refinement not claimed |

**Short version:** each public repo is a **verified part of one machine**.
The parts **connect in order** (admission → agreement → …). What is still open
is a **single composed proof** that imports one `Spec` into the next.

The **strict** spec repo is another **part of the admission layer** (a variant +
adversary model), not the pipe from proofs to merkle. For the main stack:
**proofs** (default admission) → **merkle** (agreement).

## Public slice map

| Part | Question it answers | Public repo | Verification |
|------|---------------------|-------------|--------------|
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

**Can conclude (from a given repo):** that **part of the machine** satisfies the
properties in that repo’s claims matrix, under that part’s assumptions.

**Cannot conclude:** the **fully assembled machine** is verified end-to-end; that
unpublished parts are proved here; that a property proved on part A automatically
holds on the assembled system without a composition proof; or that the strict
spec repo equals the default production admission rule (see
[proofs vs spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs#declared-limits)).

## Suggested reading order

1. This file (how the parts connect).
2. [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) — default admission + what is deductively proved.
3. [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) — per-slot agreement part.
4. [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) — strict admission variant (different rule).

## Two admission models (common confusion)

| Model | Rule | Where |
|-------|------|-------|
| **Default** (late-tolerant) | `m.cslot ≤ current_slot` | proofs repo + matches private C default |
| **Strict** | `m.cslot = current_slot` | spec repo only — pedagogical / TLC variant |

They are **two parts of the admission layer on purpose** — not two unrelated engines.
Compare each claim only to its own repo.
