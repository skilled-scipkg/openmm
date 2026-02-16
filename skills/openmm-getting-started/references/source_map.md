# openmm source map: Getting Started

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
- `testInstallation`
- `HelloArgon`
- `first run`
- `platform detection`
- `python quickstart`
- `gpu availability`
- `reference platform`

## Fast source navigation
- `rg -n "testInstallation|Platform.getPlatform" wrappers/python/openmm`
- `rg -n "HelloArgon|REMARK  Using OpenMM platform" examples/cpp-examples`
- `rg -n "Platform::|loadPluginsFromDirectory" olla platforms`

## Suggested source entry points
- `wrappers/python/openmm/testInstallation.py` | first-run consistency checks across available platforms.
- `examples/cpp-examples/HelloArgon.cpp` | minimal executable simulation smoke test.
- `examples/cpp-examples/HelloSodiumChloride.cpp` | minimal PME-enabled simulation smoke test.
- `examples/cpp-examples/Makefile` | quick local build path for tutorial binaries.
- `examples/python-examples/simulatePdb.py` | first Python simulation script with common defaults.
- `wrappers/python/openmm/app/simulation.py` | Python runtime `Simulation` setup and stepping.
- `wrappers/python/openmm/app/forcefield.py` | force field loading path used by quickstarts.
- `wrappers/python/openmm/app/pdbfile.py` | structure loading path for common first examples.
- `wrappers/python/openmm/app/modeller.py` | hydrogen/solvent setup used in onboarding flows.
- `olla/src/Platform.cpp` | platform discovery and plugin loading behavior.
- `platforms/reference/src/ReferencePlatform.cpp` | guaranteed fallback platform behavior.
- `platforms/opencl/src/OpenCLPlatform.cpp` | OpenCL platform registration and properties.
- `platforms/cuda/src/CudaPlatform.cpp` | CUDA platform registration and properties.
- `platforms/hip/src/HipPlatform.cpp` | HIP platform registration and properties.
