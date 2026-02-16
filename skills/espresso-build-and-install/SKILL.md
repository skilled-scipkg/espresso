---
name: espresso-build-and-install
description: This skill should be used when users ask about build and install in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Build and Install

## High-Signal Playbook
### Route conditions
- Use this skill for dependency setup, CMake feature selection, compile/test loops, and launch sanity checks.
- Route first-script anatomy and onboarding questions to `espresso-getting-started`.
- Route runtime integration/restart orchestration to `espresso-simulation-workflows`.
- Route MPI/OpenMP scaling and scheduler details to `espresso-parallel-hpc`.
- Route model/physics parameterization to `espresso-inputs-and-modeling`.

### Triage questions
1. Which platform are you targeting (local Linux/macOS/WSL vs HPC cluster)?
2. Are failures happening in configure, compile, link, or runtime launch?
3. Which optional features are required (`CUDA`, `HDF5`, tests, waLBerla, ScaFaCoS)?
4. Are you using an isolated Python environment (`venv`/conda/uv)?
5. Do you need reproducible debug builds (`RelWithAssert`/sanitizers) or production throughput?
6. Will this build run serial-only, MPI-only, or hybrid MPI+OpenMP?

### Canonical workflow
1. Install toolchain prerequisites and Python dependencies (`doc/sphinx/installation.rst`).
2. Create/activate a Python environment before pip installs (`doc/sphinx/installation.rst`).
3. Configure in a dedicated build directory via `cmake ..` and explicit `-D` feature flags.
4. Compile with `make -j$(nproc)` and stop on first CMake or compiler error.
5. Run `./pypresso` smoke test and one sample script.
6. Validate MPI launch with `mpirun`/`mpiexec` once serial launch succeeds.
7. Enable tests (`-D ESPRESSO_BUILD_TESTS=ON`) and run `ctest` if this is a reusable environment.
8. For CUDA, pin toolkit paths/architectures before configuring (`doc/sphinx/installation.rst`).

### Minimal working example
```bash
python3 -m venv espresso_env
. espresso_env/bin/activate
python3 -m pip install -c requirements.txt cmake cython numpy scipy packaging setuptools h5py
mkdir -p build && cd build
cmake ..
make -j"$(nproc)"
./pypresso -c "import espressomd;print(espressomd.__version__)"
mpirun -n 4 ./pypresso ../samples/lj_liquid.py
```

```bash
# CUDA example when multiple toolkits are installed
CUDAARCHS="75;86" cmake .. -D ESPRESSO_BUILD_WITH_CUDA=ON
```

### Pitfalls and fixes
- Open MPI 4.x singleton NUMA failures: set `OMPI_MCA_hwloc_base_binding_policy` (for example `l3cache` or `none`) as documented in `doc/sphinx/installation.rst`.
- Missing `Boost.MPI` on clusters: install or build Boost with MPI support (`doc/sphinx/installation.rst`).
- Using serial HDF5 with HDF5 feature enabled causes runtime/build mismatch; use parallel HDF5 packages (`doc/sphinx/io.rst`).
- CMake success is mandatory; do not proceed when configure reports missing required dependencies (`doc/sphinx/installation.rst`).
- `-ffast-math` can break correctness for some ESPResSo components; avoid aggressive math flags unless validated (`doc/sphinx/installation.rst`).
- CUDA arch/toolkit mismatch leads to failed or suboptimal binaries; set toolkit root and architectures explicitly (`doc/sphinx/installation.rst`).
- Conflicting Python headers/interpreters in mixed environments break Cython builds; keep interpreter and headers aligned (`doc/sphinx/installation.rst`).

### Convergence and validation checks
- `./pypresso -c "import espressomd"` succeeds in the target environment.
- A sample script runs in serial and under MPI without fatal startup errors.
- Requested feature toggles are reflected in CMake cache/build summary before long runs.
- If tests are enabled, `ctest --output-on-failure` passes core smoke checks.
- Debugging builds use `RelWithAssert`/sanitizers for crash triage before switching back to `Release`.

## Scope
- Handle questions about build, installation, compilation, and environment setup.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/sphinx/installation.rst`
- `doc/sphinx/running.rst`
- `doc/sphinx/contributing.rst`
- `doc/sphinx/io.rst`
- `doc/tutorials/mlip-water/Readme.md`
- `INSTALL`
- `CMakeLists.txt`
- `testsuite/CMakeLists.txt`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `samples`
- `doc/tutorials`
- `testsuite/samples`
- `testsuite/tutorials`

## Test references
- `testsuite`
- `src/core/unit_tests`
- `src/instrumentation/tests`
- `src/particle_observables/tests`
- `src/script_interface/tests`
- `src/shapes/unit_tests`
- `src/utils/tests`
- `src/walberla_bridge/tests`
- `src/core/reaction_methods/tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `CMakeLists.txt` | Top-level feature options and dependency gates.
- `src/CMakeLists.txt` | Core build graph and component composition.
- `src/core/CMakeLists.txt` | Core engine target wiring and feature flags.
- `src/script_interface/CMakeLists.txt` | Script-interface module build integration.
- `src/python/CMakeLists.txt` | Python extension build flow.
- `src/python/espressomd/CMakeLists.txt` | Python module target and extension wiring.
- `src/walberla_bridge/CMakeLists.txt` | waLBerla bridge integration and optional target gating.
- `src/script_interface/code_info/CodeInfo.cpp` | Runtime reporting of compiled features/build type.
- `src/script_interface/code_info/initialize.cpp` | Registration of code-info bindings.
- `src/python/espressomd/code_info.py` | Python API for checking compiled capabilities.
- `testsuite/CMakeLists.txt` | Test target registration and fixture behavior.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
