---
name: openmm-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Inputs and Modeling

## High-Signal Playbook
### Route Conditions
- Use this skill for preparing topology/coordinates, force-field selection, and model-editing steps before production simulation (`docs-source/usersguide/application/02_running_sims.rst`, `docs-source/usersguide/application/06_creating_ffs.rst`).
- Route install/toolchain problems to `openmm-build-and-install`.
- Route runtime protocol control (reporters, restart cadence, integrator scheduling) to `openmm-simulation-workflows`.
- Route advanced theoretical method questions to `openmm-theory-and-methods`.

### Triage Questions
- What input ecosystem are you using: PDB/mmCIF, AMBER, CHARMM, GROMACS, or TINKER? (`wrappers/python/openmm/app/pdbfile.py`, `wrappers/python/openmm/app/amberprmtopfile.py`, `wrappers/python/openmm/app/charmmpsffile.py`, `wrappers/python/openmm/app/gromacstopfile.py`)
- Are you building a model from scratch, editing an existing structure, or only converting file formats? (`wrappers/python/openmm/app/modeller.py`)
- Which force field family is required and do you need custom XML terms? (`wrappers/python/openmm/app/forcefield.py`, `docs-source/usersguide/application/06_creating_ffs.rst`)
- Are periodic box vectors, constraints, cutoff method, and water model already defined? (`docs-source/usersguide/theory/05_other_features.rst`)

### Canonical Workflow
1. Load structure/topology with the matching loader for the source format.
2. Choose a force-field stack and construct the `System` with explicit nonbonded/constraint settings.
3. Use `Modeller` to add missing hydrogens/solvent or perform local edits.
4. Minimize before dynamics and confirm no obvious geometry or parameterization issues.
5. Validate system composition (particle count, force count, box vectors, constraints) before long trajectories.

### Minimal Working Example
```python
from openmm.app import PDBFile, ForceField, Modeller
from openmm import LangevinMiddleIntegrator
from openmm.unit import kelvin, picosecond, nanometer

pdb = PDBFile("input.pdb")
modeller = Modeller(pdb.topology, pdb.positions)
forcefield = ForceField("amber14-all.xml", "amber14/tip3pfb.xml")
modeller.addHydrogens(forcefield)
system = forcefield.createSystem(
    modeller.topology,
    nonbondedMethod=1,  # CutoffNonPeriodic in script contexts
    nonbondedCutoff=1.0*nanometer,
    constraints=None,
)
integrator = LangevinMiddleIntegrator(300*kelvin, 1/picosecond, 0.004*picosecond)
```

### Pitfalls and Fixes
- Problem: mixing topology and coordinates from different preparation states. Fix: regenerate topology+positions together after edits.
- Problem: using force-field XML that does not match residue/atom naming in input files. Fix: normalize naming or provide matching template patches.
- Problem: forgetting periodic box vectors for condensed-phase systems. Fix: validate box vectors before creating the `System`.
- Problem: applying aggressive constraints/cutoffs without checking stability. Fix: start conservative, then tune.

### Convergence and Validation Checks
- Confirm total particle and residue counts match expectations after `Modeller` operations.
- Confirm all residues are parameterized (no missing templates during `createSystem`).
- Run short minimization and a short dynamics smoke test before full production.
- Verify nonbonded method, cutoff, and constraints are logged and match protocol intent.

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs-source/usersguide/application/06_creating_ffs.rst`
- `docs-source/usersguide/application/02_running_sims.rst`
- `docs-source/usersguide/theory/05_other_features.rst`
- `docs-source/usersguide/application/05_add_on_packages.rst`

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
- `wrappers/python/openmm/app/forcefield.py`
- `wrappers/python/openmm/app/modeller.py`
- `wrappers/python/openmm/app/topology.py`
- `wrappers/python/openmm/app/pdbfile.py`
- `wrappers/python/openmm/app/pdbxfile.py`
- `wrappers/python/openmm/app/amberprmtopfile.py`
- `wrappers/python/openmm/app/amberinpcrdfile.py`
- `wrappers/python/openmm/app/charmmpsffile.py`
- `wrappers/python/openmm/app/charmmparameterset.py`
- `wrappers/python/openmm/app/gromacstopfile.py`
- `wrappers/python/openmm/app/gromacsgrofile.py`
- `wrappers/python/openmm/app/internal/pdbstructure.py`
- `wrappers/python/openmm/app/internal/amber_file_parser.py`
- `openmmapi/src/System.cpp`
- `openmmapi/src/NonbondedForce.cpp`
- `openmmapi/src/LocalEnergyMinimizer.cpp`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" wrappers/python/openmm/app openmmapi/src`).
