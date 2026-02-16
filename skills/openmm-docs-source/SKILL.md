---
name: openmm-docs-source
description: This skill should be used when users ask about docs source in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Docs Source

## High-Signal Playbook
### Route Conditions
- Use this skill for documentation provenance/build questions, licensing text, and doc-toolchain generation paths (`docs-source/usersguide/license.rst`, `docs-source/usersguide/zbibliography.rst`, `docs-source/CMakeLists.txt`).
- Route technical simulation content to domain skills (`openmm-getting-started`, `openmm-api-and-scripting`, `openmm-simulation-workflows`).
- Route plugin/kernel implementation internals to `openmm-developer-guide`.

### Triage Questions
- Do you need HTML/PDF user/developer guide outputs, API docs, or license/citation references?
- Are Python wrappers enabled when requesting Python API docs? (`wrappers/CMakeLists.txt`)
- Is Doxygen available/configured for API doc generation? (`wrappers/Doxyfile.in`)
- Is this a legal-text lookup (`docs-source/licenses/*.txt`) or build-pipeline issue (`docs-source/CMakeLists.txt`)?

### Canonical Workflow
1. Identify target artifact class: docs output, API reference output, or license/citation text.
2. Build docs targets (`sphinxhtml`, `sphinxpdf`) from configured build directory (`docs-source/CMakeLists.txt`).
3. For API docs, enable `OPENMM_GENERATE_API_DOCS` and wrapper generation dependencies (`docs-source/CMakeLists.txt`, `wrappers/CMakeLists.txt`).
4. Trace wrapper-doc path from `wrappers/Doxyfile.in` and SWIG inputs to `wrappers/generateWrappers.py`.
5. For licensing responses, quote canonical texts in `docs-source/usersguide/license.rst` and `docs-source/licenses/Licenses.txt`.

### Minimal Working Example
```bash
cmake -S . -B build \
  -DOPENMM_BUILD_PYTHON_WRAPPERS=ON \
  -DOPENMM_GENERATE_API_DOCS=ON
cmake --build build --target sphinxhtml
cmake --build build --target sphinxpdf
```

### Pitfalls and Fixes
- Problem: expecting API docs without enabling API-doc generation. Fix: set `OPENMM_GENERATE_API_DOCS=ON`.
- Problem: expecting Python API docs with wrappers disabled. Fix: enable `OPENMM_BUILD_PYTHON_WRAPPERS=ON`.
- Problem: wrapper-doc generation failures after Doxygen stage. Fix: verify Doxygen config and wrapper generation steps (`wrappers/Doxyfile.in`, `wrappers/generateWrappers.py`).
- Problem: incomplete licensing response. Fix: include `docs-source/licenses/Licenses.txt`, `docs-source/licenses/LGPL.txt`, and `docs-source/licenses/GPL.txt`.

### Convergence and Validation Checks
- Confirm HTML docs index exists in build output tree after `sphinxhtml`.
- Confirm PDF artifacts are emitted after `sphinxpdf`.
- Confirm Doxygen XML generation succeeded before wrapper-doc generation.
- Confirm citation text resolves through `docs-source/usersguide/zbibliography.rst`.

## Scope
- Handle questions about documentation grouped under the 'docs-source' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs-source/usersguide/zbibliography.rst`
- `docs-source/usersguide/license.rst`
- `docs-source/usersguide/application.rst`
- `docs-source/licenses/Licenses.txt`
- `docs-source/licenses/LGPL.txt`
- `docs-source/licenses/GPL.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `examples`

## Test references
- `tests`
- `serialization/tests`
- `platforms/cpu/tests`
- `platforms/cuda/tests`
- `platforms/hip/tests`
- `platforms/opencl/tests`
- `platforms/reference/tests`
- `plugins/amoeba/tests`
- `plugins/cpupme/tests`
- `plugins/drude/tests`
- `plugins/rpmd/tests`
- `wrappers/python/tests`
- `plugins/amoeba/serialization/tests`
- `plugins/drude/serialization/tests`
- `plugins/amoeba/platforms/cuda/tests`
- `plugins/amoeba/platforms/hip/tests`
- `plugins/amoeba/platforms/opencl/tests`
- `plugins/amoeba/platforms/reference/tests`
- `plugins/drude/platforms/cuda/tests`
- `plugins/drude/platforms/hip/tests`
- `plugins/drude/platforms/opencl/tests`
- `plugins/drude/platforms/reference/tests`
- `plugins/rpmd/platforms/cuda/tests`
- `plugins/rpmd/platforms/hip/tests`
- `plugins/rpmd/platforms/opencl/tests`
- `plugins/rpmd/platforms/reference/tests`

## Optional deeper inspection
- `libraries`
- `olla`
- `openmmapi`
- `platforms`
- `plugins`
- `serialization`
- `wrappers`

## Source entry points for unresolved issues
- `docs-source/CMakeLists.txt`
- `docs-source/api-c++/CMakeLists.txt`
- `docs-source/api-python/CMakeLists.txt`
- `wrappers/CMakeLists.txt`
- `wrappers/Doxyfile.in`
- `wrappers/python/src/swig_doxygen/doxygen/Doxyfile.in`
- `wrappers/python/src/swig_doxygen/swigInputBuilder.py`
- `wrappers/python/src/swig_doxygen/OpenMM.i`
- `wrappers/generateWrappers.py`
- `docs-source/usersguide/license.rst`
- `docs-source/usersguide/zbibliography.rst`
- `docs-source/licenses/Licenses.txt`
- `docs-source/licenses/LGPL.txt`
- `docs-source/licenses/GPL.txt`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" docs-source wrappers`).
