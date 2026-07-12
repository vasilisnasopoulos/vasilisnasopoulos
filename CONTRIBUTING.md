# Contributing to Vortex DSE Formal Repositories

Thanks for your interest in the Vortex DSE public formal-methods stack.

## Best first contributions

- Improve documentation clarity for readers who are new to TLA+, TLAPS, TLC, or Apalache
- Tighten reproduction steps or fix broken links
- Propose small, well-scoped specification or proof clarifications with rationale
- Open issues that explain the invariant, threat model, or scenario you want to discuss

## Repository map

This hub repository is the landing page and verification guide.

- `formal/vortex-dse-cslot-spec` — executable strict-admission TLA+ model and reference scenarios
- `formal/vortex-dse-cslot-proofs` — TLAPS machine-checked admission safety proofs
- `formal/vortex-merkle-agreement` — per-slot agreement checks with TLC and Apalache

## Local setup

From the repository root:

```sh
git submodule update --init --recursive
```

Then use the commands in [REPRODUCTION.md](REPRODUCTION.md) for the specific proof or model you are touching.

## Change expectations

- Keep changes narrowly scoped and explain the motivation in the pull request
- Preserve reproducibility: update commands or docs if behavior changes
- Do not remove verification assets or weaken stated guarantees without discussion
- Prefer plain-language explanations alongside formal notation when possible

## Pull request checklist

- [ ] Describe what changed and why it matters
- [ ] Link the affected repository, spec, proof, or scenario
- [ ] Run the relevant existing verification command(s) from [REPRODUCTION.md](REPRODUCTION.md)
- [ ] Update README or architecture docs if the newcomer path changed

## Community and questions

If you are unsure where to start, open an issue or discussion with:

1. the repository you were reading
2. the property or scenario you were trying to understand
3. the exact command or file that caused confusion
