# Poly Mojo benchmark contribution

**Status: published-package validation complete; ready for upstream submission.**

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

Prepared code commit: `c782c5351fcfcd0039a71dd632197fd6bab00c74`. All 61 Python tests and pre-commit checks
passed; the installed wheel passed 100 measured cases and 20 warmups against FLINT
in both modes. [Release checks](release-checks/) preserve the evidence.
