# Validation of the source-based integration draft

Validated on 2026-10-25. These results describe the source-based draft; validation
against a published community-channel package is still pending.

| Component | Version or revision |
|---|---|
| Integration | `3cb99b389952c28d483b6632b527be2fcfe50276` |
| Upstream polybench base | `910864a14999f0861821ecd67747006843f3fc51` |
| Poly Mojo source | `72c92234ba9f0b85a7d8d4476ccb61cb6573716e` |
| Mojo | 1.2.0 (`2016d0cd`) |
| Python | 3.12.14 |
| FLINT | 3.3.1, compiled with GCC 14.2.0 |
| Platform | Linux x86-64, Intel Xeon Platinum 8573C |

## Checks passed

- All 61 Python tests, without requiring Mojo for the test suite.
- All configured pre-commit hooks and the commit-message check.
- Python 3.6 grammar parsing for the new Python files. The complete upstream
  Python-version CI matrix was not run locally.
- Built and installed the wheel in a separate environment. Its adapter and Mojo
  driver matched the proposed code byte for byte.
- The installed wheel passed all 100 measured cases and 20 warmups against
  FLINT in ordinary and certified modes, including every certificate check.
- Generated inputs matched the previous independent polybench pilot byte for byte.
- Zero library recompilations, two shared driver compilations, and 22 driver
  cache reuses during the installed-wheel comparison.

## Independent benchmark inputs

The run used polybench's unchanged generator and FLINT adapter, seed 42, uniform
exponents, and all four families: trivial/nontrivial GCD and trivial/nontrivial
factorisation. Each profile ran the following number of cases **per family**:

| Profile | Variables | Measured | Warmups | Building-block degree | Terms | Coefficient bound |
|---|---:|---:|---:|---|---|---:|
| Small | 2 | 10 | 2 | 1–3 | 2–4 | 100 |
| Medium | 3 | 10 | 2 | 2–4 | 4–8 | 16384 |
| Larger | 3 | 5 | 1 | 4–8 | 8–16 | 16384 |

Backend batches used a 120-second timeout. Inputs can be products of the generated
building blocks, so final input sizes can exceed the ranges shown above.

CSV operation times exclude parsing, serialisation, compilation, and certificate
verification. Certified operation time includes certificate construction;
verification is recorded separately. The ordinary factorisation API still
constructs some internal evidence. Factorisation certificates check recomposition;
polybench also compares products and factor counts with the reference backend.

This validates the integration on the stated cases; it is not an official
performance ranking or a test of the future published package.
