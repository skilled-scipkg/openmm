# Evidence: openmm-api-and-scripting

## Primary docs
- `examples/README.md`
- `docs-source/api-python/index.rst`
- `docs-source/usersguide/library/07_testing_validation.rst`
- `docs-source/usersguide/library/05_languages_not_cpp.rst`
- `docs-source/api-c++/forces.rst`
- `docs-source/api-c++/extras.rst`
- `docs-source/usersguide/library/04_platform_specifics.rst`
- `docs-source/usersguide/library/06_integration_examples.rst`
- `docs-source/usersguide/library.rst`
- `docs-source/developerguide/02_core_library.rst`
- `docs-source/usersguide/library/10_drude_plugin.rst`
- `docs-source/api-python/_templates/class.rst`

## Primary source entry points
- `skills/openmm-api-and-scripting/references/doc_map.md`
- `plugins/drude/platforms/common/src/CommonDrudeKernelSources.cpp.in`
- `plugins/drude/platforms/reference/src/ReferenceDrudeKernels.cpp`
- `plugins/drude/platforms/reference/src/ReferenceDrudeKernelFactory.cpp`
- `plugins/drude/platforms/opencl/src/OpenCLDrudeKernelFactory.cpp`
- `plugins/drude/platforms/hip/src/HipDrudeKernelFactory.cpp`
- `plugins/drude/platforms/cuda/src/CudaDrudeKernelFactory.cpp`
- `plugins/drude/platforms/common/src/CommonDrudeKernels.cpp`
- `plugins/drude/serialization/src/DrudeSerializationProxyRegistration.cpp`
- `plugins/drude/serialization/src/DrudeNoseHooverIntegratorProxy.cpp`
- `plugins/drude/serialization/src/DrudeLangevinIntegratorProxy.cpp`
- `plugins/drude/serialization/src/DrudeForceProxy.cpp`
- `plugins/drude/openmmapi/src/DrudeSCFIntegrator.cpp`
- `plugins/drude/openmmapi/src/DrudeNoseHooverIntegrator.cpp`
- `plugins/drude/openmmapi/src/DrudeLangevinIntegrator.cpp`
- `plugins/drude/openmmapi/src/DrudeIntegrator.cpp`
- `plugins/drude/openmmapi/src/DrudeHelpers.cpp`
- `plugins/drude/openmmapi/src/DrudeForceImpl.cpp`
- `plugins/drude/openmmapi/src/DrudeForce.cpp`
- `olla/src/Platform.cpp`

## Extracted headings
- OpenMM Examples
- Python API examples
- C++ API examples
- Extras
- construct a Quantity using the multiply operator
- equivalently using the explicit Quantity constructor
- or more verbosely
- or, equivalently
- or

## Executable command hints
- Python with no substantial conceptual changes. We have developed a
- Python API

## Warnings and pitfalls
- suite took to execute.  Otherwise it prints an error message.  If any tests
- These simulations were designed to minimize all sources of error except those
- inherent in OpenMM.  There are other sources of error that may be significant in
- * Using a larger time step increases the integration error (roughly
- * If a system involves constraints, the level of error will depend strongly on
- strongly on the Ewald error tolerance.
- error, and the shorter the cutoff is, the greater the error will be.
- 1 nm cutoff on direct space interactions.  For OpenMM, the Ewald error tolerance
- course, but all the important concepts remain unchanged.
- the APIs are likely to be error-free and are always available immediately when
- respectively.  When using the C++ API, it is very important to ensure that
- x = 5.0*dalton + 4.3*nanometer; # error
