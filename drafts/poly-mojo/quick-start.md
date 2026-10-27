### Quick Start
From the polybench checkout on Linux x86-64, with Python 3.12 and Pixi installed:

```bash
python3.12 -m venv .venv
.venv/bin/python -m pip install .
pixi install --locked --manifest-path environments/polymojo/pixi.toml
eval "$(pixi shell-hook --manifest-path environments/polymojo/pixi.toml --shell bash)"
export POLY_MOJO_PATH="$CONDA_PREFIX/lib/mojo"

.venv/bin/python -m polybench --polymojo --type nontrivial-gcd \
  --nvars 2 --max-degree 3 --max-nterms 4 --nproblems 5 --nwarmups 1
.venv/bin/python -m polybench --polymojocertified --type nontrivial-factor \
  --nvars 2 --max-degree 3 --max-nterms 4 --nproblems 5 --nwarmups 1 --keep-temp
```
