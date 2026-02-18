---
name: scvi-tools-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill when the user asks for a runnable tutorial path, notebook selection by task, or maintenance/release handling for tutorial docs (`docs/tutorials/index.md`, `docs/developer/maintenance.md`).
- Route model parameterization and setup details to `scvi-tools-inputs-and-modeling`.
- Route API inventory and object contracts to `scvi-tools-api-and-scripting`.
- Route mathematical background interpretation to `scvi-tools-user-guide`.

### Triage questions
- Which analysis family fits: quick-start, scRNA, ATAC, cytometry, scBS, multimodal, spatial, use-cases, or R?
- Is the goal end-user execution or maintainer-side tutorial/docs upkeep?
- Does the user need transfer learning/reference mapping specifically? (`docs/user_guide/background/transfer_learning.md`)
- Are they pinned to an older package version and therefore older docs/tutorial revisions?
- Is the run environment local, Colab, or CI doc build?

### Canonical workflow
1. Start at tutorial index and map request to a tutorial family page (`docs/tutorials/index.md`, `docs/tutorials/index_quick_start.md`, `docs/tutorials/index_scrna.md`, `docs/tutorials/index_multimodal.md`, `docs/tutorials/index_spatial.md`, `docs/tutorials/index_atac.md`, `docs/tutorials/index_cytometry.md`, `docs/tutorials/index_scbs.md`, `docs/tutorials/index_r.md`, `docs/tutorials/index_use_cases.md`).
2. Pick the minimal notebook card matching task tags and modality.
3. Confirm version alignment before running (tutorials default to latest installable version; switch docs version for older flows) (`docs/tutorials/index.md`).
4. For transfer-learning questions, route through dedicated background page and linked tutorials (`docs/user_guide/background/transfer_learning.md`).
5. For maintainers, follow maintenance release/tutorial-submodule process before publishing docs (`docs/developer/maintenance.md`).
6. Validate by reproducing notebook outputs and checking for API deprecation drift.

### Minimal working example
```bash
# Build docs (including tutorial references) after tutorial or API updates.
python -m sphinx -b html docs docs/_build
```
Doc anchor: `docs/developer/maintenance.md`

### Pitfalls and fixes
- Tutorials are version-sensitive; mismatch between installed package and docs version causes unexpected API breakage (`docs/tutorials/index.md`).
- Tutorial notebooks are a submodule and are not automatically synchronized without running the update workflow (`docs/developer/maintenance.md`).
- Release tags on PyPI cannot be republished; fix mistakes by bumping version rather than repushing (`docs/developer/maintenance.md`).
- Transfer-learning flows require compatible reference/query assumptions; route to scArches transfer references, not generic tutorials (`docs/user_guide/background/transfer_learning.md`).
- Some model pages are under construction; use linked notebooks as executable ground truth (`docs/user_guide/models/scbasset.md`, `docs/user_guide/models/contrastivevi.md`).

### Convergence and validation checks
- Notebook runs finish without unresolved deprecation/import errors.
- Expected artifacts are created (latent embeddings, model files, notebook figures).
- Re-running key cells produces stable qualitative results.
- Docs build passes after tutorial or API-reference edits.

### Source-code entry links
- `src/scvi/model/_scvi.py`: baseline scRNA tutorial model setup and training entry.
- `src/scvi/model/_scanvi.py`: label-transfer tutorial path via `from_scvi_model`.
- `src/scvi/model/_totalvi.py`: CITE-seq tutorial methods for normalized expression and DE.
- `src/scvi/model/_multivi.py`: multimodal tutorial methods for RNA/ATAC use-cases.
- `src/scvi/external/tangram/_model.py`: spatial tutorial training and projection methods.
- `src/scvi/external/scbasset/_model.py`: ATAC tutorial training and TF activity methods.
- `src/scvi/external/contrastivevi/_model.py`: contrastive tutorial train/inference methods.
- `src/scvi/external/velovi/_model.py`: velocity tutorial methods (`get_velocity`, latent time).

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/tutorials/index.md`
- `docs/developer/maintenance.md`
- `docs/user_guide/background/transfer_learning.md`
- `docs/tutorials/index_cytometry.md`
- `docs/tutorials/index_scbs.md`

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
- `src/scvi/model/_scvi.py`
- `src/scvi/model/_scanvi.py`
- `src/scvi/model/_totalvi.py`
- `src/scvi/model/_multivi.py`
- `src/scvi/external/tangram/_model.py`
- `src/scvi/external/scbasset/_model.py`
- `src/scvi/external/contrastivevi/_model.py`
- `src/scvi/external/velovi/_model.py`
- `src/scvi/external/cytovi/_model.py`
- `src/scvi/external/methylvi/_methylvi_model.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
