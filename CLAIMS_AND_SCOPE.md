# Public Claims, Evidence, and Scope

The public Vortex DSE repositories publish verified slices and measured demonstrations of a larger research stack. They do **not** publish one composed, end-to-end proof of the private production engine.

| Claim | Evidence | Scope | Not established by this evidence | Primary source |
|---|---|---|---|---|
| Default late-tolerant C-slot admission satisfies the stated admission-model invariants. | TLAPS deductive proofs for `TypeInvariant`, `NoFutureAdmission`, and `StrictExactlyOnce`. | The default model and its declared assumptions; the proofs establish the stated properties of that model. | Refinement to production code, agreement across nodes, or an end-to-end system theorem. | [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos/vortex-dse-cslot-proofs) |
| Strict same-slot admission and its clock-skew/adversarial variants behave as modeled. | TLC bounded checks and executable JavaScript reference scenarios. | The checked finite configurations and scenarios for the strict admission model. | An unbounded proof, all possible adversarial behavior, or a complete consensus guarantee. | [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos/vortex-dse-cslot-spec) |
| Per-slot Merkle agreement holds in the published agreement model. | TLC and Apalache bounded checks, plus a Lean trace-induction formalization. | The transition system, reachable traces, and declared assumptions of that artifact. The model-checking results are bounded; the Lean theorems are about the formalized model. | Refinement to the production implementation, unmodeled network behavior, or composition with admission and recovery as one end-to-end theorem. | [vortex-merkle-agreement](https://github.com/vasilisnasopoulos/vortex-merkle-agreement) ([verification status](https://github.com/vasilisnasopoulos/vortex-merkle-agreement/blob/main/STATUS.md)) |
| WAN, testnet, and demo runs report observed performance or behavior. | Published run measurements, logs, and demo artifacts. | The particular workloads, environments, configurations, and runs documented by each artifact. | Universal performance guarantees or a controlled head-to-head result unless the comparison uses matched conditions and documents them. | [testnet status](https://github.com/vasilisnasopoulos/vortex-testnet-status); [festival demo](https://github.com/vasilisnasopoulos/vortex-festival-demo); [Tesla demo](https://github.com/vasilisnasopoulos/vortex-tesla-demo); [DSS demo](https://github.com/vasilisnasopoulos/vortex-dss-demo) |
| `pick-the-order` invites falsification of arrival-order invariance. | Reported runs and an open challenge using permutations of the same 3,000-transaction set. | The fixed transaction set and the arrival orders exercised or submitted through the challenge. | A complete consensus proof, evidence for arbitrary transaction sets, or a general performance benchmark. | [`pick-the-order`](https://github.com/vasilisnasopoulos/pick-the-order) |
| Production implementation, wire protocol, loss recovery, and full end-to-end composition are not publicly established as one theorem. | The public artifact boundaries and limitations documented in this hub. | These components are unavailable publicly or are not yet publicly composed/proved together. | Any production-code refinement or complete proof inferred from the separate public artifacts. | [SLICES.md](SLICES.md), [ARCHITECTURE.md](ARCHITECTURE.md), and [PROOF_STRUCTURE.md](PROOF_STRUCTURE.md) |

## The two public admission models

The admission repositories describe **variants**, not consecutive stages of one admission rule:

- **Default, late-tolerant:** `m.cslot <= current_slot`, in [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos/vortex-dse-cslot-proofs).
- **Strict, same-slot:** `m.cslot = current_slot`, in [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos/vortex-dse-cslot-spec).

Interpret each result within its own model and stated scope. In particular, the strict model’s bounded checks do not extend the default model’s TLAPS theorems, and the two artifacts do not together establish a single admission theorem.

## Reading the evidence

TLAPS deductively proves the stated theorems from the TLA+ model and assumptions. TLC and Apalache check bounded model instances; executable scenarios demonstrate behavior for their inputs. Measurements report particular observed runs. None of these evidence types, by itself, establishes that the private production implementation refines the model or that separately checked slices compose into a complete end-to-end proof.

See [SLICES.md](SLICES.md) for the public slice map and [REPRODUCTION.md](REPRODUCTION.md) for commands and reproduction limits.
