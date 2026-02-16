# Evidence: openmm-developer-guide

## Primary docs
- `docs-source/developerguide/index.rst`
- `docs-source/developerguide/08_common_compute.rst`
- `docs-source/developerguide/07_cuda_platform.rst`
- `docs-source/developerguide/03_writing_plugins.rst`
- `docs-source/developerguide/license.rst`
- `docs-source/developerguide/09_customcppforceimpl.rst`
- `docs-source/developerguide/05_cpu_platform.rst`
- `docs-source/developerguide/04_reference_platform.rst`

## Primary source entry points
- `skills/openmm-developer-guide/references/doc_map.md`
- `plugins/amoeba/platforms/common/src/kernels/hippoComputeField.cc`
- `plugins/rpmd/platforms/common/src/CommonRpmdKernelSources.h.in`
- `plugins/rpmd/platforms/common/src/CommonRpmdKernelSources.cpp.in`
- `plugins/drude/platforms/common/src/CommonDrudeKernelSources.h.in`
- `plugins/drude/platforms/common/src/CommonDrudeKernelSources.cpp.in`
- `plugins/amoeba/platforms/cuda/src/CudaAmoebaKernelSources.h.in`
- `plugins/amoeba/platforms/cuda/src/CudaAmoebaKernelSources.cpp.in`
- `plugins/amoeba/platforms/common/src/CommonAmoebaKernelSources.h.in`
- `plugins/amoeba/platforms/common/src/CommonAmoebaKernelSources.cpp.in`
- `plugins/amoeba/platforms/common/src/kernels/multipoleInducedField.cc`
- `plugins/amoeba/platforms/common/src/kernels/multipoleFixedField.cc`
- `plugins/amoeba/platforms/common/src/kernels/hippoMutualField.cc`
- `plugins/amoeba/platforms/common/src/kernels/hippoFixedField.cc`
- `plugins/rpmd/platforms/reference/CMakeLists.txt`
- `plugins/rpmd/platforms/cuda/CMakeLists.txt`
- `plugins/rpmd/platforms/common/CMakeLists.txt`
- `plugins/drude/platforms/reference/CMakeLists.txt`
- `plugins/drude/platforms/cuda/CMakeLists.txt`
- `plugins/drude/platforms/common/CMakeLists.txt`

## Extracted headings
- (none extracted)

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- device it becomes vitally important.  It is generally best to avoid storing
- SimTKOpenMMUtilities has various utility functions, of which the most important
