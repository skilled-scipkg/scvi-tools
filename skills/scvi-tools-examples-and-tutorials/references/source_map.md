# scvi-tools source map: Examples and Tutorials

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `tutorial`
- `notebook`
- `workflow`
- `example`
- `transfer`
- `multimodal`
- `spatial`
- `cytometry`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/model src/scvi/external`

## Suggested source entry points
- `src/scvi/model/_scvi.py` | baseline scRNA tutorial model setup/training entry.
- `src/scvi/model/_scanvi.py` | label-transfer tutorial path (`from_scvi_model`, `setup_anndata`).
- `src/scvi/model/_totalvi.py` | CITE-seq tutorial operations (`get_normalized_expression`, DE).
- `src/scvi/model/_multivi.py` | multimodal ATAC+RNA tutorial behavior.
- `src/scvi/external/tangram/_model.py` | spatial mapping tutorial API (`train`, `project_*`).
- `src/scvi/external/scbasset/_model.py` | ATAC tutorial API (`train`, `get_tf_activity`).
- `src/scvi/external/contrastivevi/_model.py` | contrastive tutorial entry and salient-expression methods.
- `src/scvi/external/velovi/_model.py` | velocity tutorial methods (`get_velocity`, `get_latent_time`).
- `src/scvi/external/cytovi/_model.py` | cytometry tutorial methods (`get_normalized_expression`, DE).
- `src/scvi/external/methylvi/_methylvi_model.py` | methylation tutorial setup (`setup_anndata`, `setup_mudata`).
