---
name: openmm-getting-started
description: This skill should be used when users ask about getting started in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Getting Started

## High-Signal Playbook
### Route Conditions
- Use this skill for first-run installation checks, first simulation smoke tests, and platform detection (`docs-source/usersguide/application/01_getting_started.rst`, `docs-source/usersguide/library/03_tutorials.rst`).
- Route source builds, compiler/toolchain issues, and CMake options to `openmm-build-and-install`.
- Route wrapper mappings, unit semantics, and language-API differences to `openmm-api-and-scripting`.
- Route integrator tuning, checkpoint/restart strategy, and advanced run control to `openmm-simulation-workflows`.

### Triage Questions
- Are you installing with `conda`, `pip`, or from source? (`docs-source/usersguide/application/01_getting_started.rst`)
- Which hardware path do you need: NVIDIA CUDA, AMD HIP, OpenCL, or CPU-only? (`docs-source/usersguide/application/01_getting_started.rst`)
- Do you need the Python application layer now, or C++ tutorial binaries first? (`docs-source/usersguide/library/01_introduction.rst`, `docs-source/usersguide/library/03_tutorials.rst`)
- Have you already run `python -m openmm.testInstallation` and captured platform output? (`docs-source/usersguide/application/01_getting_started.rst`)
- Do you need a quick functionality check (`HelloArgon`) or integration template (`HelloSodiumChloride`)? (`docs-source/usersguide/library/03_tutorials.rst`)

### Canonical Workflow
1. Choose package install path (`conda`/`pip`) and match GPU runtime support to hardware (`docs-source/usersguide/application/01_getting_started.rst`).
2. Install OpenMM and optional accelerator extras (`cuda12`, `cuda13`, `hip6`, `hip7`) as needed (`docs-source/usersguide/application/01_getting_started.rst`).
3. Run `python -m openmm.testInstallation` to validate platforms and consistency (`docs-source/usersguide/application/01_getting_started.rst`).
4. Run `HelloArgon` to confirm execution path and read the printed platform banner (`docs-source/usersguide/library/03_tutorials.rst`).
5. If results are good, move to application scripts; if not, route build/runtime issues to `openmm-build-and-install`.

### Minimal Working Example
```bash
conda install -c conda-forge openmm
python -m openmm.testInstallation

cd examples/cpp-examples
make
./HelloArgon > argon.pdb
```

### Pitfalls and Fixes
- Problem: assuming source build is required for normal use. Fix: prefer package install first; source build is mainly for advanced/custom work (`docs-source/usersguide/application/01_getting_started.rst`).
- Problem: GPU unavailable after install. Fix: install current vendor drivers and match package extras to device/runtime (`docs-source/usersguide/application/01_getting_started.rst`).
- Problem: expecting HIP from conda package. Fix: use pip HIP extras for AMD HIP path (`docs-source/usersguide/application/01_getting_started.rst`).
- Problem: mixing up application layer and library layer onboarding. Fix: use application-layer `Getting Started` first, then library tutorials (`docs-source/usersguide/application/01_getting_started.rst`, `docs-source/usersguide/library/01_introduction.rst`).
- Problem: no quick signal that execution is on GPU vs Reference CPU. Fix: check first output line from `HelloArgon` (`docs-source/usersguide/library/03_tutorials.rst`).

### Convergence and Validation Checks
- `python -m openmm.testInstallation` should complete without errors and report expected platforms (`docs-source/usersguide/application/01_getting_started.rst`).
- `HelloArgon` should run and print `REMARK  Using OpenMM platform ...` (`docs-source/usersguide/library/03_tutorials.rst`).
- For later production runs, treat precision mode, timestep, and constraint tolerance as first-order accuracy knobs (`docs-source/usersguide/library/04_platform_specifics.rst`, `docs-source/usersguide/library/07_testing_validation.rst`).
- If deterministic behavior is required, explicitly verify platform/settings combination supports it (`docs-source/usersguide/library/04_platform_specifics.rst`).

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs-source/usersguide/introduction.rst`
- `docs-source/developerguide/06_opencl_platform.rst`
- `docs-source/usersguide/library/03_tutorials.rst`
- `docs-source/usersguide/library/01_introduction.rst`
- `docs-source/usersguide/theory/01_introduction.rst`
- `docs-source/usersguide/application/01_getting_started.rst`
- `docs-source/developerguide/01_introduction.rst`

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
- `wrappers/python/openmm/testInstallation.py`
- `examples/cpp-examples/HelloArgon.cpp`
- `examples/cpp-examples/HelloSodiumChloride.cpp`
- `examples/cpp-examples/Makefile`
- `examples/python-examples/simulatePdb.py`
- `wrappers/python/openmm/app/simulation.py`
- `wrappers/python/openmm/app/forcefield.py`
- `wrappers/python/openmm/app/pdbfile.py`
- `wrappers/python/openmm/app/modeller.py`
- `olla/src/Platform.cpp`
- `platforms/reference/src/ReferencePlatform.cpp`
- `platforms/opencl/src/OpenCLPlatform.cpp`
- `platforms/cuda/src/CudaPlatform.cpp`
- `platforms/hip/src/HipPlatform.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" examples wrappers/python/openmm/app olla platforms`).
