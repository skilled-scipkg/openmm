# Evidence: openmm-simulation-workflows

## Primary docs
- `docs-source/api-c++/index.rst`
- `docs-source/api-c++/integrators.rst`
- `docs-source/usersguide/theory/04_integrators.rst`
- `docs-source/usersguide/library/08_amoeba_plugin.rst`
- `docs-source/usersguide/application/04_advanced_sim_examples.rst`
- `docs-source/usersguide/library/09_rpmd_plugin.rst`

## Primary source entry points
- `skills/openmm-simulation-workflows/references/doc_map.md`
- `wrappers/python/openmm/app/simulation.py`
- `plugins/rpmd/openmmapi/src/RPMDIntegrator.cpp`
- `plugins/rpmd/openmmapi/include/openmm/RPMDIntegrator.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceWcaDispersionForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceWcaDispersionForce.cpp`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceVdwForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceVdwForce.cpp`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceTorsionTorsionForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceTorsionTorsionForce.cpp`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceMultipoleForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceMultipoleForce.cpp`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceHippoNonbondedForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceHippoNonbondedForce.cpp`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceGeneralizedKirkwoodForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceGeneralizedKirkwoodForce.cpp`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceForce.h`
- `plugins/amoeba/platforms/reference/src/SimTKReference/AmoebaReferenceForce.cpp`
- `libraries/asmjit/asmjit/core/jitruntime.h`
- `libraries/asmjit/asmjit/core/jitruntime.cpp`

## Extracted headings
- (none extracted)

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- integration error below a user-specified tolerance.  It compares the positions
- of the integration error:
- error={\left(\Delta t\right)}^{2}\sum _{i}\frac{|\mathbf{f}_{i}|}{m_i}
- is its mass.  (In practice, the error made by the Euler integrator is usually
- the true error.  Even so, it can provide a useful mechanism for step size
- It then selects the value of :math:`\Delta t` that makes the error exactly equal the
- specified error tolerance:
- where :math:`\delta` is the error tolerance.  This is the largest step that may be
- in both stability and efficiency.  It can take larger steps on average, but will
- precise energy conservation is not important, such as when simulating a system
- :math:`A` generally needs to be determined by trial and error to find a value
- that produces fast adaptation and good convergence.
