Add optional Poly Mojo backends for multivariate polynomial GCD and factorisation over the integers, using polybench's existing problem generation and result checks.

- `--polymojo` measures the ordinary public API.
- `--polymojocertified` includes certificate construction in the operation time and checks every certificate before accepting a result. Verification is timed separately and retained in `certificate-timings.json` with `--keep-temp`.

The checked-in Pixi environment and lockfile install the published **Poly Mojo 1.0.1**, **APN Mojo 1.0.2**, and **Mojo 1.2.0** packages on Linux x86-64. The adapter uses those precompiled modules; it does not download dependencies or build the library. Both modes share a cached driver per variable count, keyed by compiler, runtime, platform, driver source, and package hashes. Compilation, parsing, output serialization, and certificate verification are outside operation timers. The native executable runs directly under polybench's solver timeout.

Python tests cover exact interchange, factor units and multiplicities, timing separation, cache invalidation, and failure handling without requiring Mojo. Existing CI build jobs explicitly skip these optional native backends where Mojo is not installed. The Mojo driver is included in the Python wheel.

Ordinary factorisation still constructs some internal evidence; it is not claimed to be entirely proof-free. Factorisation certificates check recomposition, while polybench also compares products and factor counts with other backends.

Validation against the published package:

- All 61 Python tests and configured pre-commit checks passed.
- Built and installed the wheel in a separate Python environment; the installed adapter and driver match the proposed sources.
- The installed wheel passed 100 measured cases and 20 warmups against FLINT 3.3.1 in ordinary and certified modes, covering trivial/nontrivial GCD and factorisation with two and three variables, seed 42. Every certificate check passed.
- No library rebuilds. Two shared drivers were compiled, with 22 subsequent cache reuses. Compiler paths and package hashes were checked against the clean channel installation.

The [validation record](https://github.com/anatolvitold/polybench/blob/drafts/drafts/poly-mojo/validation.md) records the package builds and case parameters. This selected upstream-generator comparison validates the adapter; it is not an official performance ranking. No changes to the problem generator or reference algorithms are included.
