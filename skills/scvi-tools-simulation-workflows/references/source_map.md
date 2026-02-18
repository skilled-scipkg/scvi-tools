# scvi-tools source map: Simulation Workflows

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `workflow`
- `run`
- `train`
- `ddp`
- `checkpoint`
- `split`
- `datamodule`
- `resume`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/train src/scvi/model src/scvi/data src/scvi/dataloaders`

## Suggested source entry points
- `src/scvi/train/_trainrunner.py` | fit lifecycle, error handling, and history updates.
- `src/scvi/train/_trainer.py` | trainer runtime settings (`accelerator`, `devices`, strategy).
- `src/scvi/train/_callbacks.py` | checkpoint/early-stopping callbacks used in run control.
- `src/scvi/model/base/_training_mixin.py` | default model training orchestration path.
- `src/scvi/model/base/_save_load.py` | load/restart behavior for checkpointed runs.
- `src/scvi/data/_manager.py` | registered data access for training pipelines.
- `src/scvi/data/fields/_base_field.py` | base field contract behind `setup_anndata` validation.
- `src/scvi/dataloaders/_data_splitting.py` | train/val/test split logic for default workflows.
- `src/scvi/external/contrastivevi/_contrastive_data_splitting.py` | contrastive target/background split logic.
- `src/scvi/dataloaders/_custom_dataloaders.py` | scalable custom datamodule execution path.
- `src/scvi/train/_progress.py` | training progress/reporting path for runtime diagnostics.
