> Draft on hold: replace source-checkout setup with an exact community-channel
> release pin and validate that published package before submission.

Add optional Poly Mojo backends for multivariate polynomial GCD and factorisation
over the integers, using polybench's existing problem generation and result checks.

- `--polymojo` measures the ordinary public API.
- `--polymojocertified` includes certificate construction in the operation time
  and checks every certificate before accepting a result. Verification is timed
  separately and retained in `certificate-timings.json` with `--keep-temp`.

The adapter accepts precompiled packages through `POLY_MOJO_PATH` and uses an
activated Mojo installation. It does not download dependencies or rebuild the
library. Both modes share a cached driver per variable count; the cache accounts
for the compiler, platform, runtime location, driver source and package hashes.
Input parsing, output serialisation and compilation are outside the operation
timers. The executable runs directly, so polybench's timeout applies to the solver.

The README includes a reproducible setup using Mojo 1.2.0 and Poly Mojo revision
`72c92234ba9f0b85a7d8d4476ccb61cb6573716e`. Existing CI build jobs explicitly skip
these optional native backends where Mojo is not installed. Python tests exercise
the interchange format, factor units and multiplicities, timing separation,
cache invalidation, and failure handling without requiring Mojo.

The ordinary factorisation API still constructs some internal evidence; this is
documented so its timing is not interpreted as an entirely proof-free algorithm.
Factorisation certificates check recomposition, while polybench's existing
checks also compare products and factor counts with other backends.

Validation:

- All 61 Python tests and all configured pre-commit checks passed.
- Built and installed the wheel, including the Mojo driver resource.
- The installed wheel passed 100 measured cases and 20 warmups against FLINT
  3.3.1: trivial/nontrivial GCD and factorisation, two and three variables,
  seed 42, including every certificate check. Generated inputs matched the
  previous independent pilot byte for byte.
- Zero library rebuilds during that run; two shared driver builds and 22 cache
  reuses. Validation used Python 3.12.14 and Mojo 1.2.0 on Linux x86-64.
