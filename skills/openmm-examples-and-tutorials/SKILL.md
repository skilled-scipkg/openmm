---
name: openmm-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in openmm; it prioritizes documentation references and then source inspection only for unresolved details.
---

# openmm: Examples and Tutorials

## High-Signal Playbook
### Route Conditions
- Use this skill for runnable example selection, adapting tutorial scripts, and validating first production-like runs from known-good templates (`examples/README.md`, `examples/cpp-examples/README.md`, `docs-source/usersguide/library/03_tutorials.rst`).
- Route package/runtime installation issues to `openmm-getting-started` or `openmm-build-and-install`.
- Route force-field/model-construction questions to `openmm-inputs-and-modeling`.
- Route deeper integrator/restart/reporter strategy to `openmm-simulation-workflows`.

### Triage Questions
- Do you need Python app-layer examples or C++ API examples? (`examples/README.md`, `examples/cpp-examples/README.md`)
- Which input format are you starting from: PDB, AMBER, CHARMM, GROMACS, or TINKER? (`examples/python-examples/simulatePdb.py`, `examples/python-examples/simulateAmber.py`, `examples/python-examples/simulateCharmm.py`, `examples/python-examples/simulateGromacs.py`, `examples/python-examples/simulateTinker.py`)
- Is the goal a smoke test, a benchmark, or a template for production protocol development? (`examples/cpp-examples/HelloArgon.cpp`, `examples/benchmarks/benchmark.py`)
- Which outputs are required immediately (state log, trajectory, checkpoint, final structure)? (`wrappers/python/openmm/app/statedatareporter.py`, `wrappers/python/openmm/app/pdbreporter.py`)

### Canonical Workflow
1. Pick the closest example by input type and simulation goal (`examples/README.md`).
2. Run the example unchanged first to establish a known-good baseline.
3. Swap in your own structure/topology/parameter inputs while preserving reporter cadence.
4. Add checkpoints and at least one trajectory/reporter output for validation.
5. Validate platform selection, energy stability, and output file integrity before scaling.

### Minimal Working Example
```bash
python examples/python-examples/simulatePdb.py
python examples/python-examples/simulateAmber.py

cd examples/cpp-examples
make
./HelloArgon > argon.pdb
```

### Pitfalls and Fixes
- Problem: editing too many knobs before first run. Fix: run baseline script unchanged, then modify one dimension at a time.
- Problem: replacing topology but not matching coordinate/parameter files. Fix: keep input families consistent (for example AMBER prmtop+inpcrd).
- Problem: example appears to run but no useful diagnostics are saved. Fix: add `StateDataReporter` and a trajectory reporter early.
- Problem: assuming benchmark scripts are protocol templates. Fix: treat benchmark defaults as performance probes, not production defaults.

### Convergence and Validation Checks
- Confirm first output line reports the expected platform for the run path (`examples/cpp-examples/README.md`).
- Confirm output artifacts exist and are non-empty (for example `output.pdb`, DCD, CSV log).
- Check short-run potential energy and temperature traces for obvious blow-up before long production runs.
- Re-run with a different platform or precision mode when behavior looks suspicious.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `examples/README.md`
- `examples/cpp-examples/README.md`
- `examples/extras/README.md`
- `docs-source/usersguide/library/03_tutorials.rst`
- `docs-source/usersguide/application/02_running_sims.rst`

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
- `examples/README.md`
- `examples/cpp-examples/README.md`
- `examples/cpp-examples/HelloArgon.cpp`
- `examples/cpp-examples/HelloSodiumChloride.cpp`
- `examples/cpp-examples/HelloWaterBox.cpp`
- `examples/python-examples/simulatePdb.py`
- `examples/python-examples/simulateAmber.py`
- `examples/python-examples/simulateCharmm.py`
- `examples/python-examples/simulateGromacs.py`
- `examples/python-examples/simulateTinker.py`
- `examples/benchmarks/benchmark.py`
- `examples/extras/optimizepme.py`
- `wrappers/python/openmm/app/simulation.py`
- `wrappers/python/openmm/app/statedatareporter.py`
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" examples wrappers/python/openmm/app openmmapi`).
