# scvi-tools source map: Build and Install

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `install`
- `dependencies`
- `optional`
- `jax`
- `cuda`
- `trainer`
- `download`
- `environment`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/utils src/scvi/train src/scvi/data`

## Suggested source entry points
- `src/scvi/utils/_dependencies.py` | dependency checks (`error_on_missing_dependencies`, decorators).
- `src/scvi/utils/_jax.py` | JAX device-key helpers used in optional JAX flows.
- `src/scvi/model/__init__.py` | model export surface and optional import gating.
- `src/scvi/train/__init__.py` | training export surface and lazy optional components.
- `src/scvi/train/_trainer.py` | accelerator/device wiring and trainer defaults.
- `src/scvi/train/_trainrunner.py` | runtime exception/update path during training startup.
- `src/scvi/data/_download.py` | dataset/resource download and caching utilities.
- `src/scvi/data/_datasets.py` | user-facing dataset wrappers that trigger downloads.
- `src/scvi/_settings.py` | global runtime settings affecting startup behavior.
