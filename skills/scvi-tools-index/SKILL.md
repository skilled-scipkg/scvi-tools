---
name: scvi-tools-index
description: This skill should be used when users ask how to use scvi-tools and the correct generated documentation skill must be selected before going deeper into source code.
---

# scvi-tools Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.

## Generated topic skills
- `scvi-tools-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `scvi-tools-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `scvi-tools-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `scvi-tools-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `scvi-tools-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `scvi-tools-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `scvi-tools-user-guide`: User Guide (documentation grouped under the 'user-guide' theme)
- `scvi-tools-tests`: Tests (documentation grouped under the 'tests' theme)
- `scvi-tools-advanced-topics`: Advanced Topics (consolidated low-signal single-doc topics: analysis/output, developer docs, references, changelog)

## Documentation-first inputs
- `docs`

## Tutorials and examples roots
- `docs/tutorials`

## Test roots for behavior checks
- `tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open the selected topic skill's doc map (for example, `skills/scvi-tools-simulation-workflows/references/doc_map.md`).
- If documentation still leaves ambiguity, open that same skill's source map (for example, `skills/scvi-tools-simulation-workflows/references/source_map.md`).
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" src`).

## Source directories for deeper inspection
- `src`
