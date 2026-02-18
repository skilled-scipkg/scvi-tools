---
name: scvi-tools-user-guide
description: This skill should be used when users ask about user guide in scvi-tools; it prioritizes documentation references and then source inspection only for unresolved details.
---

# scvi-tools: User Guide

## High-Signal Playbook
### Route conditions
- Use this skill for conceptual interpretation and theory-backed usage questions: variational inference, counterfactual prediction framing, and cross-cutting use-case navigation (`docs/user_guide/background/index.md`, `docs/user_guide/background/variational_inference.md`, `docs/user_guide/background/counterfactual_prediction.md`, `docs/user_guide/background/differential_expression.md`, `docs/user_guide/use_case/index.md`).
- Route model-specific setup/training knobs to `scvi-tools-inputs-and-modeling`.
- Route API symbol-level questions to `scvi-tools-api-and-scripting`.
- Route notebook execution path selection to `scvi-tools-examples-and-tutorials`.

### Triage questions
- Is the user asking for theory interpretation, practical code path, or both?
- Is the question about ELBO/VI terms, convergence, or only API outputs?
- Is the user asking for counterfactual prediction and does the query look in-distribution?
- Which use-case lane applies: callbacks, multi-GPU, tuning, saving/loading, or downstream analysis?
- Does the response require explicit caveats about statistical vs causal interpretation?

### Canonical workflow
1. Start at user-guide background index and choose the minimum conceptual page needed (`docs/user_guide/background/index.md`).
2. For optimization/convergence interpretation, anchor on VI decomposition and ELBO framing (`docs/user_guide/background/variational_inference.md`).
3. For perturbation/counterfactual questions, apply in-distribution vs out-of-distribution caution before giving procedural advice (`docs/user_guide/background/counterfactual_prediction.md`).
4. Map concept to concrete use-case docs (callbacks, training config, tuning, save/load, downstream tasks) (`docs/user_guide/use_case/index.md`).
5. Tie conceptual answer back to explicit API methods (`get_normalized_expression`, `differential_expression`, callbacks/config objects).
6. Escalate to source for behavior ambiguities or implementation-level edge cases.

### Minimal working example
```python
import scvi

adata = scvi.data.pbmc_dataset()
scvi.model.SCVI.setup_anndata(adata, batch_key="batch")
model = scvi.model.SCVI(adata)
model.train(max_epochs=20)

# Counterfactual-style query via batch transform.
expr_cf = model.get_normalized_expression(transform_batch=0)
```
Doc anchors: `docs/user_guide/background/counterfactual_prediction.md`, `docs/api/user.md`

### Pitfalls and fixes
- Counterfactual predictions here are statistical probes, not causal claims; state this explicitly (`docs/user_guide/background/counterfactual_prediction.md`).
- OOD counterfactual queries are unreliable; prefer regions with nearby observed support (`docs/user_guide/background/counterfactual_prediction.md`).
- Misreading ELBO terms as independent objectives can produce bad tuning decisions; track reconstruction and KL jointly (`docs/user_guide/background/variational_inference.md`).
- `batch_key` vs `categorical_covariate_keys` confusion can invalidate interpretation of batch-corrected outputs (`docs/faq.md`).
- NaN failures should trigger data/layer sanity checks and callback-based recovery path, not blind retraining (`docs/faq.md`, `docs/user_guide/use_case/using_callbacks.md`).

### Convergence and validation checks
- Monitor ELBO-related metrics and ensure the selected optimization monitor matches the model/task.
- Verify counterfactual outputs are stable under small perturbations to query definitions.
- Compare in-distribution prediction quality before trusting extrapolative counterfactual conclusions.
- Validate DE/normalized-expression outputs against known biological or annotation structure.

### Source-code entry links
- `src/scvi/model/base/_differential.py`: differential analysis internals and batch-transform path.
- `src/scvi/model/_totalvi.py`: normalized expression and DE implementations with `transform_batch` support.
- `src/scvi/model/base/_training_mixin.py`: shared train behavior and callback/config integration.
- `src/scvi/train/_callbacks.py`: `LoudEarlyStopping` and `SaveCheckpoint` behavior.
- `src/scvi/train/_config.py`: typed training and trainer config schemas.

## Scope
- Handle questions about documentation grouped under the 'user-guide' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/user_guide/use_case/index.md`
- `docs/user_guide/background/index.md`
- `docs/user_guide/background/variational_inference.md`
- `docs/user_guide/background/counterfactual_prediction.md`

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
- `src/scvi/model/base/_differential.py`
- `src/scvi/model/base/_de_core.py`
- `src/scvi/model/_totalvi.py`
- `src/scvi/model/_scvi.py`
- `src/scvi/model/base/_training_mixin.py`
- `src/scvi/train/_callbacks.py`
- `src/scvi/train/_config.py`
- `src/scvi/model/base/_save_load.py`
- `src/scvi/criticism/_ppc.py`
- `src/scvi/criticism/_create_criticism_report.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
