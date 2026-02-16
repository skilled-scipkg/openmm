# openmm source map: Examples and Tutorials

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
- `simulatePdb`
- `simulateAmber`
- `simulateCharmm`
- `simulateGromacs`
- `HelloArgon`
- `reporters`
- `benchmark`
- `extras`

## Fast source navigation
- `rg -n "Simulation\(|createSystem\(|StateDataReporter|minimizeEnergy" examples wrappers/python/openmm/app`
- `rg -n "HelloArgon|HelloWaterBox|HelloSodiumChloride" examples/cpp-examples`
- `rg -n "benchmark|optimizepme|rigid" examples`

## Suggested source entry points
- `examples/README.md` | top-level example index and usage routes.
- `examples/cpp-examples/README.md` | C++ tutorial flow and expected runtime output.
- `examples/cpp-examples/HelloArgon.cpp` | minimal C++ simulation flow and platform banner.
- `examples/cpp-examples/HelloSodiumChloride.cpp` | PME/nonbonded setup example.
- `examples/cpp-examples/HelloWaterBox.cpp` | water box setup and integration loop.
- `examples/python-examples/simulatePdb.py` | canonical Python app-layer setup pipeline.
- `examples/python-examples/simulateAmber.py` | AMBER input workflow.
- `examples/python-examples/simulateCharmm.py` | CHARMM input workflow.
- `examples/python-examples/simulateGromacs.py` | GROMACS input workflow.
- `examples/python-examples/simulateTinker.py` | TINKER input workflow.
- `examples/benchmarks/benchmark.py` | reproducible benchmark harness and platform toggles.
- `examples/extras/optimizepme.py` | PME tuning workflow for production readiness.
- `examples/extras/rigid.py` | rigid-body manipulation utilities for setup debugging.
- `wrappers/python/openmm/app/simulation.py` | shared runtime behavior used by Python examples.
- `wrappers/python/openmm/app/statedatareporter.py` | reporter output fields and sampling behavior.
