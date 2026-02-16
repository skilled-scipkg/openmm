---
name: openmm-build-and-install
description: This skill should be used when users ask about build and install in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Build and Install

## High-Signal Playbook
### Route Conditions
- Use this skill for source builds, CMake option selection, wrapper/docs targets, and install/test failures (`docs-source/usersguide/library/02_compiling.rst`).
- Route package-manager quick install questions to `openmm-getting-started`.
- Route runtime script behavior and integrator/reporter tuning to `openmm-simulation-workflows`.
- Route wrapper/API semantics to `openmm-api-and-scripting`.

### Triage Questions
- Which OS/toolchain are you targeting (Linux/macOS with `ccmake` or Windows with `cmake-gui` + Visual Studio)? (`docs-source/usersguide/library/02_compiling.rst`)
- Do you need GPU backends (`OPENMM_BUILD_CUDA_LIB`, `OPENMM_BUILD_OPENCL_LIB`, `OPENMM_BUILD_HIP_LIB`) or CPU-only? (`CMakeLists.txt`)
- Do you need wrappers (`OPENMM_BUILD_PYTHON_WRAPPERS`, `OPENMM_BUILD_C_AND_FORTRAN_WRAPPERS`) and docs (`OPENMM_GENERATE_API_DOCS`)? (`CMakeLists.txt`, `docs-source/CMakeLists.txt`)
- Are you building shared, static, or both (`OPENMM_BUILD_SHARED_LIB`, `OPENMM_BUILD_STATIC_LIB`)? (`CMakeLists.txt`)
- What failed first: configure, compile, unit tests, install, or runtime loading? (`docs-source/usersguide/library/02_compiling.rst`)

### Canonical Workflow
1. Install prerequisites (`cmake`, compiler, `swig`, `cython`, `doxygen`, Python toolchain) (`docs-source/usersguide/library/02_compiling.rst`).
2. Configure a clean build dir and set key cache vars (`CMAKE_INSTALL_PREFIX`, `PYTHON_EXECUTABLE`, relevant `OPENMM_BUILD_*`) (`docs-source/usersguide/library/02_compiling.rst`, `CMakeLists.txt`).
3. Build with `make` (or Visual Studio Build Solution) (`docs-source/usersguide/library/02_compiling.rst`).
4. Run tests with `make test`; re-run failing suites directly for detail (`docs-source/usersguide/library/02_compiling.rst`).
5. Install core libs (`make install`) and Python API (`make PythonInstall`) (`docs-source/usersguide/library/02_compiling.rst`).
6. Validate runtime with `python -m openmm.testInstallation`; optionally run tutorial binaries (`docs-source/usersguide/library/02_compiling.rst`, `examples/cpp-examples/README.md`).

### Minimal Working Example
```bash
conda install -c conda-forge cmake make cython swig doxygen numpy setuptools
mkdir build && cd build
ccmake ..
make -j
make test
make install
make PythonInstall
python -m openmm.testInstallation
```

### Pitfalls and Fixes
- Problem: CMake cannot find OpenCL headers/libs. Fix: set `OPENCL_INCLUDE_DIR` and `OPENCL_LIBRARY` explicitly (`docs-source/usersguide/library/02_compiling.rst`).
- Problem: Windows build cannot find conda tools. Fix: launch `cmake-gui` from Anaconda Prompt, not Start menu (`docs-source/usersguide/library/02_compiling.rst`).
- Problem: intermittent test failures. Fix: re-run individual stochastic tests before escalating (`docs-source/usersguide/library/02_compiling.rst`).
- Problem: example executables fail at runtime due to missing shared libs. Fix: export library path (`LD_LIBRARY_PATH`/`DYLD_LIBRARY_PATH`/`PATH`) (`examples/cpp-examples/README.md`).
- Problem: wrong binary mode in Visual Studio. Fix: build `Release`, not `Debug` (`docs-source/usersguide/library/02_compiling.rst`, `docs-source/usersguide/library/03_tutorials.rst`).
- Problem: wrappers/docs expected but not generated. Fix: enable wrapper/docs options at configure time (`CMakeLists.txt`, `docs-source/CMakeLists.txt`, `wrappers/CMakeLists.txt`).

### Convergence and Validation Checks
- Unit test matrix should pass; investigate only persistent non-stochastic failures (`docs-source/usersguide/library/02_compiling.rst`).
- `python -m openmm.testInstallation` should report platform availability and consistency (`docs-source/usersguide/library/02_compiling.rst`).
- Validate a tiny run (`HelloArgon`) before scaling to production models (`examples/cpp-examples/README.md`).
- If switching precision/backend, re-check energy behavior and force agreement expectations (`docs-source/usersguide/library/07_testing_validation.rst`, `docs-source/usersguide/library/04_platform_specifics.rst`).

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/cpp-examples/README.md`
- `examples/cpp-examples/CMakeLists.txt`
- `platforms/opencl/tests/CMakeLists.txt`
- `docs-source/usersguide/library/02_compiling.rst`
- `docs-source/usersguide/application/03_model_building_editing.rst`
- `tests/CMakeLists.txt`
- `docs-source/CMakeLists.txt`
- `examples/CMakeLists.txt`
- `serialization/tests/CMakeLists.txt`
- `examples/python-examples/CMakeLists.txt`
- `plugins/cpupme/tests/CMakeLists.txt`
- `platforms/reference/tests/CMakeLists.txt`

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
- `CMakeLists.txt`
- `cmake_modules/FindOpenCL.cmake`
- `docs-source/CMakeLists.txt`
- `wrappers/CMakeLists.txt`
- `examples/CMakeLists.txt`
- `examples/cpp-examples/CMakeLists.txt`
- `tests/CMakeLists.txt`
- `wrappers/generateWrappers.py`
- `platforms/cpu/CMakeLists.txt`
- `platforms/opencl/CMakeLists.txt`
- `platforms/cuda/CMakeLists.txt`
- `platforms/hip/CMakeLists.txt`
- `plugins/amoeba/CMakeLists.txt`
- `plugins/drude/CMakeLists.txt`
- `plugins/rpmd/CMakeLists.txt`
- `plugins/cpupme/CMakeLists.txt`
- `wrappers/python/openmm/testInstallation.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" CMakeLists.txt docs-source wrappers platforms plugins`).
