---
name: scvi-tools-api-and-scripting
description: This skill should be used when users ask about api and scripting in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: API and Scripting

## High-Signal Playbook
### Route conditions
- Use this skill for import paths, class/function discovery, built-in dataset loaders, and programmatic training configuration (`docs/api/index.md`, `docs/api/user.md`, `docs/api/datasets.md`).
- Route modeling strategy and modality-specific decisions to `scvi-tools-inputs-and-modeling`.
- Route workflow execution sequencing to `scvi-tools-simulation-workflows`.
- Route deeper theory interpretation to `scvi-tools-user-guide`.

### Triage questions
- Do you need user-facing model API, developer extension API, or both? (`docs/api/user.md`, `docs/api/developer.md`)
- Are you scripting with built-in datasets or custom AnnData inputs?
- Do you need structured train configs (`TrainingPlanConfig`/`TrainerConfig`) or ad-hoc kwargs?
- Are optional dependencies needed (`jax`, `dataloaders`, `autotune`, etc.)? (`docs/installation.md`)
- Is the goal model training, downstream inference methods, or persistence/loadability?

### Canonical workflow
1. Start from `docs/api/index.md` and choose `user` vs `developer` API surface.
2. Load data using `scvi.data` loaders or AnnData readers (`docs/api/datasets.md`, `docs/api/user.md`).
3. Register fields with model-specific `setup_anndata` before model construction (`docs/api/user.md`).
4. Configure training with config objects or kwargs (`docs/user_guide/use_case/training_configuration.md`).
5. Train, run inference methods, and save model artifact (`docs/user_guide/use_case/saving_and_loading_models.md`).
6. If API behavior differs from docs, inspect the exported modules and implementation entry points.

### Minimal working example
```python
import scvi
from scvi.train import TrainingPlanConfig, TrainerConfig

adata = scvi.data.pbmc_dataset()
scvi.model.SCVI.setup_anndata(adata, batch_key="batch")
model = scvi.model.SCVI(adata)

model.train(
    max_epochs=50,
    plan_config=TrainingPlanConfig(lr=1e-3),
    trainer_config=TrainerConfig(early_stopping=True, early_stopping_patience=10),
)

model.save("my_model.pt")
reloaded = scvi.model.SCVI.load("my_model.pt")
```
Doc anchors: `docs/api/datasets.md`, `docs/api/user.md`, `docs/user_guide/use_case/training_configuration.md`, `docs/user_guide/use_case/saving_and_loading_models.md`

### Pitfalls and fixes
- Calling model APIs before `setup_anndata` leads to registry/data-manager errors; register first (`docs/api/user.md`).
- Missing optional extras causes deferred import failures for optional features; install matching extras (`docs/installation.md`).
- Confusing user API with developer API can lead to unstable extension choices; confirm intended abstraction layer (`docs/api/user.md`, `docs/api/developer.md`).
- Built-in dataset helpers are for benchmarking/onboarding, not a substitute for proper production input checks (`docs/api/datasets.md`).
- Counterfactual decoding through `transform_batch` is statistical, not causal inference (`docs/user_guide/background/counterfactual_prediction.md`).

### Convergence and validation checks
- Verify training monitor trends and callback behavior match configured monitor/mode.
- Ensure `save`/`load` round-trips preserve expected inference outputs.
- Confirm API-selected model class matches modality/task assumptions from user guide.
- Check that requested optional capabilities are actually installed before runtime.

### Source-code entry links
- `src/scvi/data/_datasets.py`: built-in data loader implementations and defaults.
- `src/scvi/data/_manager.py`: `AnnDataManager` registration and validation flow.
- `src/scvi/model/_scvi.py`: canonical model setup entry (`setup_anndata`) for API-driven runs.
- `src/scvi/model/base/_save_load.py`: save/load mechanics used by all high-level models.
- `src/scvi/model/base/_training_mixin.py`: shared `train()` behavior used across model classes.
- `src/scvi/train/_config.py`: structured config classes used by `model.train`.
- `src/scvi/train/_trainer.py`: trainer runtime options and defaults.
- `src/scvi/train/_trainrunner.py`: full fit execution lifecycle and history updates.
- `src/scvi/utils/_dependencies.py`: optional dependency guards surfaced in scripted usage.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/api/index.md`
- `docs/api/datasets.md`
- `docs/_templates/class_no_inherited.rst`
- `docs/_templates/autosummary/class.rst`

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
- `src/scvi/data/_datasets.py`
- `src/scvi/data/_manager.py`
- `src/scvi/model/_scvi.py`
- `src/scvi/model/base/_base_model.py`
- `src/scvi/model/base/_training_mixin.py`
- `src/scvi/model/base/_save_load.py`
- `src/scvi/train/_config.py`
- `src/scvi/train/_trainer.py`
- `src/scvi/train/_trainrunner.py`
- `src/scvi/utils/_dependencies.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
