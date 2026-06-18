# Vasilis Nasopoulos

Formal methods and systems research around **Vortex DSE** — deterministic slot
engineering for distributed admission, ordering, and agreement.

## Public formal surface

Production C and benchmarks are **private**. These three repos are the public,
reviewable evidence layer — **parts of one machine**, each formally checked on
its own:

| Repo | Role |
|------|------|
| [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) | Default late-tolerant C-slot model — **TLAPS** proofs |
| [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) | **Strict** admission variant — TLC + JS reference |
| [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) | Per-slot **Merkle agreement** on the admitted input set |

> **Start here:** default model + proofs → **proofs** repo.
> Strict single-slot admission → **spec** repo. They are different variants on purpose.

## Read this first: parts of one machine, not the whole engine

These repos are **verified components of the same Vortex DSE stack** — admission,
agreement, and variants — each checked on its own. They are **not** unrelated
specs, and **not** the full production engine or one composed end-to-end proof.

**[→ SLICES.md](SLICES.md)** — how the parts connect, what is missing, what you
can and cannot conclude.

## Scope

- Machine-checked and model-checked **parts** only — not a full public engine.
- Loss-under-reconcile and cross-slot composition specs are **not** on GitHub yet.
- Questions about private implementation: open an issue on any public repo.

## Topics

`formal-methods` · `tla+` · `distributed-systems` · `consensus`
