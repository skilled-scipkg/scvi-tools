---
name: scvi-tools-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use this skill for model selection, AnnData registration decisions, covariates, training knobs, and downstream modeling outputs (`docs/user_guide/models/index.md`, `docs/api/user.md`).
- Route pure workflow execution sequencing to `scvi-tools-simulation-workflows`.
- Route API surface questions (module/class availability, import paths) to `scvi-tools-api-and-scripting`.
- Route mathematical interpretation (ELBO, counterfactual assumptions) to `scvi-tools-user-guide`.

### Triage questions
- What modality is in scope: scRNA, ATAC, CITE-seq, spatial, multimodal, or methylation?
- Which user-facing model class is intended (`SCVI`, `SCANVI`, `TOTALVI`, external models, etc.)?
- Are raw counts available in `.X` or a dedicated count layer? (`docs/api/user.md`, `docs/faq.md`)
- What nuisance factors are present, and are they best represented as `batch_key` or `categorical_covariate_keys`? (`docs/faq.md`)
- Is scaling limited by memory, requiring custom dataloaders or multi-GPU training?
- Is the goal integration, DE, normalization, label transfer, or hyperparameter search?

### Canonical workflow
1. Pick model family and modality from model index and tutorial family pages (`docs/user_guide/models/index.md`, `docs/tutorials/index_scrna.md`, `docs/tutorials/index_multimodal.md`, `docs/tutorials/index_use_cases.md`).
2. Confirm environment extras needed for workflow (`[cuda]`, `[autotune]`, `[dataloaders]`, `[mlflow]`) (`docs/installation.md`, `docs/user_guide/use_case/training_configuration.md`, `docs/user_guide/use_case/using_callbacks.md`, `docs/user_guide/use_case/custom_dataloaders.md`, `docs/user_guide/use_case/multi_gpu_training.md`, `docs/user_guide/use_case/hyper_parameters_tuning.md`).
3. Register data with the correct count layer and covariates using `setup_anndata` (`docs/api/user.md`, `docs/faq.md`).
4. Instantiate model and train with either simple kwargs or structured configs (`docs/user_guide/use_case/training_configuration.md`).
5. Add optional workflow controls (callbacks, checkpointing, custom datamodules, distributed strategy) (`docs/user_guide/use_case/using_callbacks.md`, `docs/user_guide/use_case/custom_dataloaders.md`, `docs/user_guide/use_case/multi_gpu_training.md`).
6. Run downstream methods (`differential_expression`, `get_normalized_expression`, latent extraction) and save model artifacts (`docs/user_guide/use_case/downstream_analysis_tasks.md`, `docs/user_guide/use_case/saving_and_loading_models.md`).
7. If behavior is unclear, inspect implementation files named in source links.

### Minimal working example
```python
import scvi
from scvi.train import TrainingPlanConfig, TrainerConfig

adata = scvi.data.pbmc_dataset()
scvi.model.SCVI.setup_anndata(adata, batch_key="batch")
model = scvi.model.SCVI(adata)

model.train(
    max_epochs=100,
    plan_config=TrainingPlanConfig(lr=1e-3, weight_decay=0.0, compile=False),
    trainer_config=TrainerConfig(early_stopping=True, early_stopping_patience=10),
)

de = model.differential_expression()
norm = model.get_normalized_expression(transform_batch=0)
model.save("scvi_model.pt")
```
Doc anchors: `docs/api/datasets.md`, `docs/user_guide/use_case/training_configuration.md`, `docs/user_guide/background/counterfactual_prediction.md`, `docs/user_guide/use_case/saving_and_loading_models.md`

### Pitfalls and fixes
- Passing normalized/transformed data to models expecting raw counts causes unstable training; set the correct count layer in `setup_anndata` (`docs/api/user.md`, `docs/faq.md`).
- Misusing `categorical_covariate_keys` when `batch_key` should encode the main technical effect reduces feature support (`docs/faq.md`).
- NaN training failures: reduce learning rate, adjust batch size, verify data quality, and enable checkpoint recovery (`docs/faq.md`, `docs/user_guide/use_case/using_callbacks.md`).
- Multi-GPU DDP currently has caveats: interactive sessions are limited and early stopping should be disabled (`docs/user_guide/use_case/multi_gpu_training.md`).
- Custom dataloaders are experimental and currently centered on SCVI/SCANVI workflows (`docs/user_guide/use_case/custom_dataloaders.md`).
- TileDB workflows require non-integer categorical covariates, even if values look string-like in AnnData (`docs/user_guide/use_case/custom_dataloaders.md`).
- Treat scib-metrics autotune targets as objective-specific; choose `mode`/metric pair intentionally (`docs/user_guide/use_case/hyper_parameters_tuning.md`).

### Convergence and validation checks
- Track ELBO-related validation metrics and ensure they move in the intended direction for the chosen monitor (`docs/user_guide/use_case/using_callbacks.md`).
- Validate that latent spaces preserve biology while reducing technical batch structure (e.g., with scib-metrics where relevant) (`docs/user_guide/use_case/hyper_parameters_tuning.md`).
- Cross-check DE and normalized expression outputs against expected group structure before interpretation (`docs/user_guide/use_case/downstream_analysis_tasks.md`).
- Confirm checkpoint reloadability and reproducible outputs after `save`/`load` (`docs/user_guide/use_case/saving_and_loading_models.md`).
- For counterfactual decoding via `transform_batch`, ensure queries stay close to observed support (`docs/user_guide/background/counterfactual_prediction.md`).

### Source-code entry links
- `src/scvi/model/_scvi.py`: base SCVI API setup entry point.
- `src/scvi/model/_scanvi.py`: SCANVI transfer workflow and setup registration.
- `src/scvi/model/_totalvi.py`: multimodal normalization and DE methods.
- `src/scvi/model/_autozi.py`: alternative RNA model setup and parameters.
- `src/scvi/model/base/_training_mixin.py`: shared `train()` orchestration across models.
- `src/scvi/model/base/_differential.py`: differential computation internals and transform-batch handling.
- `src/scvi/dataloaders/_custom_dataloaders.py`: `MappedCollectionDataModule` and `TileDBDataModule` implementation.
- `src/scvi/train/_config.py`: typed `TrainingPlanConfig` / `TrainerConfig` schema.
- `src/scvi/external/totalanvi/_model.py`: semisupervised CITE-seq external workflow.
- `src/scvi/external/sysvi/_model.py`: cycle-consistency integration caveats and overrides.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/index.md`
- `docs/user_guide/models/index.md`
- `docs/tutorials/index_scrna.md`
- `docs/api/user.md`
- `docs/api/developer.md`
- `docs/tutorials/index_use_cases.md`
- `docs/tutorials/index_multimodal.md`
- `docs/user_guide/use_case/multi_gpu_training.md`
- `docs/user_guide/models/totalanvi.md`
- `docs/user_guide/models/sysvi.md`
- `docs/user_guide/use_case/custom_dataloaders.md`
- `docs/user_guide/models/scar.md`

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
- `src/scvi/data/_manager.py`
- `src/scvi/data/fields/_layer_field.py`
- `src/scvi/model/_scvi.py`
- `src/scvi/model/_scanvi.py`
- `src/scvi/model/_totalvi.py`
- `src/scvi/model/_multivi.py`
- `src/scvi/model/base/_training_mixin.py`
- `src/scvi/model/base/_differential.py`
- `src/scvi/dataloaders/_custom_dataloaders.py`
- `src/scvi/train/_config.py`
- `src/scvi/train/_callbacks.py`
- `src/scvi/external/totalanvi/_model.py`
- `src/scvi/external/sysvi/_model.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
