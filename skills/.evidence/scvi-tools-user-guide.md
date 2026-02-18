# Evidence: scvi-tools-user-guide

## Primary docs
- `docs/user_guide/use_case/index.md`
- `docs/user_guide/background/index.md`
- `docs/user_guide/background/variational_inference.md`
- `docs/user_guide/background/counterfactual_prediction.md`

## Primary source entry points
- `skills/scvi-tools-user-guide/references/doc_map.md`
- `src/scvi/__init__.py`
- `src/scvi/utils/__init__.py`
- `src/scvi/train/__init__.py`
- `src/scvi/nn/__init__.py`
- `src/scvi/module/__init__.py`
- `src/scvi/model/__init__.py`
- `src/scvi/hub/__init__.py`
- `src/scvi/external/__init__.py`
- `src/scvi/distributions/__init__.py`
- `src/scvi/dataloaders/__init__.py`
- `src/scvi/data/__init__.py`
- `src/scvi/criticism/__init__.py`
- `src/scvi/autotune/__init__.py`
- `src/scvi/module/base/__init__.py`
- `src/scvi/model/utils/__init__.py`
- `src/scvi/model/base/__init__.py`
- `src/scvi/external/velovi/__init__.py`
- `src/scvi/external/totalanvi/__init__.py`
- `src/scvi/external/tangram/__init__.py`

## Extracted headings
- Use Cases
- Background
- Variational Inference
- Approximating the posterior
- End-to-end learning
- Amortizing inference
- Counterfactual prediction
- Preliminaries
- In-distribution vs. out-of-distribution
- Applications

## Executable command hints
- $Q$ and the true posterior. As an example, if $Q$ is the family of multivariate Gaussians, then we would like to find the a

## Warnings and pitfalls
- where the first term is often called the "reconstruction error" and the second term as the KL divergence or "regularizer." Presenting the problem this way reveals that
- :::{warning}
