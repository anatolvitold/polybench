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
- [Pinned environment](https://github.com/anatolvitold/polybench/tree/feat/poly-mojo/polybench/solvers/polymojo)

The community-channel package is now available: Poly Mojo 1.0.1 and APN Mojo
1.0.2, both build `hb0f4dca_0`, with Mojo 1.2.0. The code branch's Pixi lockfile
pins the exact builds on Linux x86-64. The owner has authorized upstream
submission after checking the installed package; no further approval is needed.

Current code commit: `a19ed93f5120e510d0b0a2dc52d3baad6a1daa02`, based on
upstream `29d2928bf1fbaf97cb47897ba866728f52d49df7`.

The maintainer's four review points are addressed: CI exercises ordinary and
certified backends; backend resources are grouped together; Pixi installs pinned
packages automatically; and `poetry2pip.py` returns `contains()` directly.
All 74 Python tests and applicable pre-commit hooks pass. Installed-wheel checks
passed 220 measured cases in both modes and another 200 ordinary benchmark cases
against FLINT. [Review checks](review-checks/) preserve the latest evidence;
[release checks](release-checks/) retain the earlier validation.

## Submission

The owner opened [PR #178](https://github.com/tueda/polybench/pull/178)
from `anatolvitold:feat/poly-mojo` to `tueda/polybench:main` on October 27, 2026.
It now contains the updated code commit above and is open for review.

The earlier API permission errors are retained as historical information in
[the submission state](submission-state.json); they no longer block submission.

The submitted PR description still contains the previous manual setup. The
[updated description](pull-request.md) and [Quick Start](quick-start.md) are ready
to replace it. GitHub denied this integration permission to edit the description
(HTTP 403). A [reply to the maintainer](maintainer-reply.md) is drafted but has not
been posted.
