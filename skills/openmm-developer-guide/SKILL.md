---
name: openmm-developer-guide
description: This skill should be used when users ask about developer guide in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Developer Guide

## High-Signal Playbook
### Route Conditions
- Use this skill for extending OpenMM internals: new platforms, new force plugins, kernel factories, Common Compute, and platform-independent `CustomCPPForceImpl` paths (`docs-source/developerguide/03_writing_plugins.rst`, `docs-source/developerguide/08_common_compute.rst`, `docs-source/developerguide/09_customcppforceimpl.rst`).
- Route user-side simulation scripts and protocol tuning to `openmm-simulation-workflows`.
- Route build/install failures to `openmm-build-and-install`.
- Route Python/C/Fortran wrapper usage to `openmm-api-and-scripting`.

### Triage Questions
- Are you adding a new `Platform`, a new `Force` for existing platforms, or both? (`docs-source/developerguide/03_writing_plugins.rst`)
- Do you need high-performance platform-specific kernels, or is `CustomCPPForceImpl` sufficient? (`docs-source/developerguide/09_customcppforceimpl.rst`)
- Are you targeting CUDA/OpenCL dual support via Common Compute abstractions? (`docs-source/developerguide/08_common_compute.rst`)
- Have `registerPlatforms()` and `registerKernelFactories()` been exported and wired? (`docs-source/developerguide/03_writing_plugins.rst`)
- Which platform implementation diverges from expected behavior (Reference/CPU/CUDA/HIP/OpenCL)?

### Canonical Workflow
1. Decide extension shape: public API class + `ForceImpl` + kernel interface, or platform-only addition.
2. Implement plugin registration functions and factory wiring for each target platform.
3. Use shared abstractions for CUDA/OpenCL where practical; keep reference implementation as a correctness baseline.
4. If external library code dominates compute, consider `CustomCPPForceImpl` to avoid full kernel stack.
5. Build, load plugin from plugin path, and verify registration before numerical tuning.
6. Validate against Reference behavior and targeted tests before broad rollout.

### Minimal Working Example
```cpp
// Plugin entry points required by olla/include/openmm/PluginInitializer.h
extern "C" void registerPlatforms();
extern "C" void registerKernelFactories();

Platform::loadPluginsFromDirectory(Platform::getDefaultPluginsDirectory());
```

### Pitfalls and Fixes
- Problem: trying to ship a new public `Force` from only a runtime plugin library. Fix: provide API header + link library + plugin runtime library trio.
- Problem: missing/hidden registration symbols. Fix: export exact `extern "C"` function names from `olla/include/openmm/PluginInitializer.h`.
- Problem: OpenCL/CUDA common kernels fail due type/macro mismatch. Fix: use Common Compute-supported types/macros and avoid backend-specific assumptions.
- Problem: plugin hard-fails when target platform unavailable. Fix: catch platform lookup exceptions and skip registration gracefully.
- Problem: over-engineered platform code for simple external-force wrapper case. Fix: use `CustomCPPForceImpl` where it is sufficient.

### Convergence and Validation Checks
- Verify kernel registration coverage for every exposed force/integrator path.
- Compare forces/energies against Reference and platform baselines before performance tuning (`docs-source/usersguide/library/07_testing_validation.rst`).
- Validate precision/determinism assumptions per backend before claiming reproducibility (`docs-source/usersguide/library/04_platform_specifics.rst`).
- Ensure tests cover plugin load, kernel dispatch, and serialization where applicable.

## Scope
- Handle questions about developer architecture, extension points, and contribution workflow.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs-source/developerguide/index.rst`
- `docs-source/developerguide/08_common_compute.rst`
- `docs-source/developerguide/07_cuda_platform.rst`
- `docs-source/developerguide/03_writing_plugins.rst`
- `docs-source/developerguide/license.rst`
- `docs-source/developerguide/09_customcppforceimpl.rst`
- `docs-source/developerguide/05_cpu_platform.rst`
- `docs-source/developerguide/04_reference_platform.rst`

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
- `olla/include/openmm/PluginInitializer.h`
- `olla/include/openmm/Platform.h`
- `olla/src/Platform.cpp`
- `openmmapi/include/openmm/internal/ContextImpl.h`
- `openmmapi/src/ContextImpl.cpp`
- `openmmapi/src/CustomCPPForceImpl.cpp`
- `platforms/reference/src/ReferencePlatform.cpp`
- `platforms/cpu/src/CpuPlatform.cpp`
- `platforms/opencl/src/OpenCLPlatform.cpp`
- `platforms/cuda/src/CudaPlatform.cpp`
- `platforms/hip/src/HipPlatform.cpp`
- `platforms/opencl/src/OpenCLKernelFactory.cpp`
- `platforms/cuda/src/CudaKernelFactory.cpp`
- `platforms/hip/src/HipKernelFactory.cpp`
- `plugins/amoeba/platforms/cuda/src/AmoebaCudaKernelFactory.cpp`
- `plugins/drude/platforms/reference/src/ReferenceDrudeKernelFactory.cpp`
- `plugins/rpmd/platforms/cuda/src/CudaRpmdKernelFactory.cpp`
- `plugins/amoeba/serialization/src/AmoebaSerializationProxyRegistration.cpp`
- `plugins/drude/serialization/src/DrudeSerializationProxyRegistration.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" olla openmmapi platforms plugins`).
