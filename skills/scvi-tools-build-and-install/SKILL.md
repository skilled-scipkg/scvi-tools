---
name: scvi-tools-build-and-install
description: This skill should be used when users ask about build and install in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: Build and Install

## Simulation-ready playbook
### Commands
```bash
# from repo root
python -m venv .venv
source .venv/bin/activate
pip install -U pip
pip install -e ".[dev]"
```

### Minimal startup check
```bash
python - <<'PY'
import scvi
adata = scvi.data.synthetic_iid(n_batches=2)
scvi.model.SCVI.setup_anndata(adata, batch_key="batch")
model = scvi.model.SCVI(adata)
model.train(max_epochs=1)
print("ok", adata.n_obs, adata.n_vars)
PY
```

### Validation checkpoints
- Import succeeds without optional-dependency errors.
- One-epoch training completes and prints `ok`.
- If GPU is expected, verify accelerator/device selection explicitly in training kwargs.

## Primary documentation references
- `docs/installation.md`
- `docs/developer/code.md`
- `docs/user_guide/use_case/hyper_parameters_tuning.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/scvi/utils/_dependencies.py`
- `src/scvi/utils/_jax.py`
- `src/scvi/model/__init__.py`
- `src/scvi/train/__init__.py`
- `src/scvi/train/_trainer.py`
- `src/scvi/train/_trainrunner.py`
- `src/scvi/data/_download.py`
- `src/scvi/data/_datasets.py`
- `src/scvi/_settings.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
