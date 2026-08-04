# README Blueprints for Vortex DSE Repositories

Use these sections to keep formatting, navigation, and onboarding consistent across all repos.

## Shared section order

1. Title + one-line purpose
2. Why this repo matters
3. Quick Start / Getting Started
4. What is verified / proved
5. How this repo connects to the other Vortex DSE repos
6. Reproduction commands
7. Next reading path

---

## `vortex-dse-cslot-proofs` blueprint notes

- Explain TLAPS simply: "TLAPS is a machine-checker for TLA+ proofs."
- Mention status: 325 obligations proved (194 + 131 across two modules).
- Enumerate theorem families in plain language:
  - type consistency invariant
  - no-future admission safety
  - exactly-once admission safety
- Quick Start must include:
  ```sh
  tlapm --toolbox 0 0 specs/Vortex_DSE_CSlot_Proofs.tla
  tlapm --toolbox 0 0 specs/Vortex_DSE_CSlot_ExactlyOnce_Proof.tla
  ```
- Cross-link to:
  - `vortex-dse-cslot-spec`
  - `vortex-merkle-agreement`
  - `vortex-dse-whitepaper`

## `vortex-dse-cslot-spec` blueprint notes

- Explain strict C-slot admission clearly (`tx.cslot = current_slot`).
- Include TLA+ file map (main model, skew/adversarial variants, configs).
- Include JavaScript reference snippet/command.
- Add a short comparison section:
  - strict C-slot vs late-tolerant admission
  - local admission vs agreement/consensus phases
- Cross-link to proofs and Merkle agreement repos.

## `vortex-merkle-agreement` blueprint notes

- Explain per-slot Merkle agreement in plain language:
  Freeze → Reconcile → Root equality check → Commit.
- Include TLC + Apalache verification commands.
- State clearly how it consumes admission output from C-slot repos.
- Cross-link to specification/proofs/whitepaper.

## `vortex-dse-whitepaper` blueprint notes

- Start with direct paper link/navigation.
- Add concise "key insights" bullets.
- Link to implementation artifacts:
  - spec repo
  - proofs repo
  - Merkle agreement repo
- Include a "How to cite" section with canonical citation text.

## `vasilisnasopoulos` (profile) blueprint notes

- Keep as portfolio landing page/hub.
- Provide fast nav to all repositories.
- Keep a <2 minute newcomer path.
- Include badge/status + verification resource links.
