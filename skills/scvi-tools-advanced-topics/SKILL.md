---
name: scvi-tools-advanced-topics
description: This skill should be used when users ask about narrower scvi-tools topics that were each represented by a single documentation page; it consolidates those docs into one routing skill before source inspection.
---

# scvi-tools: Advanced Topics

## Route the request
- `analysis-and-output` style requests: route to `docs/user_guide/index.md` for task/model matrix and analysis capability coverage.
- `developer-guide` style requests: route to `docs/developer/index.md` for contribution and maintenance entry points.
- `references` style requests: route to `docs/references.md` for bibliography lookup and citation context.
- `changelog` style requests: route to `docs/changelog.md` for release deltas.

## Workflow
- Start from the exact primary doc listed for the subtopic.
- If doc detail is insufficient, inspect `references/doc_map.md` for combined inventory.
- Escalate to `references/source_map.md` for concrete source entry links.
- Keep responses concise and cite exact doc paths.

## Primary documentation references
- `docs/user_guide/index.md`
- `docs/developer/index.md`
- `docs/references.md`
- `docs/changelog.md`

## Source entry points for unresolved issues
- `src/scvi/train/_callbacks.py`
- `src/scvi/train/_config.py`
- `src/scvi/model/base/_training_mixin.py`
- `src/scvi/model/base/_save_load.py`
- `src/scvi/data/_preprocessing.py`
- `src/scvi/external/cytovi/_plotting.py`
- `src/scvi/external/decipher/utils/_trajectory.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
