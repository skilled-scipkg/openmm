---
name: openmm-simulation-workflows
description: This skill should be used when users ask about simulation workflows in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Simulation Workflows

## High-Signal Playbook
### Route Conditions
- Use this skill for end-to-end run control: setup-to-step loops, reporters, checkpoints/states, integrator choices, and advanced workflows (annealing, external forces, RPMD/AMOEBA) (`docs-source/usersguide/application/04_advanced_sim_examples.rst`, `docs-source/usersguide/theory/04_integrators.rst`, `docs-source/usersguide/library/09_rpmd_plugin.rst`, `docs-source/usersguide/library/08_amoeba_plugin.rst`).
- Route force-field/input construction questions to `openmm-inputs-and-modeling`.
- Route wrapper/language API mapping to `openmm-api-and-scripting`.
- Route plugin authoring and low-level kernels to `openmm-developer-guide`.

### Triage Questions
- What simulation class is this: classical MD, AMOEBA polarizable, or RPMD? (`docs-source/usersguide/library/08_amoeba_plugin.rst`, `docs-source/usersguide/library/09_rpmd_plugin.rst`)
- Which ensemble/integrator is required (Verlet, LangevinMiddle, NoseHoover, variable-step)? (`docs-source/usersguide/theory/04_integrators.rst`)
- Do you need exact restart continuity (`checkpoint`) or portable restart (`state`)? (`wrappers/python/openmm/app/simulation.py`)
- Are you adding new forces before `Simulation` creation, or trying to modify `System` after initialization? (`docs-source/usersguide/application/04_advanced_sim_examples.rst`)
- Which observables must be reported: positions, energies, forces, parameters? (`docs-source/usersguide/application/04_advanced_sim_examples.rst`, `wrappers/python/openmm/app/simulation.py`)
- For RPMD, how many beads and contractions are required for the target temperature/system? (`docs-source/usersguide/library/09_rpmd_plugin.rst`)

### Canonical Workflow
1. Build `System` and select integrator based on ensemble/accuracy goals (`docs-source/usersguide/theory/04_integrators.rst`).
2. Add all required forces before creating `Simulation` (`docs-source/usersguide/application/04_advanced_sim_examples.rst`).
3. Create `Simulation`, set positions, then minimize/equilibrate (`docs-source/usersguide/application/04_advanced_sim_examples.rst`, `wrappers/python/openmm/app/simulation.py`).
4. Attach reporters for required outputs; include force/energy reporters where needed (`docs-source/usersguide/application/04_advanced_sim_examples.rst`).
5. Run production steps or wall-clock bounded runs; emit checkpoints/states on interval (`wrappers/python/openmm/app/simulation.py`).
6. Validate energy/drift/force behavior and rerun with tighter knobs if needed (`docs-source/usersguide/library/07_testing_validation.rst`).

### Minimal Working Example
```python
from openmm.app import StateDataReporter

simulation.context.setPositions(pdb.positions)
simulation.minimizeEnergy()
for i in range(100):
    integrator.setTemperature(3 * (100 - i) * kelvin)
    simulation.step(1000)

simulation.reporters.append(
    StateDataReporter("log.csv", 1000, step=True, temperature=True, potentialEnergy=True)
)
simulation.saveCheckpoint("prod.chk")
simulation.saveState("prod_state.xml")
```

### Pitfalls and Fixes
- Problem: adding/modifying forces after `Simulation` is created has no effect. Fix: finalize `System` first (`docs-source/usersguide/application/04_advanced_sim_examples.rst`).
- Problem: assuming checkpoint files are portable. Fix: use `saveState()` for portability; use checkpoints for exact continuation on same platform/hardware (`wrappers/python/openmm/app/simulation.py`).
- Problem: misleading total energy from half-step velocity integrators. Fix: follow integrator-specific energy interpretation guidance (`docs-source/usersguide/theory/04_integrators.rst`).
- Problem: unstable/drifting trajectories from aggressive timestep. Fix: reduce `dt`; drift scales roughly with `dt^2` (`docs-source/usersguide/library/07_testing_validation.rst`).
- Problem: constraints/PME settings silently degrade accuracy. Fix: tune constraint tolerance and Ewald tolerance explicitly (`docs-source/usersguide/library/07_testing_validation.rst`).
- Problem: RPMD used with constrained system. Fix: `RPMDIntegrator` rejects constrained systems; remove constraints or switch method (`plugins/rpmd/openmmapi/src/RPMDIntegrator.cpp`).

### Convergence and Validation Checks
- Sweep timestep first; then re-check with tighter constraints and PME error tolerance (`docs-source/usersguide/library/07_testing_validation.rst`).
- Compare precision modes (`single`/`mixed`/`double`) when drift or reproducibility is suspect (`docs-source/usersguide/library/04_platform_specifics.rst`, `docs-source/usersguide/library/07_testing_validation.rst`).
- Validate reporter/state cadence by restoring from produced restart artifacts and checking continuity (`wrappers/python/openmm/app/simulation.py`).
- For RPMD, converge bead count with `n > ħωmax/(kBT)` and verify contraction choices do not bias observables (`docs-source/usersguide/library/09_rpmd_plugin.rst`).

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs-source/api-c++/index.rst`
- `docs-source/api-c++/integrators.rst`
- `docs-source/usersguide/theory/04_integrators.rst`
- `docs-source/usersguide/library/08_amoeba_plugin.rst`
- `docs-source/usersguide/application/04_advanced_sim_examples.rst`
- `docs-source/usersguide/library/09_rpmd_plugin.rst`

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
- `wrappers/python/openmm/app/checkpointreporter.py`
- `wrappers/python/openmm/app/statedatareporter.py`
- `wrappers/python/openmm/app/pdbreporter.py`
- `wrappers/python/openmm/app/dcdreporter.py`
- `wrappers/python/openmm/app/metadynamics.py`
- `openmmapi/src/Context.cpp`
- `openmmapi/src/LocalEnergyMinimizer.cpp`
- `openmmapi/src/VerletIntegrator.cpp`
- `openmmapi/src/LangevinMiddleIntegrator.cpp`
- `openmmapi/src/NoseHooverIntegrator.cpp`
- `openmmapi/src/VariableVerletIntegrator.cpp`
- `plugins/rpmd/openmmapi/src/RPMDIntegrator.cpp`
- `plugins/rpmd/openmmapi/src/RPMDMonteCarloBarostat.cpp`
- `plugins/amoeba/openmmapi/src/AmoebaMultipoleForceImpl.cpp`
- `plugins/amoeba/openmmapi/src/HippoNonbondedForceImpl.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" wrappers/python/openmm/app openmmapi/src plugins/rpmd plugins/amoeba`).
