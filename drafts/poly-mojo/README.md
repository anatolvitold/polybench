# Poly Mojo benchmark contribution

**Status: submitted as [tueda/polybench#178](https://github.com/tueda/polybench/pull/178).**

The implementation is on
[`feat/poly-mojo`](https://github.com/anatolvitold/polybench/tree/feat/poly-mojo).
The upstream target is `tueda/polybench:main`. This separate `drafts` branch
preserves the PR description, package records, and validation evidence; it is
not part of the proposed upstream code diff.

- [PR title](title.txt) and [description](pull-request.md)
- [Validation record](validation.md)
- [Submission state](submission-state.json)
- [Pinned environment](https://github.com/anatolvitold/polybench/tree/feat/poly-mojo/environments/polymojo)

The community-channel package is now available: Poly Mojo 1.0.1 and APN Mojo
1.0.2, both build `hb0f4dca_0`, with Mojo 1.2.0. The code branch's Pixi lockfile
pins the exact builds on Linux x86-64. The owner has authorized upstream
submission after checking the installed package; no further approval is needed.

Current code commit: `bbc64e67269c5d42ea232997e972c9023ef05dfe`, rebased onto
upstream `29d2928bf1fbaf97cb47897ba866728f52d49df7`. All 61 Python tests and pre-commit checks
passed again after the rebase. The earlier installed-wheel validation at
`c782c5351fcfcd0039a71dd632197fd6bab00c74` passed 100 measured cases and 20 warmups
against FLINT in both modes; those benchmarks were not rerun for the rebase. [Release checks](release-checks/) preserve the evidence.

## Submission

The owner opened [PR #178](https://github.com/tueda/polybench/pull/178)
from `anatolvitold:feat/poly-mojo` to `tueda/polybench:main` on October 27, 2026.
It now contains the rebased code commit above and is open for review.

The earlier API permission errors are retained as historical information in
[the submission state](submission-state.json); they no longer block submission.

The owner updated the PR description's Quick Start. It now matches
[the verified instructions](quick-start.md), including the pinned manifest path,
`POLY_MOJO_PATH`, and polybench's actual CLI. The description correction is resolved.
