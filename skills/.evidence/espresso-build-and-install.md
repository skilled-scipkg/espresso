# Evidence: espresso-build-and-install

## Primary docs
- `doc/tutorials/mlip-water/Readme.md`
- `testsuite/CMakeLists.txt`
- `doc/CMakeLists.txt`
- `testsuite/tutorials/CMakeLists.txt`
- `testsuite/scripts/CMakeLists.txt`
- `testsuite/samples/CMakeLists.txt`
- `testsuite/python/CMakeLists.txt`
- `testsuite/cmake/CMakeLists.txt`
- `testsuite/benchmarks/CMakeLists.txt`
- `doc/tutorials/CMakeLists.txt`
- `doc/sphinx/CMakeLists.txt`
- `doc/logo/CMakeLists.txt`

## Primary source entry points
- `skills/espresso-build-and-install/references/doc_map.md`
- `src/script_interface/walberla/CMakeLists.txt`
- `src/script_interface/shapes/CMakeLists.txt`
- `src/script_interface/particle_data/CMakeLists.txt`
- `src/script_interface/observables/CMakeLists.txt`
- `src/walberla_bridge/CMakeLists.txt`
- `src/script_interface/CMakeLists.txt`
- `src/particle_observables/CMakeLists.txt`
- `src/walberla_bridge/src/CMakeLists.txt`
- `src/script_interface/thermostat/CMakeLists.txt`
- `src/script_interface/system/CMakeLists.txt`
- `src/script_interface/scafacos/CMakeLists.txt`
- `src/script_interface/reaction_methods/CMakeLists.txt`
- `src/script_interface/profiler/CMakeLists.txt`
- `src/script_interface/pair_criteria/CMakeLists.txt`
- `src/script_interface/mpiio/CMakeLists.txt`
- `src/script_interface/math/CMakeLists.txt`
- `src/script_interface/magnetostatics/CMakeLists.txt`
- `src/script_interface/lees_edwards/CMakeLists.txt`
- `src/script_interface/lb/CMakeLists.txt`

## Extracted headings
- Tutorial: integrating MLIPs with ESPResSo - a tutorial on simulating water
- Environment setup
- create virtual environment
- install dependencies
- patch dependencies
- build and install Packmol
- download training data
- launch JupyterLab inside the environment
- Run the tutorial
- Part 1: TIP4P Water
- Copyright (C) 2015-2024 The ESPResSo project
- This file is part of ESPResSo.

## Executable command hints
- python -m venv venv
- ${CMAKE_SOURCE_DIR}/maintainer/parsing/importlib_wrapper.py)
- ${CMAKE_CURRENT_BINARY_DIR}/test_importlib_wrapper.py)
- ${PYPRESSO_OPTIONS} ${TEST_SRC})
- ${TEST_NAME} PROPERTIES FIXTURES_SETUP "FIXTURE_${TEST_TYPE}"
- ${ARGN})
- ${TEST_FILE_CONFIGURED})
- ${TEST_NAME} PROPERTIES FIXTURES_REQUIRED "FIXTURE_${TEST_TYPE}"
- ${CMAKE_CURRENT_BINARY_DIR}/importlib_wrapper.py COPYONLY)
- ${TUTORIALS_DIR} # cleanup
- ${TUTORIALS_DIR} DEPENDS tutorials_python)
- ${ESPRESSO_CTEST_ARGS} --output-on-failure)

## Warnings and pitfalls
- (none extracted)
