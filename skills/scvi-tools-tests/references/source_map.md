# scvi-tools source map: Tests

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `test-data`
- `matrix`
- `read`
- `preprocessing`
- `split`
- `registry`
- `differential-expression`
- `validation`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src tests`
- `rg -n "class|def" src/scvi/data src/scvi/dataloaders src/scvi/model/base`

## Suggested source entry points
- `src/scvi/data/_read.py` | data readers used by ingestion-oriented tests.
- `src/scvi/data/_preprocessing.py` | preprocessing utilities commonly validated in tests.
- `src/scvi/data/_manager.py` | setup registry and manager state checks.
- `src/scvi/data/_datasets.py` | built-in dataset creation/downloading for test fixtures.
- `src/scvi/data/_anntorchdataset.py` | tensor dataset conversion behavior.
- `src/scvi/data/fields/_layer_field.py` | layer field registration and schema checks.
- `src/scvi/data/fields/_uns_field.py` | unstructured metadata registration path.
- `src/scvi/dataloaders/_data_splitting.py` | deterministic split behavior for training tests.
- `src/scvi/model/base/_differential.py` | DE-related calculations used in behavior regression checks.
- `src/scvi/external/scviva/differential_expression/_niche_de_core.py` | external DE computation kernel.
- `src/scvi/external/scviva/differential_expression/_results_dataclass.py` | structured DE result contracts.
