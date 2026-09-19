
## Review kit (mandatory)

Replace `/Users/navidrashik/Documents/Zealve/zealve-roadmap/.git/review-kit` below with the path install.sh printed; it ends in `.git/review-kit`.

### Rule one, before anything else: establish the surface, then read

**Do not search the tree to find out what a change touches.** Two lookups come before the first
source file is opened, and they have an order:

```
rk memory find "<topic>"        step one - the memory bank: what a human already wrote down
                                about this feature - traps, constraints, owning paths
rk impact --base main           step two - the graph: which files depend on the change, which
                                tests cover them, which entrypoints QA has to exercise
```

**`rk map --base main --freeze` is the one command that does both**, and that is the reason to
reach for it: it consults the bank as one of its four sources, merges that with the graph and the
data coupling, and freezes the result as the impact contract every later gate checks. `rk impact`
is the graph half on its own — it does not consult the bank, so step one is still owed after it.

The bank comes first because the two answer different questions. The graph answers *what depends
on what*. The bank answers *what a human already learned and wrote down* — a trap someone already
paid for, a constraint, the owning path — and no graph reconstructs that from syntax. Each half is
owed only where the repo has it: with no bank yet there is nothing to consult, so that half is
vacuous, and with no graph `rk memory find` is the whole of what is owed, because neither
`rk impact` nor `rk map` can run without one.

Then read the feature docs `/Users/navidrashik/Documents/Zealve/zealve-roadmap/.git/review-kit/memory-bank/index.md` names, and search the tree **only**
for what the two came back UNRESOLVED on — that residue is the sole part of the tree a search can
add to. Everything else it would tell you, the graph already knows, and knows more precisely: the
impacted files, the tests that cover them, the entrypoints to exercise. A surface derived from
grepping is a guess, and every scope built on it — what to read, what a subagent may touch, what
QA must cover — inherits the guess.

**This one is enforced, not requested.** In a repo with a graph or a memory bank, a tree-wide
search before those lookups is refused by review-kit's hook, in every harness it is installed
in. The refusal names what satisfies it; `rk map --base main --freeze` satisfies both steps in
one run, and an already-frozen contract for the branch clears it outright. There is no way to
earn an exception and no reason to want one — the way out is `REVIEW_KIT_DISABLE`, a
comma-separated list of gate names. `REVIEW_KIT_DISABLE=surface` turns off this gate alone and
leaves the claim, done and converge gates armed; `REVIEW_KIT_DISABLE=1` turns the whole kit off.
Both say so in the refusal, and a report that relied on either names which one.

### The rest

1. **Run the tests `rk impact` names.** If it names an entrypoint you did not know about,
   stop and re-read the feature doc before writing code.
2. **The merge decision is a command, not an opinion.** `rk scan --base main
   --fail-on-blocking` is the deterministic gate and must be clean; `rk ledger verdict
   --key <branch>` is authoritative and has three answers: `MERGEABLE` at exit 0,
   `BLOCKED` at exit 1, and `NO VERDICT` at exit 2 for a ledger nothing was ever
   ingested into. Exit 2 is not a pass — it says no review reached this ledger. Never
   dismiss a finding to make it pass — `rk ledger dismiss` is a human's call, recorded
   in `review-ignore.md`.
3. **Never re-run a full review when a ledger exists for this branch.** Round 1 saw the
   whole diff; every later round is delta-only. Run `rk ledger next-round --key <branch>`,
   review *only* the `<old>..<new>` range it prints, and stop if it prints `LOCKED` (round
   cap reached — ship or escalate). Re-reviewing everything is how the loop fails to end.
4. **Label every finding** `REPRODUCED` / `OBSERVED` / `REASONED` / `SPECULATIVE`. Only the
   first two may block, and closing one needs a before/after pair: the same command
   captured failing, then passing. No failing before-state means the bug was imagined.

If your harness has review-kit's slash commands installed, `/rk-map` is rule one in one
command and `/rk-memory` then `/rk-impact` are its two halves; `/rk-done` and `/rk-next`
are rules 2-3. The exit code is still the answer.
