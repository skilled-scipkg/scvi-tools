# scvi-tools source map: Getting Started

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `getting-started`
- `quickstart`
- `solo`
- `tangram`
- `scbasset`
- `contrastivevi`
- `setup`
- `train`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/model src/scvi/external`

## Suggested source entry points
- `src/scvi/data/_datasets.py` | starter datasets (`pbmc_dataset`) for first-run scripts.
- `src/scvi/model/_scvi.py` | core model setup (`setup_anndata`) and constructor behavior.
- `src/scvi/external/solo/_model.py` | SOLO bootstrapping via `from_scvi_model` and scoring.
- `src/scvi/external/tangram/_model.py` | Tangram spatial mapping training and projection methods.
- `src/scvi/external/scbasset/_model.py` | SCBASSET training and latent/TF activity methods.
- `src/scvi/external/contrastivevi/_model.py` | contrastive train/inference path.
- `src/scvi/external/contrastivevi/_contrastive_data_splitting.py` | target/background split semantics.
- `src/scvi/model/base/_training_mixin.py` | shared `train()` behavior used by beginner workflows.
- `src/scvi/model/base/_save_load.py` | checkpoint/model reload behavior for workflow continuation.
