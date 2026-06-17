# Vasilis Nasopoulos

Formal methods and systems research around **Vortex DSE** — deterministic slot
engineering for distributed admission, ordering, and agreement.

## Public formal surface

Production C and benchmarks are **private**. These three repos are the public,
reviewable evidence layer:

| Repo | Role |
|------|------|
| [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) | Default late-tolerant C-slot model — **TLAPS** proofs |
| [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) | **Strict** admission variant — TLC, Apalache, JS reference |
| [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) | Per-slot **Merkle agreement** on the admitted input set |

> **Start here:** default model + proofs → **proofs** repo.
> Strict single-slot admission → **spec** repo. They are different variants on purpose.

## Scope

- Machine-checked and model-checked **slices** of the protocol — not a full public engine.
- Loss-under-reconcile specs exist in private staging; not all are published yet.
- Questions about private implementation: open an issue on any public repo.

## Topics

`formal-methods` · `tla+` · `distributed-systems` · `consensus`
