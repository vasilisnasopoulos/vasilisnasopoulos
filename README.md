# 👋 Vasilis Nasopoulos — Vortex DSE

I work on **formal methods**, **TLA+**, **TLAPS machine-checked proofs**, and correctness-first **distributed systems / consensus**.

This profile is the public landing page for the Vortex DSE artifacts: from whitepaper ➜ executable specification ➜ deductive proofs ➜ agreement model.

## 🚀 What is Vortex DSE?

**Vortex DSE** is a deterministic ordering and agreement research stack for distributed systems:

- Admission logic formalized in **TLA+**
- Safety obligations proved with **TLAPS**
- Bounded behavior validated with **TLC** and **Apalache**
- Reference scenarios provided for easier implementation alignment

## 🧭 Quick Navigation (all public repos)

| Repository | What you will find | Start here |
|---|---|---|
| [vortex-dse-whitepaper](https://github.com/vasilisnasopoulos-stack/vortex-dse-whitepaper) | Paper, figures, high-level motivation, and research framing | Read abstract + intro first |
| [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) | Strict C-slot admission TLA+ model + JS reference scenarios | Run TLC tiny config, then JS examples |
| [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) | TLAPS machine-checked proofs (194 obligations proved) for admission safety | Verify proofs locally with `tlapm` |
| [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) | Per-slot Merkle agreement layer with TLC + Apalache checks | Run `run_tlc.sh`, then `run_apalache.sh` |
| [vasilisnasopoulos-stack](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack) | Portfolio hub, architecture map, reproduction guide, dependency flow | Continue with sections below |

## ⚡ Getting Started (new visitor, < 2 minutes)

1. Read the [whitepaper repo](https://github.com/vasilisnasopoulos-stack/vortex-dse-whitepaper) to understand problem, goals, and terminology.
2. Open [cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) to see the executable strict admission model.
3. Open [cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) to inspect TLAPS theorems and local proof verification.
4. Open [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement) to see post-admission convergence/commit.
5. Use this repo’s [REPRODUCTION.md](REPRODUCTION.md) to run the same checks locally.

## 🧪 Verification status

![TLAPS](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-proofs.yml/badge.svg)
![TLC](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-tlc.yml/badge.svg)
![Apalache](https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack/actions/workflows/verify-apalache.yml/badge.svg)

## 🧱 Component map (how repos connect)

```text
Whitepaper
   ↓
C-slot Spec (strict admission, executable)
   ↓
C-slot Proofs (late-tolerant admission, TLAPS safety)
   ↓
Merkle Agreement (Freeze → Reconcile → Commit)
```

- Spec + proofs cover admission properties from complementary angles.
- Merkle agreement models convergence after admission output.

## 📚 Repo-by-repo quick start

### 1) `vortex-dse-cslot-proofs`

- **TLAPS in plain words:** TLAPS is the TLA+ Proof System that checks formal proof steps mechanically.
- **What is proved:** 194 proof obligations, including invariants around type safety, no-future admission, and exactly-once admission behavior.
- **Verify locally:**
  ```sh
  tlapm --toolbox 0 0 specs/Vortex_DSE_CSlot_Proofs.tla
  tlapm --toolbox 0 0 specs/Vortex_DSE_CSlot_ExactlyOnce_Proof.tla
  ```
- **Related repo:** [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec)

### 2) `vortex-dse-cslot-spec`

- **Focus:** strict admission (`tx.cslot = current_slot`) modeled in TLA+.
- **Structure:** core model + skew/adversarial variants + TLC configs + JS reference implementation.
- **Run locally:**
  ```sh
  java -jar tla2tools.jar -workers auto \
    -config specs/Vortex_DSE_CSlot_tiny.cfg \
    specs/Vortex_DSE_CSlot.tla
  node ref_impl/cslot_ref.mjs
  ```
- **Compare with:** [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs) and [vortex-merkle-agreement](https://github.com/vasilisnasopoulos-stack/vortex-merkle-agreement)

### 3) `vortex-merkle-agreement`

- **Focus:** per-slot agreement after admission (Freeze → Reconcile → Commit).
- **Verification:** TLC plus bounded checking with Apalache.
- **Run locally:**
  ```sh
  ./run_tlc.sh /path/to/tla2tools.jar
  APALACHE_BIN=/path/to/apalache-mc ./run_apalache.sh
  ```
- **Depends conceptually on:** admission output from C-slot repos.

### 4) `vortex-dse-whitepaper`

- **Focus:** research narrative, architecture intuition, and key claims.
- **Use it for:** terminology and threat/assumption context before reading specs/proofs.
- **Then continue to:** [vortex-dse-cslot-spec](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-spec) and [vortex-dse-cslot-proofs](https://github.com/vasilisnasopoulos-stack/vortex-dse-cslot-proofs)
- **Citation guidance:** see the whitepaper repo for canonical citation text and versioning.

## 🗂️ Core resources in this hub repo

- [ARCHITECTURE.md](ARCHITECTURE.md) — cross-repository system map and CI topology
- [PROOF_STRUCTURE.md](PROOF_STRUCTURE.md) — proof/model-check dependency flow
- [REPRODUCTION.md](REPRODUCTION.md) — canonical local reproduction commands
- [SLICES.md](SLICES.md) — public verification slices and boundaries
- [proof-dependencies.json](proof-dependencies.json) — machine-readable dependency graph
- [REPOSITORY_DESCRIPTIONS.md](REPOSITORY_DESCRIPTIONS.md) — suggested one-line GitHub descriptions
- [README_BLUEPRINTS.md](README_BLUEPRINTS.md) — consistent README section blueprint for all related repos

## 🧾 Scope notes

- These repositories are public formal artifacts; they are not the complete production engine.
- Production C internals, benchmark internals, and some end-to-end composition details remain private.
- Each repository documents assumptions, guarantees, and reproducibility commands for its scope.

## 🔖 Topics

`formal-methods` · `tla+` · `tlaps` · `tlc` · `apalache` · `distributed-systems` · `consensus`
