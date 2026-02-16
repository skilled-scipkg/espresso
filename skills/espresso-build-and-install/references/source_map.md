# ESPResSo source map: Build and Install

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `cmake`
- `build`
- `dependencies`
- `features`
- `python`
- `walberla`
- `cuda`
- `tests`

## Fast source navigation
- `rg -n "option\(|find_package|ESPRESSO_BUILD_WITH" CMakeLists.txt src/CMakeLists.txt src/core/CMakeLists.txt src/script_interface/CMakeLists.txt`
- `rg -n "add_subdirectory|target_link_libraries|target_compile_definitions" src/CMakeLists.txt src/python/CMakeLists.txt src/script_interface/CMakeLists.txt`
- `rg -n "build_type|features|scafacos_methods" src/python/espressomd/code_info.py src/script_interface/code_info/CodeInfo.cpp`

## Function-level behavior checks
- Feature gate path: `rg -n "ESPRESSO_BUILD_WITH|CUDA|HDF5|WALBERLA|SCAFACOS" CMakeLists.txt src/CMakeLists.txt src/core/CMakeLists.txt`
- Python module build path: `rg -n "espressomd|cython|python" src/python/CMakeLists.txt src/python/espressomd/CMakeLists.txt`
- Runtime feature reporting path: `rg -n "features|all_features|build_type" src/python/espressomd/code_info.py src/script_interface/code_info/CodeInfo.cpp src/script_interface/code_info/initialize.cpp`
- Test integration path: `rg -n "add_test|ctest|FIXTURES" testsuite/CMakeLists.txt`

## Suggested source entry points
- `CMakeLists.txt` | role: top-level project options and dependency checks.
- `src/CMakeLists.txt` | role: core/source subtree composition.
- `src/core/CMakeLists.txt` | role: core engine build graph and feature toggles.
- `src/script_interface/CMakeLists.txt` | role: script-interface module wiring.
- `src/python/CMakeLists.txt` | role: Python package build and extension integration.
- `src/python/espressomd/CMakeLists.txt` | role: Python extension target details.
- `src/walberla_bridge/CMakeLists.txt` | role: waLBerla bridge build integration.
- `src/script_interface/code_info/CodeInfo.cpp` | role: build feature reporting implementation.
- `src/script_interface/code_info/initialize.cpp` | role: registration of code-info bindings.
- `src/python/espressomd/code_info.py` | role: Python-level build-feature API.
- `testsuite/CMakeLists.txt` | role: test target registration and fixtures.
