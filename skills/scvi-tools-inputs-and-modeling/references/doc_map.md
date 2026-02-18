# scvi-tools documentation map: Inputs and Modeling

Generated from documentation roots:
- `docs`
- `docs/tutorials`
- `tests`

Total docs grouped in this topic: 43

## File inventory
- `docs/index.md` | title: Documentation | headings: Documentation; Model hub <https://huggingface.co/scvi-tools>
- `docs/user_guide/models/index.md` | title: Models | headings: Models; velovi
- `docs/tutorials/index_scrna.md` | title: scRNA-seq | headings: scRNA-seq; notebooks/scrna/Tahoe100_mrVI_Jax; Perform integration of multiple scRNA-seq datasets both with and without cell type annotation (scVI and scANVI)
- `docs/api/user.md` | title: User | headings: User; Model; External models
- `docs/api/developer.md` | title: Developer | headings: Developer; Data Registration; Data Loaders
- `docs/tutorials/index_use_cases.md` | title: Common Modelling Use Cases | headings: Common Modelling Use Cases; notebooks/use_cases/multiGPU; Learn how to preprocess various types of data for use with scvi-tools models.
- `docs/tutorials/index_multimodal.md` | title: Multimodal | headings: Multimodal; notebooks/multimodal/MultiVI_tutorial; Go through the totalVI workflow to analyze CITE-seq datasets
- `docs/user_guide/use_case/multi_gpu_training.md` | title: Train SCVI model with multi-GPU support | headings: Train SCVI model with multi-GPU support; Some of the benefits of using MultiGPU training; 1. **Faster Training**
- `docs/user_guide/models/totalanvi.md` | title: TotalANVI | headings: TotalANVI; Preliminaries; Generative process
- `docs/user_guide/models/sysvi.md` | title: SysVI | headings: SysVI; Method background; Stronger batch correction with cycle-consistency loss
- `docs/user_guide/use_case/custom_dataloaders.md` | title: Train SCVI model with custom dataloaders | headings: Train SCVI model with custom dataloaders; a test for mapped collection; this test checks the local custom dataloader made by CZI and run several tests with it
- `docs/user_guide/models/scar.md` | title: scAR | headings: scAR; Ambient RNA removal; Estimating the ambient profile
- `docs/user_guide/models/mrvi.md` | title: MrVI | headings: MrVI; Preliminaries; Generative process
- `docs/user_guide/models/autozi.md` | title: AUTOZI | headings: AUTOZI; Generative process; Inference Procedure
- `docs/user_guide/background/differential_expression.md` | title: Differential Expression | headings: Differential Expression; Problem statement; Motivation
- `docs/user_guide/models/totalvi.md` | title: totalVI | headings: totalVI; Preliminaries; Generative process
- `docs/user_guide/models/stereoscope.md` | title: Stereoscope | headings: Stereoscope; Preliminaries; Generative process
- `docs/user_guide/models/scviva.md` | title: scVIVA | headings: scVIVA; Preliminaries; Descriptive model
- `docs/user_guide/models/scvi.md` | title: scVI | headings: scVI; Preliminaries; Generative process
- `docs/user_guide/models/scanvi.md` | title: scANVI | headings: scANVI; Preliminaries; Generative process
- `docs/user_guide/models/resolvi.md` | title: ResolVI | headings: ResolVI; Preliminaries; Generative process
- `docs/user_guide/models/peakvi.md` | title: PeakVI | headings: PeakVI; Preliminaries; Generative process
- `docs/user_guide/models/multivi.md` | title: MultiVI | headings: MultiVI; Preliminaries; Generative process
- `docs/user_guide/models/methylvi.md` | title: MethylVI | headings: MethylVI; Preliminaries; Generative process
- `docs/user_guide/models/methylanvi.md` | title: MethylANVI | headings: MethylANVI; Preliminaries; Generative process
- `docs/user_guide/models/destvi.md` | title: DestVI | headings: DestVI; Preliminaries; Generative process
- `docs/user_guide/models/cytovi.md` | title: CytoVI | headings: CytoVI; Preliminaries; Descriptive model
- `docs/user_guide/models/cellassign.md` | title: CellAssign | headings: CellAssign; Preliminaries; Generative process
- `docs/user_guide/models/amortizedlda.md` | title: Amortized LDA | headings: Amortized LDA; Preliminaries; Generative process
- `docs/tutorials/index_hub.md` | title: Model hub | headings: Model hub; Learn how to use Hugging Face and scvi-hub to download pretrained scvi-tools models; Learn how to upload pretrained scvi-tools models to Hugging Face
- `docs/tutorials/index_custom_dl.md` | title: Custom Data Loaders | headings: Custom Data Loaders; notebooks/custom_dl/Tahoe100_mrVI_lamin; Learn a scalable approach using TileDBDataModule dataloader to training an scVI model on Census data.
- `docs/user_guide/use_case/training_configuration.md` | title: Training configuration | headings: Training configuration; When to use which config; Example (SCVI)
- `docs/tutorials/index_dev.md` | title: Development | headings: Development; notebooks/dev/model_user_guide; Learn about how data is handled in scvi-tools
- `docs/user_guide/use_case/scvi_criticism.md` | title: SCVI Criticism | headings: SCVI Criticism; There are a few metrics we calculate to achieve that:; Example of use:
- `docs/faq.md` | title: Frequently asked questions | headings: Frequently asked questions; What is the difference between `batch_key` and `categorical_covariate_keys`?; My model errors out during training due to `NaN`s - how can I fix this?
- `docs/user_guide/use_case/using_callbacks.md` | title: Train SCVI model with callbacks | headings: Train SCVI model with callbacks; model.train(..., **early_stopping_kwargs); model.train(..., trainer_config=trainer_config, plan_config=plan_config)
- `docs/user_guide/use_case/saving_and_loading_models.md` | title: Saving and loading SCVI models | headings: Saving and loading SCVI models; Saving a model; Loading a model
- `docs/user_guide/models/linearscvi.md` | title: LDVAE | headings: LDVAE; Contrasting with scVI; tutorial link to linear-decoder walkthrough
- `docs/user_guide/use_case/downstream_analysis_tasks.md` | title: Perform downstream analysis tasks of SCVI models | headings: Perform downstream analysis tasks of SCVI models; differential_expression = scvi.model.SCVI().differential_expression()
- `docs/user_guide/models/velovi.md` | title: VeloVI | headings: VeloVI; tutorial link to RNA velocity walkthrough
- `docs/user_guide/models/poissonvi.md` | title: PoissonVI | headings: PoissonVI; tutorial link to ATAC PoissonVI walkthrough
- `docs/user_guide/models/gimvi.md` | title: gimVI | headings: gimVI; tutorial link to spatial gimVI walkthrough
- `docs/user_guide/models/decipher.md` | title: Decipher | headings: Decipher; tutorial link to decipher workflow walkthrough
