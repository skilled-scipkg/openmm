# openmm source map: Build and Install

Generated from source roots:
- `libraries`
- `olla`
- `openmmapi`
- `platforms`
- `plugins`
- `serialization`
- `wrappers`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `cmake`
- `build flags`
- `wrappers`
- `plugin build`
- `test installation`
- `opencl`
- `cuda`
- `hip`
- `cpu`
- `python wrappers`

## Fast source navigation
- `rg -n "OPENMM_BUILD_|OPENMM_GENERATE_API_DOCS|option\(" CMakeLists.txt docs-source wrappers platforms plugins`
- `rg -n "add_subdirectory|add_library|target_link_libraries" CMakeLists.txt docs-source wrappers platforms plugins`
- `rg -n "testInstallation|Platform.getPlatform" wrappers/python/openmm`

## Suggested source entry points
- `CMakeLists.txt` | top-level options, platform toggles, and install flow.
- `cmake_modules/FindOpenCL.cmake` | OpenCL detection and required variables.
- `docs-source/CMakeLists.txt` | docs build targets (`sphinxhtml`, `sphinxpdf`) and API docs integration.
- `wrappers/CMakeLists.txt` | wrapper build toggles and wrapper target wiring.
- `wrappers/generateWrappers.py` | wrapper generation stage used by build targets.
- `examples/CMakeLists.txt` | example target registration.
- `examples/cpp-examples/CMakeLists.txt` | C/C++/Fortran tutorial binary targets.
- `tests/CMakeLists.txt` | unit test target assembly.
- `platforms/cpu/CMakeLists.txt` | CPU platform build wiring.
- `platforms/opencl/CMakeLists.txt` | OpenCL platform build and linkage.
- `platforms/cuda/CMakeLists.txt` | CUDA platform build and linkage.
- `platforms/hip/CMakeLists.txt` | HIP platform build and linkage.
- `plugins/amoeba/CMakeLists.txt` | AMOEBA plugin build integration.
- `plugins/drude/CMakeLists.txt` | Drude plugin build integration.
- `plugins/rpmd/CMakeLists.txt` | RPMD plugin build integration.
- `plugins/cpupme/CMakeLists.txt` | CPU PME plugin build integration.
- `wrappers/python/openmm/testInstallation.py` | post-install runtime validation logic.
