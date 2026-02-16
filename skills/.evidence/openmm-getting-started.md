# Evidence: openmm-getting-started

## Primary docs
- `docs-source/usersguide/introduction.rst`
- `docs-source/developerguide/06_opencl_platform.rst`
- `docs-source/usersguide/library/03_tutorials.rst`
- `docs-source/usersguide/library/01_introduction.rst`
- `docs-source/usersguide/theory/01_introduction.rst`
- `docs-source/usersguide/application/01_getting_started.rst`
- `docs-source/developerguide/01_introduction.rst`

## Primary source entry points
- `skills/openmm-getting-started/references/doc_map.md`
- `platforms/opencl/src/OpenCLKernelSources.h.in`
- `platforms/opencl/src/OpenCLKernelSources.cpp.in`
- `platforms/opencl/CMakeLists.txt`
- `platforms/opencl/staticTarget/CMakeLists.txt`
- `platforms/opencl/src/OpenCLSort.cpp`
- `platforms/opencl/src/OpenCLProgram.cpp`
- `platforms/opencl/src/OpenCLPlatform.cpp`
- `platforms/opencl/src/OpenCLParallelKernels.cpp`
- `platforms/opencl/src/OpenCLNonbondedUtilities.cpp`
- `platforms/opencl/src/OpenCLKernels.cpp`
- `platforms/opencl/src/OpenCLKernelFactory.cpp`
- `platforms/opencl/src/OpenCLKernel.cpp`
- `platforms/opencl/src/OpenCLIntegrationUtilities.cpp`
- `platforms/opencl/src/OpenCLFFT3D.cpp`
- `platforms/opencl/src/OpenCLEvent.cpp`
- `platforms/opencl/src/OpenCLContext.cpp`
- `platforms/opencl/src/OpenCLCompact.cpp`
- `platforms/opencl/src/OpenCLArray.cpp`
- `platforms/opencl/src/opencl.hpp`

## Extracted headings
- (none extracted)

## Executable command hints
- ./HelloArgon
- ./HelloArgon > argon.pdb
- Python programming language.  Those libraries can easily be chained together to
- python -m openmm.testInstallation

## Warnings and pitfalls
- to use some of the most important ones.  It will *not* teach you how to
- OpenCLPlatform.h.  The most important field of this class is :code:`contexts`
- OpenCLContext stores most of the important information about a simulation:
- so on.  It also provides access to three other important objects: the
- particles or groups of particles are identical.  This is important when
- Of course, this system relies on certain assumptions, the most important of
- An important point is that this code is executed for every pair of particles in
- important point is that the list of particles forming a “bond” is known in
- by many integrators.  The two most important are random number generation and
- Error handling for OpenMM
- Error handling for OpenMM is explicitly designed so you do not have to check the
- format.   Again, we emphasize how important it is to track the units being used!
