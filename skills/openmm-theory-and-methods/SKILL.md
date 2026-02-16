---
name: openmm-theory-and-methods
description: This skill should be used when users ask about theory and methods in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Theory and Methods

## High-Signal Playbook
### Route Conditions
- Use this skill for force-form derivations, custom-force semantics, and method-level reasoning about integrators/constraints/nonbonded formulations (`docs-source/usersguide/theory/02_standard_forces.rst`, `docs-source/usersguide/theory/03_custom_forces.rst`).
- Route model-construction and input-file mechanics to `openmm-inputs-and-modeling`.
- Route simulation protocol execution details to `openmm-simulation-workflows`.
- Route wrapper/API usage mechanics to `openmm-api-and-scripting`.

### Triage Questions
- Is the question about a standard built-in force or a custom expression-based force?
- Do you need symbolic interpretation, implementation behavior, or numerical validation guidance?
- Which observables must match across methods (energy, forces, drift, ensemble averages)?
- Are you comparing two mathematically equivalent formulations in code?

### Canonical Workflow
1. Start from theory docs to establish expected equations and assumptions.
2. Map equations to API objects (`Custom*Force`, `NonbondedForce`, `CustomIntegrator`, etc.).
3. Build a minimal reproducible system where only the target term is active.
4. Compare numerical outputs (energy/force) against analytical or baseline implementation expectations.
5. If discrepancy remains, inspect corresponding implementation and serialization paths.

### Minimal Working Example
```python
# Practical theory sanity check pattern:
# 1) Build tiny two-particle system.
# 2) Add a standard force and an equivalent custom force in separate runs.
# 3) Compare energies and forces at fixed coordinates.
```

### Pitfalls and Fixes
- Problem: interpreting custom expressions without confirming parameter scope. Fix: verify global vs per-particle/per-bond parameter definitions.
- Problem: comparing methods with mismatched cutoff/constraint/precision settings. Fix: align numerical knobs before drawing theory conclusions.
- Problem: assuming serialized XML mismatch is purely numerical. Fix: inspect proxy serialization classes for dropped settings.
- Problem: attributing instability to force form when integrator settings dominate error. Fix: isolate integrator effects in separate tests.

### Convergence and Validation Checks
- Use fixed coordinates to compare pure energy/force evaluation first.
- Run short trajectories to detect drift trends only after static checks pass.
- Re-check in multiple precision modes when differences are near tolerance.
- Verify serialization round-trip preserves all custom force parameters.

## Scope
- Handle questions about theoretical background and algorithmic methods.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs-source/usersguide/index.rst`
- `docs-source/usersguide/theory/03_custom_forces.rst`
- `docs-source/usersguide/theory/02_standard_forces.rst`
- `docs-source/usersguide/theory.rst`

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
- `openmmapi/src/HarmonicBondForce.cpp`
- `openmmapi/src/HarmonicAngleForce.cpp`
- `openmmapi/src/NonbondedForce.cpp`
- `openmmapi/src/CustomBondForce.cpp`
- `openmmapi/src/CustomBondForceImpl.cpp`
- `openmmapi/src/CustomAngleForce.cpp`
- `openmmapi/src/CustomAngleForceImpl.cpp`
- `openmmapi/src/CustomNonbondedForce.cpp`
- `openmmapi/src/CustomNonbondedForceImpl.cpp`
- `openmmapi/src/CustomManyParticleForce.cpp`
- `openmmapi/src/CustomIntegrator.cpp`
- `openmmapi/src/CompiledExpressionSet.cpp`
- `wrappers/python/openmm/app/internal/customgbforces.py`
- `serialization/src/CustomNonbondedForceProxy.cpp`
- `serialization/src/CustomIntegratorProxy.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" openmmapi/src serialization/src wrappers/python/openmm/app/internal`).
