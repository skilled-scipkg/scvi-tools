# scvi-tools source map: Advanced Topics

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `analysis`
- `output`
- `plot`
- `trajectory`
- `developer`
- `maintenance`
- `changelog`
- `references`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/train src/scvi/model src/scvi/external`

## Suggested source entry points
- `src/scvi/train/_callbacks.py` | checkpointing and early-stopping behavior (`SaveCheckpoint`, `LoudEarlyStopping`).
- `src/scvi/train/_config.py` | typed training configuration objects (`TrainingPlanConfig`, `TrainerConfig`).
- `src/scvi/model/base/_training_mixin.py` | shared `train()` orchestration used by user-facing models.
- `src/scvi/model/base/_save_load.py` | model serialization/loading behavior for reproducibility checks.
- `src/scvi/data/_preprocessing.py` | preprocessing transforms often discussed in output-quality issues.
- `src/scvi/external/cytovi/_plotting.py` | plotting utilities for cytometry workflows.
- `src/scvi/external/decipher/utils/_trajectory.py` | trajectory helper functions for advanced analyses.
