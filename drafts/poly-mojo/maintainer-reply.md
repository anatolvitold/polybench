Thanks for the suggestions. All four points are addressed in `a19ed93` and `5deaeb1`:

1. The Python 3.7–3.13 `testrun` jobs now exercise both `polymojo` and `polymojocertified`; `bench` runs ordinary Poly Mojo. Setup failures and missing or inconsistent results fail the jobs. The legacy Python 3.6 container continues to skip Mojo.
2. The Pixi manifest and lockfile are now alongside the driver under `polybench/solvers/polymojo/`, together with the CI result checker.
3. The adapter installs the locked packages automatically through Pixi, including the matching Mojo compiler. Both modes share the environment and cached driver. The README now shows a single benchmark command, with no manual activation or package-path configuration.
4. Removing the obsolete `type: ignore` is sufficient for mypy. `SpecifierSet.contains()` is returned directly; the redundant `bool()` conversion was removed in its own commit.

All 74 Python tests and pre-commit checks pass locally. A fresh installed wheel passed 220 measured cases in both modes and 200 additional ordinary benchmark cases against FLINT, using the upstream test and benchmark parameters. Every certificate check passed. The validation details are in the [review record](https://github.com/anatolvitold/polybench/blob/drafts/drafts/poly-mojo/validation.md).
