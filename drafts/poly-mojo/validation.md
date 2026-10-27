# Validation against the published Poly Mojo package

Validated on October 27, 2026 (America/New_York). These checks use a fresh
community-channel package installation and a separately installed polybench
wheel, without a Poly Mojo source checkout or source-package overrides.

| Component | Version or build |
|---|---|
| Poly Mojo | 1.0.1, `hb0f4dca_0` |
| APN Mojo | 1.0.2, `hb0f4dca_0` |
| Mojo | 1.2.0 (`2016d0cd`), `release` |
| Polybench upstream base | `910864a14999f0861821ecd67747006843f3fc51` |
| Python running the installed wheel | 3.12.14 |
| Python in the locked Mojo environment | 3.12.16 |
| FLINT | 3.3.1, compiled with GCC 14.2.0 |
| Platform | Linux x86-64, Intel Xeon Platinum 8573C |

The code branch includes `environments/polymojo/pixi.toml` and `pixi.lock`.
[Package records](release-checks/installed-packages.json) preserve the channel
URLs, package archive hashes, and installed module hashes. The adapters' recorded
compiler paths and module hashes match that clean installation.

## Checks passed

- All 61 Python tests, which do not require Mojo.
- All configured pre-commit hooks, plus the commit-message check. The environment's
  `/usr/bin/go` was not the Go toolchain; lint tooling was run with a real Go
  installation supplied by Pixi. No hooks were skipped.
- Built the Python wheel and installed it with dependencies into a separate
  environment. The installed adapter and Mojo driver match the proposed sources
  byte for byte; all native checks ran from outside the source checkout.
- All 100 measured cases and 20 warmups passed against FLINT in ordinary and
  certified modes, including every certificate check.
- Generated problem records match the previous validation byte for byte.
- Zero library rebuilds. Two drivers were compiled, one per variable count,
  and reused 22 times across modes and batches. No case compiles a driver.

[Logs and structured evidence](release-checks/) are preserved in this review
branch. Terminal control sequences were removed from display logs; recorded
values are unchanged. Raw inputs and solver outputs remain in the local workspace.

## Independent benchmark inputs

The run used polybench's unchanged generator, FLINT adapter, and consistency
checks, with seed 42 and uniform exponents. It covers trivial/nontrivial GCD and
trivial/nontrivial factorisation. Each profile runs these counts **per family**:

| Profile | Variables | Measured | Warmups | Building-block degree | Terms | Coefficient bound |
|---|---:|---:|---:|---|---|---:|
| Small | 2 | 10 | 2 | 1–3 | 2–4 | 100 |
| Medium | 3 | 10 | 2 | 2–4 | 4–8 | 16384 |
| Larger | 3 | 5 | 1 | 4–8 | 8–16 | 16384 |

Each backend batch has a 120-second timeout. Inputs can be products of generated
building blocks, so final input sizes can exceed the table's ranges. Compilation
happens during setup, outside the batch timeout and operation timers.

CSV operation times exclude parsing, serialization, compilation, and certificate
verification. Certified computation includes certificate construction; verification
is recorded separately. Ordinary factorisation still constructs internal evidence.
Factorisation certificates check recomposition; polybench additionally compares
products and factor counts against FLINT. GCD results are compared up to sign.

This is adapter validation on the stated independently generated problems, not an
official performance ranking. Only Linux x86-64 was tested. The earlier Python 3.6
grammar check passed for the unchanged adapter; the full upstream Python-version
CI matrix has not been run locally.
