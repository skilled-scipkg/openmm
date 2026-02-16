# openmm source map: Docs Source

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
- `docs build`
- `sphinx`
- `doxygen`
- `api docs`
- `license`
- `bibliography`
- `wrapper docs`

## Fast source navigation
- `rg -n "sphinxhtml|sphinxpdf|OPENMM_GENERATE_API_DOCS" docs-source wrappers CMakeLists.txt`
- `rg -n "Doxyfile|swig_doxygen|generateWrappers" wrappers docs-source`
- `rg -n "License|Bibliography|Citation" docs-source/usersguide docs-source/licenses`

## Suggested source entry points
- `docs-source/CMakeLists.txt` | user/developer guide and API-doc build target definitions.
- `docs-source/api-c++/CMakeLists.txt` | C++ API docs build wiring.
- `docs-source/api-python/CMakeLists.txt` | Python API docs build wiring.
- `docs-source/usersguide/license.rst` | canonical license wording for user guide responses.
- `docs-source/usersguide/zbibliography.rst` | canonical bibliography/citation source.
- `docs-source/licenses/Licenses.txt` | aggregated third-party licensing text.
- `docs-source/licenses/LGPL.txt` | LGPL license text used in docs guidance.
- `docs-source/licenses/GPL.txt` | GPL license text used in docs guidance.
- `wrappers/CMakeLists.txt` | wrapper docs generation targets and dependencies.
- `wrappers/Doxyfile.in` | Doxygen template used for API extraction.
- `wrappers/python/src/swig_doxygen/doxygen/Doxyfile.in` | SWIG+doxygen extraction settings.
- `wrappers/python/src/swig_doxygen/swigInputBuilder.py` | generation step from XML docs to SWIG inputs.
- `wrappers/python/src/swig_doxygen/OpenMM.i` | wrapper interface consumed by generated docs.
- `wrappers/generateWrappers.py` | final wrapper-generation pipeline tied to docs metadata.
