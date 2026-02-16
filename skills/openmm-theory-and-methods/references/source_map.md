# openmm source map: Theory and Methods

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
- `standard forces`
- `custom forces`
- `expression parsing`
- `integrator formalism`
- `constraints`
- `nonbonded methods`
- `serialization`

## Fast source navigation
- `rg -n "Custom.*Force|NonbondedForce|HarmonicBondForce|HarmonicAngleForce" openmmapi/src`
- `rg -n "CustomIntegrator|CompiledExpressionSet" openmmapi/src`
- `rg -n "Custom.*Proxy" serialization/src`

## Suggested source entry points
- `openmmapi/src/HarmonicBondForce.cpp` | standard bonded force functional form and parameter behavior.
- `openmmapi/src/HarmonicAngleForce.cpp` | standard angular force functional form and parameter behavior.
- `openmmapi/src/NonbondedForce.cpp` | electrostatics/LJ method settings and cutoff/Ewald controls.
- `openmmapi/src/CustomBondForce.cpp` | custom bonded expression parsing and parameter handling.
- `openmmapi/src/CustomBondForceImpl.cpp` | custom bonded kernel interface behavior.
- `openmmapi/src/CustomAngleForce.cpp` | custom angle expression parsing behavior.
- `openmmapi/src/CustomAngleForceImpl.cpp` | custom angle kernel interface behavior.
- `openmmapi/src/CustomNonbondedForce.cpp` | custom nonbonded expression and exclusion behavior.
- `openmmapi/src/CustomNonbondedForceImpl.cpp` | custom nonbonded implementation details.
- `openmmapi/src/CustomManyParticleForce.cpp` | many-particle custom method behavior.
- `openmmapi/src/CustomIntegrator.cpp` | custom integrator stepping semantics.
- `openmmapi/src/CompiledExpressionSet.cpp` | symbolic expression compilation path.
- `wrappers/python/openmm/app/internal/customgbforces.py` | Python-side custom GB helper expressions.
- `serialization/src/CustomNonbondedForceProxy.cpp` | serialization format for custom nonbonded forces.
- `serialization/src/CustomIntegratorProxy.cpp` | serialization format for custom integrators.
