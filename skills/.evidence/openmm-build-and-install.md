# Evidence: openmm-build-and-install

## Primary docs
- `examples/cpp-examples/README.md`
- `examples/cpp-examples/CMakeLists.txt`
- `platforms/opencl/tests/CMakeLists.txt`
- `docs-source/usersguide/library/02_compiling.rst`
- `docs-source/usersguide/application/03_model_building_editing.rst`
- `tests/CMakeLists.txt`
- `docs-source/CMakeLists.txt`
- `examples/CMakeLists.txt`
- `serialization/tests/CMakeLists.txt`
- `examples/python-examples/CMakeLists.txt`
- `plugins/cpupme/tests/CMakeLists.txt`
- `platforms/reference/tests/CMakeLists.txt`

## Primary source entry points
- `skills/openmm-build-and-install/references/doc_map.md`
- `plugins/rpmd/platforms/reference/CMakeLists.txt`
- `plugins/rpmd/platforms/opencl/CMakeLists.txt`
- `plugins/rpmd/platforms/hip/CMakeLists.txt`
- `plugins/rpmd/platforms/cuda/CMakeLists.txt`
- `plugins/drude/platforms/reference/CMakeLists.txt`
- `plugins/drude/platforms/opencl/CMakeLists.txt`
- `plugins/drude/platforms/hip/CMakeLists.txt`
- `plugins/drude/platforms/cuda/CMakeLists.txt`
- `plugins/amoeba/platforms/reference/CMakeLists.txt`
- `plugins/amoeba/platforms/opencl/CMakeLists.txt`
- `plugins/amoeba/platforms/hip/CMakeLists.txt`
- `plugins/amoeba/platforms/cuda/CMakeLists.txt`
- `plugins/rpmd/platforms/common/CMakeLists.txt`
- `plugins/drude/platforms/common/CMakeLists.txt`
- `plugins/amoeba/platforms/common/CMakeLists.txt`
- `plugins/cpupme/CMakeLists.txt`
- `plugins/rpmd/CMakeLists.txt`
- `plugins/drude/CMakeLists.txt`
- `plugins/amoeba/CMakeLists.txt`

## Extracted headings
- OpenMM C++, C, and Fortran API Examples
- Example Details
- Building the examples
- Generate and install C++, C, and Fortran examples.
- This is boilerplate code for generating a set of executables, one per
- .cpp file in the "cpp-examples" subdirectory.
- For IDEs that can deal with PROJECT_LABEL properties (at least
- Visual Studio) the projects for building each of these adhoc
- executables will be labeled "Example - TheExampleName" if a file
- TheExampleName.cpp is found in this directory.
- We check the BUILD_TESTING_{SHARED,STATIC} variables to determine
- whether to build dynamically linked, statically linked, or both

## Executable command hints
- $ export LD_LIBRARY_PATH=/usr/local/openmm/lib
- $ export DYLD_LIBRARY_PATH=/usr/local/openmm/lib
- ./TestReferenceLangevinIntegrator
- python -m openmm.testInstallation

## Warnings and pitfalls
- Configure (press “c”) again.  Adjust any variables that cause an error.
- can run them individually to get more detailed error information.  For example,
- fraction of the time.  These tests will say so in the error message:
- Press "Configure" again.  Adjust any variables that cause an error.
- can run them individually to get more detailed error information.  Right-click
