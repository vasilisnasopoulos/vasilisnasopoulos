---
layout: default
title: "A green checkmark is not a proof"
description: "Two independent ways a verification pipeline can report success over a proof that never closed — one from a twenty-year-old prover, one from a language model."
date: 2026-07-31
---

# A green checkmark is not a proof

*31 July 2026*

For about four days at the end of June, one of my public repositories displayed
a passing CI badge over a proof that did not close. Nothing was hidden. The
prover said so, in plain text, in a log anyone could open:

```
[ERROR]: 1/99 obligations failed.
```

GitHub Actions recorded the run as **success**.

I only noticed because I happened to read the log by hand while working on
something else. That is a bad way to find out, so I went looking for how it
happened. What I found was two independent failures with the same shape — one
from a twenty-year-old tool, one from a language model — and it seems worth
writing down, because the fix in both cases is boring and the failure mode is
not.

## The tool that told the truth, quietly

I use TLAPS, the TLA⁺ Proof System, to discharge safety proofs for a consensus
protocol I work on. The CI step was about as simple as it gets:

```yaml
- run: tlapm --toolbox 0 0 Spec.tla
```

`tlapm` reports failures clearly. It prints the summary above. It also emits
structured, machine-readable markers intended for tooling — in that same run,
three of them said `@!!status:failed`.

And then it exits `0`.

That is the whole bug, if it is even a bug: the information exists in every
channel except the one automation reads. The tool was designed for interactive
use inside the Toolbox, where a human is looking at the output. Wiring it into
CI came later, and exit-code semantics were never part of the contract.

Once I knew what to look for, the damage was easy to find. The failing
obligation was real: my `ExactlyOnce` proof was missing a `TypeInvariant`
hypothesis, so the `Process` case did not have `network ⊆ MsgRecord` in scope.
With that carried through, it closes at 131 obligations. A separate
bounded-latency proof had two diameter-induction steps the prover could not
discharge; those are now explicit `OMITTED` with comments, rather than sitting
in a file that looked complete.

The stopgap is three lines:

```sh
tlapm --toolbox 0 0 Spec.tla > tlapm.log 2>&1   # note: no pipe
grep -q '@!!status:failed' tlapm.log && exit 1
```

No pipe, because in `cmd | tee log` the shell reports `tee`'s status, not the
prover's — a second, quieter way to lose the signal. And grep the structured
markers rather than the English summary, because a guard against silent failure
should not itself depend on a message that could be reworded.

## The proof that had never been compiled

A week later I opened a Lean 4 file in another of my repositories. It had been
written by a coding agent, opened as a pull request, and merged. The PR
description was confident and specific:

> **Proved:** `reachable_typeInvariant`, `reachable_committedSupersetsProcessed`,
> `reachable_merkleAgreement`, `reachable_reconciledContainsProcessed`

Three hundred lines of structured induction, named lemmas, a clean invariant
bundle. It looked like exactly what it claimed to be.

There was no `lakefile.lean`. No `lean-toolchain`. No CI.

Which means the file had never been through a compiler. Not once. It was not a
proof that had broken; it was a document shaped like a proof that had never been
checked at all.

I added the build scaffolding and pushed it. Four rounds:

1. `Unknown identifier 'Set'`, `Unknown identifier 'Function.update'`. The proof
   used Mathlib concepts while importing only `Std`. It could never have worked.
2. With Mathlib: `failed to synthesize Repr (Set MsgId)` — you cannot `deriving
   Repr` a structure containing a `Set` — plus four application type mismatches.
3. `Function.update` needed the `Function.update_apply` simp lemma. That cleared,
   the mismatches remained: `simpa ... using hsup k hk` was applying the
   hypothesis before rewriting it. Each step had to be split in two.
4. One error left. The induction case bound its arguments in the wrong order:
   `| step hreach ih hstep` where Lean supplies the induction hypothesis last.
   One name, moved one position.

Then it compiled. No errors, no `sorry`. The theorem is now actually proved, and
CI keeps it that way.

I want to be careful about the moral here. The agent did not hallucinate
nonsense — the structure was sound, the invariant bundle was well chosen, and
after four mechanical fixes the mathematics held up. The failure was not in the
writing. It was that nobody, including me, ran it before calling it proved.

## Reporting it

I filed an issue on `tlaplus/tlapm` with a minimal reproducer: one theorem that
closes, one that cannot.

```tla
THEOREM Provable == 1 = 1
  OBVIOUS

THEOREM Unprovable == 1 = 2
  OBVIOUS
```

Both the current stable release and the rolling pre-release print
`1/2 obligations failed` and exit `0`. The CI run demonstrating this was itself
reported as a success, which felt like the right note to end the report on.

The maintainer replied in twenty minutes, and the answer was: already fixed. A
`--strict` flag had landed six weeks earlier, giving distinct non-zero codes —
10 for a failed obligation, 11 for an incomplete proof, 12 for an empty target.
I confirmed it works: same reproducer, `--strict`, exit 10.

So the mechanism was never the problem. Reach was.

`--strict` exists only in the rolling pre-release. The last stable release is
from October 2022, and the download page still offered it as *the* package, with
no indication that four years of development had happened since. That download
page is where my CI recipe came from in the first place. The README already
pointed at the newer builds; the website had not caught up.

That turned into a small pull request, which is merged. The download pages now
lead with the current builds — including, on macOS, an Apple-silicon build
instead of the 2022 Intel installer that was the only thing on offer before.

## The part that is still open

While preparing that, I looked at how the TLA⁺ community modules repository
verifies its own proofs:

```sh
for proof in *_proofs.tla; do
  tlapm --cleanfp "$proof" || status=1
done
exit $status
```

No `--strict`. Which means: if a contribution breaks one of those proofs today,
`tlapm` exits 0, `|| status=1` never fires, and the build goes green.

Before suggesting anything I ran all six proof modules both ways. They are in
good shape — 2,889 obligations, all discharged, exit 0 with the flag and
without. Adding `--strict` changes nothing about today. It changes what happens
the first time someone breaks something. That patch is open.

## What I actually take from this

Not "tools are bad" or "don't use AI for proofs." Both of those are too easy.

The useful version is narrower. **Verification has a last mile, and it is the
part nobody looks at.** A prover can be sound, a proof can be well-structured,
an author can be careful — and the whole thing can still land in a repository
where the only thing anyone ever checks is a green circle whose connection to
the mathematics was never established.

Three things I would ask of any verification setup now, including my own:

- **Does the check fail?** Not "does it pass" — deliberately break something and
  confirm the pipeline goes red. If you have never seen it fail, you do not know
  that it can.
- **Was it ever run?** For anything generated rather than typed, this is not
  paranoia. A file can look like a proof for a long time before anyone finds out.
- **Are you reading the right signal?** Exit codes, structured output, and prose
  summaries do not always agree. Prefer the one the tool intends for machines,
  and know which one your CI is actually consuming.

Formal methods is the one field whose entire premise is that "it looks right"
should count for nothing. That makes it the field where a convincing-looking
green checkmark does the most damage.

---

*The proofs and reproducers referenced here are public: the TLAPS issue is
[tlaplus/tlapm#287](https://github.com/tlaplus/tlapm/issues/287), the docs fix is
[#288](https://github.com/tlaplus/tlapm/pull/288), and the CI patch is
[tlaplus/CommunityModules#128](https://github.com/tlaplus/CommunityModules/pull/128).
The protocol work that occasioned all of this is Vortex DSE; its public
specifications and proofs are at
[github.com/vasilisnasopoulos-stack](https://github.com/vasilisnasopoulos-stack).*
