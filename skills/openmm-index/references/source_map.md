# openmm source map: Skills Index

Generated from source roots:
- `skills`
- `examples`
- `wrappers`
- `openmmapi`
- `olla`
- `platforms`

Use this map only after exhausting the index docs in `doc_map.md`.

## Topic query tokens
- `first run`
- `routing`
- `skill selection`
- `smoke test`
- `model setup`
- `simulation control`
- `validation`

## Fast source navigation
- `rg -n "High-Signal Playbook|Canonical Workflow|Convergence and Validation Checks" skills/openmm-*/SKILL.md`
- `rg -n "testInstallation|HelloArgon|simulatePdb" wrappers/python/openmm examples`
- `rg -n "Simulation\.|createSystem\(|Platform::" wrappers/python/openmm openmmapi olla`

## Suggested source entry points
- `skills/openmm-getting-started/SKILL.md` | first stop for installation and smoke-test flow.
- `skills/openmm-inputs-and-modeling/SKILL.md` | model and force-field preparation flow.
- `skills/openmm-simulation-workflows/SKILL.md` | production run control, checkpoints, reporters.
- `skills/openmm-api-and-scripting/SKILL.md` | API and wrapper semantics.
- `skills/openmm-build-and-install/SKILL.md` | source builds and environment/toolchain issues.
- `skills/openmm-theory-and-methods/SKILL.md` | algorithmic and force-form reasoning.
- `skills/openmm-examples-and-tutorials/SKILL.md` | runnable templates and adaptation path.
- `wrappers/python/openmm/testInstallation.py` | installation validation logic.
- `examples/cpp-examples/HelloArgon.cpp` | minimal compiled simulation path.
- `examples/python-examples/simulatePdb.py` | minimal Python simulation path.
- `wrappers/python/openmm/app/forcefield.py` | force-field-driven `System` construction behavior.
- `wrappers/python/openmm/app/simulation.py` | runtime stepping, state, and checkpoint behavior.
- `openmmapi/src/System.cpp` | core system object behavior.
- `openmmapi/src/Context.cpp` | context and state lifecycle behavior.
- `olla/src/Platform.cpp` | platform discovery and plugin loading behavior.
