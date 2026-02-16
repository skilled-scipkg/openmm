# openmm source map: API and Scripting

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
- `python`
- `c-api`
- `wrappers`
- `units`
- `platform properties`
- `context`
- `state`
- `serialization`
- `integration`
- `drude`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" wrappers openmmapi olla plugins serialization`
- `rg -n "class |def |struct |namespace " wrappers openmmapi olla plugins serialization`
- Check call chains from wrapper API -> C++ API -> platform implementation before assuming binding bugs.

## Suggested source entry points
- `wrappers/python/openmm/__init__.py` | module exports and high-level API surface.
- `wrappers/python/openmm/app/simulation.py` | `Simulation` construction, `step()`, checkpoints, and state save/load behavior.
- `wrappers/python/openmm/unit/quantity.py` | unit-bearing arithmetic and conversion behavior.
- `wrappers/python/openmm/unit/unit_math.py` | quantity-safe math helpers.
- `wrappers/python/src/swig_doxygen/OpenMM.i` | SWIG interface definitions for Python/C wrapper exposure.
- `wrappers/python/src/swig_doxygen/swig_lib/python/features.i` | generated Python wrapper feature flags.
- `wrappers/generateWrappers.py` | wrapper generation workflow and symbol mapping.
- `wrappers/python/openmm/testInstallation.py` | runtime platform checks and smoke validation logic.
- `openmmapi/include/OpenMM.h` | umbrella API include and public class exposure.
- `openmmapi/src/Context.cpp` | context lifecycle, platform selection, and state retrieval.
- `openmmapi/src/System.cpp` | system composition and force ownership behavior.
- `openmmapi/src/NonbondedForce.cpp` | nonbonded API parameters and consistency checks.
- `olla/include/openmm/Platform.h` | platform properties API and plugin load interfaces.
- `olla/src/Platform.cpp` | platform registry and plugin loading behavior.
- `plugins/drude/openmmapi/src/DrudeForce.cpp` | plugin-level API behavior for Drude force classes.
