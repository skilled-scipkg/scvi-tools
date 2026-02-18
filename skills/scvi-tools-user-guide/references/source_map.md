# scvi-tools source map: User Guide

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `variational`
- `elbo`
- `counterfactual`
- `differential-expression`
- `callbacks`
- `training`
- `criticism`
- `use-case`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/model src/scvi/train src/scvi/criticism`

## Suggested source entry points
- `src/scvi/model/base/_differential.py` | differential and transform-batch internals.
- `src/scvi/model/base/_de_core.py` | core DE computations used by multiple models.
- `src/scvi/model/_totalvi.py` | user-facing normalized-expression and DE methods.
- `src/scvi/model/_scvi.py` | baseline model setup path used throughout user-guide workflows.
- `src/scvi/model/base/_training_mixin.py` | training behavior shared across model classes.
- `src/scvi/train/_callbacks.py` | callback logic (`SaveCheckpoint`, `LoudEarlyStopping`).
- `src/scvi/train/_config.py` | typed training configuration interfaces.
- `src/scvi/model/base/_save_load.py` | save/load behavior for reproducibility guidance.
- `src/scvi/criticism/_ppc.py` | posterior predictive checks used in criticism use-cases.
- `src/scvi/criticism/_create_criticism_report.py` | report generation and metric aggregation.
