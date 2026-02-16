# openmm source map: Developer Guide

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
- `plugin registration`
- `kernel factory`
- `platform internals`
- `context internals`
- `customcppforceimpl`
- `common compute`
- `serialization registration`
- `reference parity`

## Fast source navigation
- `rg -n "registerPlatforms|registerKernelFactories|PluginInitializer" olla plugins platforms`
- `rg -n "KernelFactory|createKernel|registerKernelFactory" platforms plugins`
- `rg -n "CustomCPPForceImpl|ContextImpl|PlatformData" openmmapi platforms`

## Suggested source entry points
- `olla/include/openmm/PluginInitializer.h` | required exported plugin initialization symbols.
- `olla/include/openmm/Platform.h` | platform registration, property APIs, and plugin loading interfaces.
- `olla/src/Platform.cpp` | plugin loading and platform registry internals.
- `openmmapi/include/openmm/internal/ContextImpl.h` | context internals used by platform kernels.
- `openmmapi/src/ContextImpl.cpp` | context state transitions and kernel dispatch integration.
- `openmmapi/src/CustomCPPForceImpl.cpp` | platform-independent force implementation path.
- `platforms/reference/src/ReferencePlatform.cpp` | baseline platform registration and reference behavior.
- `platforms/cpu/src/CpuPlatform.cpp` | CPU platform setup and property defaults.
- `platforms/opencl/src/OpenCLPlatform.cpp` | OpenCL platform registration and property parsing.
- `platforms/cuda/src/CudaPlatform.cpp` | CUDA platform registration and property parsing.
- `platforms/hip/src/HipPlatform.cpp` | HIP platform registration and property parsing.
- `platforms/opencl/src/OpenCLKernelFactory.cpp` | OpenCL kernel factory wiring.
- `platforms/cuda/src/CudaKernelFactory.cpp` | CUDA kernel factory wiring.
- `platforms/hip/src/HipKernelFactory.cpp` | HIP kernel factory wiring.
- `plugins/amoeba/platforms/cuda/src/AmoebaCudaKernelFactory.cpp` | plugin kernel registration for CUDA path.
- `plugins/drude/platforms/reference/src/ReferenceDrudeKernelFactory.cpp` | plugin kernel registration for Reference path.
- `plugins/rpmd/platforms/cuda/src/CudaRpmdKernelFactory.cpp` | RPMD kernel registration for CUDA path.
- `plugins/amoeba/serialization/src/AmoebaSerializationProxyRegistration.cpp` | plugin serialization registration hooks.
- `plugins/drude/serialization/src/DrudeSerializationProxyRegistration.cpp` | plugin serialization registration hooks.
