---
name: scvi-tools-getting-started
description: This skill should be used when users ask about getting started in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill when the user needs a first model/task choice and a shortest path into scvi-tools model families (`docs/user_guide/models/solo.md`, `docs/user_guide/models/tangram.md`, `docs/user_guide/models/scbasset.md`, `docs/user_guide/models/contrastivevi.md`).
- Route installation or environment issues to `scvi-tools-build-and-install` (`docs/installation.md`).
- Route detailed training config, custom dataloaders, and multi-GPU setup to `scvi-tools-inputs-and-modeling` (`docs/user_guide/use_case/index.md`).
- Route theory-heavy questions (ELBO, counterfactual assumptions) to `scvi-tools-user-guide` (`docs/user_guide/background/index.md`).

### Triage questions
- Which modality/task is primary: doublet detection, spatial mapping, scATAC, or contrastive target-vs-background analysis?
- Do you already have a trained `SCVI` model (required for the SOLO workflow)? (`docs/user_guide/models/solo.md`)
- Do you have explicit target/background groups for contrastive analysis? (`docs/user_guide/models/contrastivevi.md`)
- Are you starting from tutorial notebooks or scripting from API docs? (`docs/tutorials/index.md`, `docs/api/index.md`)
- Is the request conceptual model selection or runnable code path?

### Canonical workflow
1. Map task to model family from the model overview docs (`docs/user_guide/models/solo.md`, `docs/user_guide/models/tangram.md`, `docs/user_guide/models/scbasset.md`, `docs/user_guide/models/contrastivevi.md`).
2. Open the matching tutorial index card for executable workflow context (`docs/tutorials/index_spatial.md`, `docs/tutorials/index_atac.md`, `docs/tutorials/index_scrna.md`).
3. Prepare AnnData and register inputs with `setup_anndata` for the chosen model class (`docs/api/user.md`).
4. Train the base model and run the task-specific entry point (for SOLO, initialize from pretrained SCVI; for contrastive workflows, separate target/background indices) (`docs/user_guide/models/solo.md`, `src/scvi/external/contrastivevi/_contrastive_data_splitting.py`).
5. Validate expected artifacts (doublet probabilities, mapped embeddings, or learned latent spaces) and then expand to full notebook workflows.
6. Escalate to source only when docs leave behavior ambiguity.

### Minimal working example
```python
import scvi

adata = scvi.data.pbmc_dataset()
scvi.model.SCVI.setup_anndata(adata, batch_key="batch")
base = scvi.model.SCVI(adata)
base.train(max_epochs=20)

# SOLO starts from a pretrained SCVI model.
solo = scvi.external.SOLO.from_scvi_model(base, doublet_ratio=2.0)
solo.train(max_epochs=20)
adata.obs["solo_score"] = solo.predict()
```
Doc anchors: `docs/api/datasets.md`, `docs/api/user.md`, `docs/user_guide/models/solo.md`

### Pitfalls and fixes
- SOLO is not a stand-alone first step; initialize from a trained SCVI model via `from_scvi_model`.
- `doublet_ratio` drives how many synthetic doublets are generated; unrealistic values can skew classifier behavior (`docs/user_guide/models/solo.md`).
- scBasset and contrastiveVI model pages are explicitly marked under construction; prefer linked notebooks for operational steps (`docs/user_guide/models/scbasset.md`, `docs/user_guide/models/contrastivevi.md`).
- scBasset currently does not cover transfer-learning workflows; do not route scArches-style requests there (`docs/user_guide/models/scbasset.md`).
- Tangram docs are intentionally concise; use the linked spatial tutorial path when users ask for full run instructions (`docs/user_guide/models/tangram.md`, `docs/tutorials/index_spatial.md`).

### Convergence and validation checks
- For SOLO, check that score distributions are sensible and not collapsed to a narrow range.
- For contrastive analysis, verify target/background group definitions before interpreting salient variation (`docs/user_guide/models/contrastivevi.md`).
- For Tangram, confirm mapping outputs are stable across reruns and consistent with expected spatial structure (`docs/user_guide/models/tangram.md`).
- Confirm training completed without NaN losses; if unstable, adjust data layer and training settings (`docs/faq.md`).

### Source-code entry links
- `src/scvi/external/solo/_model.py`: `SOLO.from_scvi_model`, SOLO `train`, and setup flow.
- `src/scvi/external/tangram/_model.py`: Tangram class train/setup methods.
- `src/scvi/external/scbasset/_model.py`: SCBASSET train/setup behavior.
- `src/scvi/external/contrastivevi/_model.py`: ContrastiveVI setup, train, normalized expression, DE hooks.
- `src/scvi/external/contrastivevi/_contrastive_dataloader.py`: paired background/target batch iterator behavior.
- `src/scvi/external/contrastivevi/_contrastive_data_splitting.py`: split semantics for target/background indices.

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user_guide/models/solo.md`
- `docs/user_guide/models/tangram.md`
- `docs/user_guide/models/scbasset.md`
- `docs/user_guide/models/contrastivevi.md`
- `docs/user_guide/background/codebase_overview.md`

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
- `src/scvi/model/_scvi.py`
- `src/scvi/external/tangram/_model.py`
- `src/scvi/external/solo/_model.py`
- `src/scvi/external/scbasset/_model.py`
- `src/scvi/external/contrastivevi/_model.py`
- `src/scvi/external/contrastivevi/_contrastive_data_splitting.py`
- `src/scvi/model/base/_training_mixin.py`
- `src/scvi/model/base/_save_load.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
