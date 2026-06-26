# Unified Reproduction Guide

All commands below are run from the hub repository root.

## 1) Clone with submodules

```sh
git clone --recurse-submodules https://github.com/vasilisnasopoulos-stack/vasilisnasopoulos-stack.git
cd vasilisnasopoulos-stack
```

If already cloned:

```sh
git submodule update --init --recursive
```

## 2) TLAPS (default admission proofs)

Requires `tlapm` (or run via Docker image `tlaplus/tlaplus:latest`):

```sh
cd formal/vortex-dse-cslot-proofs
tlapm --toolbox 0 0 specs/Vortex_DSE_CSlot_Proofs.tla
tlapm --toolbox 0 0 specs/Vortex_DSE_CSlot_ExactlyOnce_Proof.tla
```

Expected: `All obligations proved.`

## 3) TLC bounded checks

Download `tla2tools.jar` and run:

```sh
curl -fsSL -o tla2tools.jar https://github.com/tlaplus/tlaplus/releases/latest/download/tla2tools.jar

java -jar tla2tools.jar -workers auto \
  -config formal/vortex-dse-cslot-spec/specs/Vortex_DSE_CSlot_tiny.cfg \
  formal/vortex-dse-cslot-spec/specs/Vortex_DSE_CSlot.tla

java -jar tla2tools.jar -workers auto \
  -config formal/vortex-dse-cslot-spec/specs/Vortex_DSE_CSlot_Skew_tiny.cfg \
  formal/vortex-dse-cslot-spec/specs/Vortex_DSE_CSlot_Skew.tla

(cd formal/vortex-merkle-agreement && ./run_tlc.sh "$PWD/../../tla2tools.jar")
```

## 4) Apalache bounded model checking

Using docker:

```sh
docker run --rm \
  -v "$PWD":/workspace \
  -w /workspace/formal/vortex-merkle-agreement \
  ghcr.io/informalsystems/apalache:latest \
  ./run_apalache.sh 8
```

## 5) CI parity

The same checks are automated in:

- `.github/workflows/verify-proofs.yml`
- `.github/workflows/verify-tlc.yml`
- `.github/workflows/verify-apalache.yml`
