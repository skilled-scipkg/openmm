# openmm source map: Inputs and Modeling

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
- `forcefield`
- `topology`
- `modeller`
- `pdb`
- `amber`
- `charmm`
- `gromacs`
- `minimization`
- `constraints`
- `nonbonded`

## Fast source navigation
- `rg -n "createSystem\(|addHydrogens|addSolvent|setDefaultPeriodicBoxVectors" wrappers/python/openmm/app`
- `rg -n "ForceField|Topology|PDBFile|AmberPrmtopFile|CharmmPsfFile|GromacsTopFile" wrappers/python/openmm/app`
- `rg -n "LocalEnergyMinimizer|System::|NonbondedForce" openmmapi/src`

## Suggested source entry points
- `wrappers/python/openmm/app/forcefield.py` | force field XML parsing and `createSystem()` implementation.
- `wrappers/python/openmm/app/modeller.py` | model editing (`addHydrogens`, `addSolvent`) and topology updates.
- `wrappers/python/openmm/app/topology.py` | topology graph representation used by all loaders.
- `wrappers/python/openmm/app/pdbfile.py` | PDB parsing and coordinate/topology extraction.
- `wrappers/python/openmm/app/pdbxfile.py` | mmCIF parsing and topology loading.
- `wrappers/python/openmm/app/amberprmtopfile.py` | AMBER topology to `System` conversion.
- `wrappers/python/openmm/app/amberinpcrdfile.py` | AMBER coordinate loading behavior.
- `wrappers/python/openmm/app/charmmpsffile.py` | CHARMM PSF to `System` conversion.
- `wrappers/python/openmm/app/charmmparameterset.py` | CHARMM parameter loading and assignment.
- `wrappers/python/openmm/app/gromacstopfile.py` | GROMACS topology conversion behavior.
- `wrappers/python/openmm/app/gromacsgrofile.py` | GROMACS coordinate and box parsing.
- `wrappers/python/openmm/app/internal/pdbstructure.py` | low-level PDB structure object behavior.
- `wrappers/python/openmm/app/internal/amber_file_parser.py` | AMBER file parsing internals.
- `openmmapi/src/System.cpp` | force container semantics and particle metadata behavior.
- `openmmapi/src/NonbondedForce.cpp` | nonbonded parameter and cutoff setup behavior.
- `openmmapi/src/LocalEnergyMinimizer.cpp` | minimization convergence and tolerance controls.
