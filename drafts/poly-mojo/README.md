# Poly Mojo integration draft

**Status: awaiting a published Poly Mojo release and approval to submit upstream.**

This branch preserves the proposal and validation record. The implementation is
on [`feat/poly-mojo`](https://github.com/anatolvitold/polybench-integration/tree/feat/poly-mojo),
at commit `3cb99b389952c28d483b6632b527be2fcfe50276`. The proposed upstream target is
[`tueda/polybench:main`](https://github.com/tueda/polybench/tree/main).

- [Proposed PR title](title.txt)
- [Proposed PR description](pull-request.md)
- [Validation record](validation.md)

## Release pin

The exact `poly_mojo` release version is **not available yet**. Current code and
instructions were validated against the source revision
`72c92234ba9f0b85a7d8d4476ccb61cb6573716e` with Mojo 1.2.0. That source checkout is
a temporary basis for the draft, not the intended final installation method.

Before opening the upstream pull request:

1. Wait for the intended `poly_mojo` release in the Mojo community channel.
2. Pin that exact release and its compatible Mojo compiler in the setup recipe.
3. Replace the source-build instructions with installation of the released package.
4. Run the Python tests, pre-commit checks, wheel packaging check, and independent
   FLINT comparison against the published package in both certificate modes.
5. Update the PR description and validation record for that release.
6. Obtain approval to submit the PR.

Public storage of this fork is approved. Upstream submission remains on hold.
The `drafts` branch is for proposal material; `feat/poly-mojo` is the code branch
to use for the eventual upstream pull request.
