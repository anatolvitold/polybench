### Quick Start

Install [Pixi](https://pixi.sh/) and run from the polybench checkout on Linux x86-64:

```sh
./run.sh --polymojo --polymojocertified --keep-temp \
  --type nontrivial-gcd --nvars 2 --max-degree 3 --max-nterms 4
```

Package installation, compiler selection and driver setup are automatic; no shell activation or package-path configuration is required. See the [README](https://github.com/anatolvitold/polybench/blob/feat/poly-mojo/README.md#poly-mojo-setup) for timing details and development overrides.
