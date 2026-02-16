# openmm source map: Simulation Workflows

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
- `simulation loop`
- `reporters`
- `checkpoint`
- `state`
- `integrator`
- `annealing`
- `amoeba`
- `rpmd`
- `energy drift`
- `restart`

## Fast source navigation
- `rg -n "Simulation\.|step\(|minimizeEnergy|saveCheckpoint|saveState" wrappers/python/openmm/app`
- `rg -n "Integrator|step\(|setTemperature|setConstraintTolerance" openmmapi/src`
- `rg -n "RPMDIntegrator|Amoeba|Hippo" plugins/rpmd plugins/amoeba`

## Suggested source entry points
- `wrappers/python/openmm/app/simulation.py` | core Python run-control flow, restarts, and context access.
- `wrappers/python/openmm/app/statedatareporter.py` | thermodynamic/kinetic logging behavior.
- `wrappers/python/openmm/app/checkpointreporter.py` | checkpoint emission schedule and file behavior.
- `wrappers/python/openmm/app/pdbreporter.py` | trajectory frame export behavior.
- `wrappers/python/openmm/app/dcdreporter.py` | binary trajectory export behavior.
- `wrappers/python/openmm/app/metadynamics.py` | adaptive bias workflow for advanced runs.
- `openmmapi/src/Context.cpp` | state retrieval and context lifecycle behavior.
- `openmmapi/src/LocalEnergyMinimizer.cpp` | minimization stage behavior before production.
- `openmmapi/src/VerletIntegrator.cpp` | deterministic baseline integrator stepping behavior.
- `openmmapi/src/LangevinMiddleIntegrator.cpp` | stochastic NVT integrator behavior.
- `openmmapi/src/NoseHooverIntegrator.cpp` | thermostat chain behavior and controls.
- `openmmapi/src/VariableVerletIntegrator.cpp` | adaptive-step integrator behavior.
- `plugins/rpmd/openmmapi/src/RPMDIntegrator.cpp` | ring-polymer dynamics stepping and constraints restrictions.
- `plugins/rpmd/openmmapi/src/RPMDMonteCarloBarostat.cpp` | RPMD barostat coupling behavior.
- `plugins/amoeba/openmmapi/src/AmoebaMultipoleForceImpl.cpp` | AMOEBA force workflow behavior.
- `plugins/amoeba/openmmapi/src/HippoNonbondedForceImpl.cpp` | HIPPO nonbonded workflow behavior.
