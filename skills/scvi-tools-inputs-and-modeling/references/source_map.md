# scvi-tools source map: Inputs and Modeling

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `setup_anndata`
- `batch_key`
- `covariates`
- `training`
- `differential_expression`
- `multimodal`
- `dataloaders`
- `model-selection`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src`
- `rg -n "class|def" src/scvi/data src/scvi/model src/scvi/train src/scvi/dataloaders`

## Suggested source entry points
- `src/scvi/data/_manager.py` | registration/validation flow for model inputs.
- `src/scvi/data/fields/_layer_field.py` | count-layer registration behavior and state registry.
- `src/scvi/model/_scvi.py` | baseline scRNA model entry point.
- `src/scvi/model/_scanvi.py` | semisupervised modeling setup and transfer path.
- `src/scvi/model/_totalvi.py` | multimodal CITE-seq modeling and normalized outputs.
- `src/scvi/model/_multivi.py` | joint RNA/ATAC modeling behaviors.
- `src/scvi/model/base/_training_mixin.py` | shared training orchestration.
- `src/scvi/model/base/_differential.py` | DE/counterfactual-related computation internals.
- `src/scvi/dataloaders/_custom_dataloaders.py` | `MappedCollectionDataModule`/`TileDBDataModule` behavior.
- `src/scvi/train/_config.py` | typed train/trainer config contracts.
- `src/scvi/train/_callbacks.py` | callback-based control points for advanced runs.
- `src/scvi/external/totalanvi/_model.py` | semisupervised CITE-seq external modeling path.
- `src/scvi/external/sysvi/_model.py` | system-level integration model specifics.
