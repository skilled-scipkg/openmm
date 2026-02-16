---
name: openmm-api-and-scripting
description: This skill should be used when users ask about api and scripting in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: API and Scripting

## High-Signal Playbook
### Route Conditions
- Use this skill for language bindings (Python/C/C++/Fortran), wrapper behavior, platform-property control, and API-level validation (`docs-source/usersguide/library/05_languages_not_cpp.rst`, `docs-source/usersguide/library/04_platform_specifics.rst`).
- Route install/build toolchain questions to `openmm-build-and-install`.
- Route full simulation protocol design (equilibration/restart/reporters) to `openmm-simulation-workflows`.
- Route plugin architecture and kernel authoring to `openmm-developer-guide`.

### Triage Questions
- Which API surface are you using now: Python, C++, C wrapper, or Fortran wrapper? (`docs-source/usersguide/library/05_languages_not_cpp.rst`)
- Are unit-bearing Python quantities being mixed with raw numbers from non-unit APIs? (`docs-source/usersguide/library/05_languages_not_cpp.rst`)
- Do you need explicit platform properties (`Precision`, `DeviceIndex`, `UseCpuPme`, determinism settings)? (`docs-source/usersguide/library/04_platform_specifics.rst`)
- Is your issue semantic (API mapping), runtime (library path/platform select), or numerical (precision/drift)? (`docs-source/usersguide/library/05_languages_not_cpp.rst`, `docs-source/usersguide/library/07_testing_validation.rst`)
- Are you integrating OpenMM into an external codebase through C API wrappers? (`docs-source/usersguide/library/05_languages_not_cpp.rst`, `docs-source/usersguide/library/06_integration_examples.rst`)

### Canonical Workflow
1. Pick primary language API and confirm wrapper availability/build options (`docs-source/usersguide/library/05_languages_not_cpp.rst`, `CMakeLists.txt`).
2. Start from minimal object creation in that API (System/Force/Context) and keep units explicit in Python (`docs-source/usersguide/library/05_languages_not_cpp.rst`).
3. If backend control is needed, pass platform + property map at Context/Simulation creation (`docs-source/usersguide/library/04_platform_specifics.rst`, `wrappers/python/openmm/app/simulation.py`).
4. Run a short validation job and compare expected behavior across precision/platform choices (`docs-source/usersguide/library/07_testing_validation.rst`).
5. For unresolved binding behavior, inspect generated wrapper pipeline and concrete implementation files (`wrappers/generateWrappers.py`, `wrappers/python/openmm/__init__.py`).

### Minimal Working Example
```python
import openmm as mm
import openmm.unit as unit

system = mm.System()
nb = mm.NonbondedForce()
nb.setNonbondedMethod(mm.NonbondedForce.CutoffNonPeriodic)
nb.setCutoffDistance(1.2 * unit.nanometer)
system.addForce(nb)

platform = mm.Platform.getPlatformByName("OpenCL")
properties = {"DeviceIndex": "0", "Precision": "mixed"}
context = mm.Context(system, mm.VerletIntegrator(0.001), platform, properties)
```

### Pitfalls and Fixes
- Problem: C API leaks around `getState()`/plugin-load results. Fix: explicitly destroy heap objects returned by wrapper helpers (`docs-source/usersguide/library/05_languages_not_cpp.rst`).
- Problem: Python unit mismatch exceptions. Fix: keep arithmetic dimensionally consistent and use `openmm.unit` helpers (`docs-source/usersguide/library/05_languages_not_cpp.rst`).
- Problem: hidden conversion bugs from stripping units too early with `value_in_unit()`. Fix: delay conversion to API boundaries (`docs-source/usersguide/library/05_languages_not_cpp.rst`).
- Problem: nondeterministic or drifting results blamed on API layer. Fix: evaluate precision mode, timestep, constraints, PME tolerance first (`docs-source/usersguide/library/04_platform_specifics.rst`, `docs-source/usersguide/library/07_testing_validation.rst`).
- Problem: setting platform properties without explicit platform object in high-level API. Fix: pass both platform and properties together (`wrappers/python/openmm/app/simulation.py`).
- Problem: using Python `math.sqrt` on quantities. Fix: use `openmm.unit.sqrt` (`docs-source/usersguide/library/05_languages_not_cpp.rst`).

### Convergence and Validation Checks
- For GPU workflows, test `single` vs `mixed` vs `double` precision and verify acceptable energy drift (`docs-source/usersguide/library/04_platform_specifics.rst`, `docs-source/usersguide/library/07_testing_validation.rst`).
- Re-check timestep, constraints, nonbonded cutoff, and Ewald tolerance before attributing errors to wrappers (`docs-source/usersguide/library/07_testing_validation.rst`).
- Run installation/consistency checks before deeper API debugging (`docs-source/usersguide/application/01_getting_started.rst`).
- If integrating with external engines, validate unit conversions explicitly at API boundaries (`docs-source/usersguide/library/06_integration_examples.rst`).

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/README.md`
- `docs-source/api-python/index.rst`
- `docs-source/usersguide/library/07_testing_validation.rst`
- `docs-source/usersguide/library/05_languages_not_cpp.rst`
- `docs-source/api-c++/forces.rst`
- `docs-source/api-c++/extras.rst`
- `docs-source/usersguide/library/04_platform_specifics.rst`
- `docs-source/usersguide/library/06_integration_examples.rst`
- `docs-source/usersguide/library.rst`
- `docs-source/developerguide/02_core_library.rst`
- `docs-source/usersguide/library/10_drude_plugin.rst`
- `docs-source/api-python/_templates/class.rst`

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
- `wrappers/python/openmm/app/simulation.py`
- `wrappers/python/openmm/__init__.py`
- `wrappers/python/openmm/unit/quantity.py`
- `wrappers/python/openmm/unit/unit_math.py`
- `wrappers/python/src/swig_doxygen/OpenMM.i`
- `wrappers/python/src/swig_doxygen/swig_lib/python/features.i`
- `wrappers/generateWrappers.py`
- `wrappers/python/openmm/testInstallation.py`
- `openmmapi/include/OpenMM.h`
- `openmmapi/src/Context.cpp`
- `openmmapi/src/System.cpp`
- `openmmapi/src/NonbondedForce.cpp`
- `olla/include/openmm/Platform.h`
- `olla/src/Platform.cpp`
- `plugins/drude/openmmapi/src/DrudeForce.cpp`
- `plugins/drude/platforms/reference/src/ReferenceDrudeKernelFactory.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" wrappers openmmapi olla plugins serialization`).
