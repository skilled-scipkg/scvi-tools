---
name: scvi-tools-tests
description: This skill should be used when users ask about tests in scvi-tools; it prioritizes test assets/docs first and then source inspection for unresolved behavior.
---

# scvi-tools: Tests

## High-signal playbook
### Commands
```bash
# run focused tests first
pytest -q tests -k "data or dataloader"

# run a single test file when narrowing failures
pytest -q tests/test_data.py
```

### Inputs to confirm before running
- Python environment has test extras installed (`pip install -e ".[dev]"`).
- Required test data files exist under `tests/test_data`.
- Optional markers (`jax`, `mlflow`, `multigpu`) are only enabled when dependencies exist.

### Validation checkpoints
- Failing tests map to a concrete source path in `references/source_map.md`.
- Data-shape/type assertions pass for both control and stimulated matrices.
- Re-runs are deterministic for the same seed/split configuration.

## Primary documentation references
- `tests/test_data/immune_stimulated_expression_matrix.txt`
- `tests/test_data/immune_control_expression_matrix.txt`
- `tests/test_data/HEMATO/bBM.filtered_gene_list.paper.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs/tests, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/scvi/data/_read.py`
- `src/scvi/data/_preprocessing.py`
- `src/scvi/data/_manager.py`
- `src/scvi/data/_datasets.py`
- `src/scvi/data/_anntorchdataset.py`
- `src/scvi/data/fields/_layer_field.py`
- `src/scvi/data/fields/_uns_field.py`
- `src/scvi/dataloaders/_data_splitting.py`
- `src/scvi/model/base/_differential.py`
- `src/scvi/external/scviva/differential_expression/_niche_de_core.py`
- `src/scvi/external/scviva/differential_expression/_results_dataclass.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src tests`).
