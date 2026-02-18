# scvi-tools source map: API and Scripting

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `api`
- `datasets`
- `setup_anndata`
- `train`
- `save`
- `load`
- `config`
- `manager`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/data src/scvi/model src/scvi/train`
- If docs mention a symbol, search that exact symbol first and inspect nearby implementations.

## Suggested source entry points
- `src/scvi/data/_datasets.py` | built-in dataset loader APIs (`pbmc_dataset`, `synthetic_iid`, etc.).
- `src/scvi/data/_manager.py` | `AnnDataManager` registration, transfer, and registry validation behavior.
- `src/scvi/model/_scvi.py` | canonical user model API entry (`setup_anndata`, constructor).
- `src/scvi/model/base/_base_model.py` | shared model lifecycle hooks and common API behavior.
- `src/scvi/model/base/_training_mixin.py` | shared `train()` logic for unsupervised/semisupervised models.
- `src/scvi/model/base/_save_load.py` | cross-model save/load implementation details.
- `src/scvi/train/_config.py` | config dataclasses and kwargs conversion (`to_kwargs`).
- `src/scvi/train/_trainer.py` | trainer initialization and runtime flags.
- `src/scvi/train/_trainrunner.py` | end-to-end fit execution path and history updates.
- `src/scvi/utils/_dependencies.py` | optional dependency guards and import-time errors.
