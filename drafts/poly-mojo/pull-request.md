Add optional Poly Mojo backends for multivariate polynomial GCD and factorisation over the integers, using polybench's existing problem generation and result checks.

- `--polymojo` measures the ordinary public API.
- `--polymojocertified` includes certificate construction in operation time and checks every certificate before accepting a result. Verification is timed separately in `certificate-timings.json` with `--keep-temp`.

On Linux x86-64, the adapter uses Pixi to install the locked, precompiled **Poly Mojo 1.0.1**, **APN Mojo 1.0.2**, and matching **Mojo 1.2.0** compiler automatically. The driver, manifest, lockfile and CI result checker are together under `polybench/solvers/polymojo/`, following the existing backend layout. Both modes share one build environment and a cached driver per variable count. A `POLY_MOJO_PATH` override remains available for development with an existing package build.

Installation, compilation, parsing, output serialization and certificate verification are outside operation timers. The native executable runs directly under polybench's solver timeout. The adapter does not rebuild the library. Ordinary factorisation still constructs some internal evidence; it is not claimed to be entirely proof-free. Factorisation certificates check recomposition, while polybench also compares products and factor counts with other backends.

### CI

The Python 3.7–3.13 `testrun` jobs install Pixi and exercise both modes. The four `bench` jobs exercise ordinary Poly Mojo. Setup failures are fatal, and a result checker rejects missing backend columns, incomplete case counts, invalid timings and reported comparison failures. Host-specific drivers are reused within each job but excluded from the cache shared across runners. The legacy Python 3.6 container continues to skip Mojo.

### Quick Start

Install [Pixi](https://pixi.sh/) and run from the polybench checkout on Linux x86-64:

```sh
./run.sh --polymojo --polymojocertified --keep-temp \
  --type nontrivial-gcd --nvars 2 --max-degree 3 --max-nterms 4
```

Package installation, compiler selection and driver setup are automatic; no shell activation or package-path configuration is required. See the [README](https://github.com/anatolvitold/polybench/blob/feat/poly-mojo/README.md#poly-mojo-setup) for timing details and development overrides.

### Validation

- 74 Python tests and all applicable pre-commit checks passed, including mypy and workflow linting.
- Built and installed the wheel in a separate Python environment, then tested automatic package setup with no package/compiler overrides and a build path containing spaces.
- Both modes passed 20 small measured cases plus all 200 measured cases using the upstream `testrun` parameters against FLINT 3.3.1. Every certificate check passed.
- Ordinary Poly Mojo passed all 200 measured cases using the upstream `bench` parameters against FLINT 3.3.1.
- The two variable counts needed two driver builds, shared across modes and reused by later batches; no library rebuilds. Installed module hashes match the published packages.
- `scripts/poetry2pip.py` returns `SpecifierSet.contains()` directly. Removing the obsolete type-ignore is sufficient for mypy; the redundant `bool()` conversion was removed in a separate commit.

The [validation record](https://github.com/anatolvitold/polybench/blob/drafts/drafts/poly-mojo/validation.md) records package builds and check parameters. These local checks validate the integration; they are not an official performance ranking. No problem-generator or reference-algorithm changes are included.
