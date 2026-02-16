---
name: openmm-index
description: This skill should be used when users ask how to use openmm and the correct generated documentation skill must be selected before going deeper into source code.
---

# openmm Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer workflow-level guidance first; escalate to function-level source checks only when docs are insufficient.

## Quick Launch From `skills/`
1. Start with `openmm-getting-started` to verify install/runtime path.
2. Move to `openmm-inputs-and-modeling` to prepare the system and force field.
3. Continue with `openmm-simulation-workflows` for run control, reporters, and restart strategy.
4. Use `openmm-api-and-scripting` only for wrapper/API semantics and `openmm-developer-guide` for internals/plugin work.

### Minimum smoke-test commands
```bash
python -m openmm.testInstallation
python examples/python-examples/simulatePdb.py
cd examples/cpp-examples && make && ./HelloArgon > argon.pdb
```

### Minimum validation checkpoints
- `python -m openmm.testInstallation` reports expected available platforms.
- Python example runs and writes expected outputs/logs.
- `HelloArgon` writes `argon.pdb` and prints platform banner.

## Generated topic skills
- `openmm-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `openmm-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `openmm-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `openmm-developer-guide`: Developer Guide (developer architecture, extension points, and contribution workflow)
- `openmm-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `openmm-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `openmm-theory-and-methods`: Theory and Methods (theoretical background and algorithmic methods)
- `openmm-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `openmm-docs-source`: Docs Source (documentation grouped under the `docs-source` theme)

## Documentation-first inputs
- `docs-source`

## Tutorials and examples roots
- `examples`

## Test roots for behavior checks
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

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, inspect this skill's `references/doc_map.md`.
- If documentation still leaves ambiguity, inspect this skill's `references/source_map.md`.
- Use targeted symbol search during source inspection (for example: `rg -n "<symbol_or_keyword>" libraries olla openmmapi platforms plugins serialization wrappers`).

## Source directories for deeper inspection
- `libraries`
- `olla`
- `openmmapi`
- `platforms`
- `plugins`
- `serialization`
- `wrappers`
