---
name: scvi-tools-simulation-workflows
description: This skill should be used when users ask about simulation workflows in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for end-to-end run sequencing: tutorial track selection, execution mode (script vs notebook), training/restart flow, and runtime controls (`docs/tutorials/index_quick_start.md`, `docs/tutorials/index_r.md`).
- Route model-family selection and deep data registration choices to `scvi-tools-inputs-and-modeling`.
- Route API inventory questions to `scvi-tools-api-and-scripting`.
- Route conceptual interpretation (VI and counterfactual assumptions) to `scvi-tools-user-guide`.

### Triage questions
- Are you running in Python notebooks, Python scripts, or R/reticulate workflows?
- Which track fits best: quick-start, spatial, ATAC, or R? (`docs/tutorials/index_quick_start.md`, `docs/tutorials/index_spatial.md`, `docs/tutorials/index_atac.md`, `docs/tutorials/index_r.md`)
- Is compute single-device or multi-GPU DDP?
- Do you need custom dataloaders for large or disk-backed data?
- Are you starting from scratch training or loading/reusing an existing checkpoint?
- What output is required first: latent embedding, DE, normalized expression, or mapping?

### Canonical workflow
1. Choose the tutorial family index matching modality/runtime (`docs/tutorials/index_quick_start.md`, `docs/tutorials/index_spatial.md`, `docs/tutorials/index_atac.md`, `docs/tutorials/index_r.md`).
2. Begin with quick-start cards to align on data-loading and API-overview conventions before specialized notebooks.
3. Register data and start training with model defaults, then add structured config/callbacks if needed (`docs/user_guide/use_case/training_configuration.md`, `docs/user_guide/use_case/using_callbacks.md`).
4. If scaling is required, switch to DDP strategy or custom datamodule path (`docs/user_guide/use_case/multi_gpu_training.md`, `docs/user_guide/use_case/custom_dataloaders.md`).
5. Save model state and key outputs after a stable run (`docs/user_guide/use_case/saving_and_loading_models.md`).
6. Validate workflow outputs with downstream analyses and expected notebook artifacts.
7. Escalate to `TrainRunner` and data-field internals only when runtime behavior differs from docs.

### Minimal working example
```python
# Multi-GPU script mode (non-interactive).
model.train(
    max_epochs=100,
    accelerator="gpu",
    devices=-1,
    strategy="ddp_find_unused_parameters_true",
    early_stopping=False,
)
```
Doc anchors: `docs/user_guide/use_case/multi_gpu_training.md`

### Pitfalls and fixes
- DDP support is CUDA/NVIDIA-focused; do not assume equivalent behavior on unsupported accelerators (`docs/user_guide/use_case/multi_gpu_training.md`).
- In interactive sessions, multi-GPU caveats can block multi-stage chained training in one notebook session (`docs/user_guide/use_case/multi_gpu_training.md`).
- Early stopping should be disabled for current DDP path to avoid validation-loop issues (`docs/user_guide/use_case/multi_gpu_training.md`).
- Skipping quick-start data registration often causes downstream method failures; align with quick-start ordering first (`docs/tutorials/index_quick_start.md`).
- Custom dataloader workflows need optional dependencies and are experimental (`docs/user_guide/use_case/custom_dataloaders.md`).
- If training fails mid-run, use checkpoint callback recovery rather than discarding the run (`docs/user_guide/use_case/using_callbacks.md`, `docs/faq.md`).

### Convergence and validation checks
- Track monitored validation metrics and ensure monotonic trend in the chosen direction.
- Verify train/val/test split assumptions before enabling validation-driven callbacks.
- Re-load saved checkpoints and verify reproducibility of key outputs.
- Check that downstream DE/normalization output is stable across reruns with same seed/settings.
- For DDP runs, confirm performance gain is material for dataset scale (small data can lose to overhead).

### Source-code entry links
- `src/scvi/train/_trainrunner.py`: core fit lifecycle, callback interaction, and error handling.
- `src/scvi/model/base/_training_mixin.py`: default training orchestration, splitter, and runner wiring.
- `src/scvi/data/fields/_base_field.py`: abstract registration field contract used by setup flows.
- `src/scvi/data/fields/_layer_field.py`: count-layer field registration behavior.
- `src/scvi/data/fields/_scanvi.py`: semisupervised label field wiring for SCANVI-like workflows.
- `src/scvi/external/contrastivevi/_contrastive_data_splitting.py`: specialized train/val/test splitting for contrastive runs.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/tutorials/index_r.md`
- `docs/tutorials/index_spatial.md`
- `docs/tutorials/index_atac.md`
- `docs/tutorials/index_quick_start.md`

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
- `src/scvi/train/_trainrunner.py`
- `src/scvi/train/_trainer.py`
- `src/scvi/train/_callbacks.py`
- `src/scvi/model/base/_training_mixin.py`
- `src/scvi/model/base/_save_load.py`
- `src/scvi/data/_manager.py`
- `src/scvi/data/fields/_base_field.py`
- `src/scvi/dataloaders/_data_splitting.py`
- `src/scvi/external/contrastivevi/_contrastive_data_splitting.py`
- `src/scvi/dataloaders/_custom_dataloaders.py`
- `src/scvi/train/_progress.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
