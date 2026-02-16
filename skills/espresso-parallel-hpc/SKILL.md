---
name: espresso-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Parallel and HPC

## High-Signal Playbook
### Route conditions
- Use this skill for MPI/OpenMP/GPU launch strategy, decomposition constraints, and scaling bottlenecks.
- Route toolchain/build feature enablement to `espresso-build-and-install`.
- Route first-run local setup and basic sanity scripts to `espresso-getting-started`.
- Route integrator/restart orchestration to `espresso-simulation-workflows`.
- Route detailed Sphinx physics-method semantics to `espresso-sphinx`.

### Triage questions
1. What launch mode is required (serial, MPI-only, MPI+OpenMP, GPU-enabled)?
2. Which subsystem dominates runtime (P3M, LB/waLBerla, short-range interactions, IO)?
3. Are you blocked by launch/runtime errors, poor scaling, or feature availability?
4. What are box size, cutoff, skin, and rank count (decomposition feasibility)?
5. Are long-range solvers and FFT backends enabled as expected?
6. Do you need throughput (many jobs) or low time-to-solution (single large job)?

### Canonical workflow
1. Confirm build/runtime prerequisites in `doc/sphinx/installation.rst` and launch semantics in `doc/sphinx/running.rst`.
2. Start from a serial smoke run, then scale to MPI (`mpiexec -n N ./pypresso simulation.py`).
3. Set OpenMP threads explicitly for hybrid runs (`OMP_NUM_THREADS`) before launch.
4. Verify decomposition constraints against box geometry and interaction ranges (`doc/sphinx/system_setup.rst`).
5. Tune long-range electrostatics only after baseline run is stable (`doc/sphinx/electrostatics.rst`).
6. For LB-heavy workloads, verify waLBerla/LB configuration and output cadence (`doc/sphinx/lb.rst`).
7. For ensemble throughput workloads, use scheduler/worker approaches from `samples/high_throughput_with_dask/Readme.md`.

### Minimal working example
```bash
./pypresso simulation.py
mpiexec -n 4 ./pypresso simulation.py
OMP_NUM_THREADS=2 mpiexec -n 4 ./pypresso simulation.py
```

```bash
./pypresso -c "import espressomd.code_info as ci; print(ci.build_type()); print(ci.features())"
```

### Pitfalls and fixes
- Launching MPI before serial sanity checks hides basic API/model issues; validate serial first.
- Excessive rank count for box/cutoff/skin can trigger runtime decomposition errors (`doc/sphinx/system_setup.rst`).
- Thread oversubscription (high `OMP_NUM_THREADS` with many MPI ranks) degrades throughput.
- Assuming all algorithms scale uniformly leads to poor resource use; some paths are rank-0 heavy (`doc/sphinx/running.rst`).
- Feature mismatch between expected and compiled capabilities causes runtime surprises; verify via `espressomd.code_info`.

### Convergence and validation checks
- Serial and MPI runs produce consistent short-window observables (within statistical noise).
- Strong-scaling tests reduce wall time for the target workload size.
- Requested features are visible in `espressomd.code_info.features()` before production runs.
- Long-range and LB workloads remain stable over short pilot windows before large-scale sweeps.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch systems.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/sphinx/installation.rst`
- `doc/sphinx/running.rst`
- `doc/sphinx/system_setup.rst`
- `doc/sphinx/electrostatics.rst`
- `doc/sphinx/lb.rst`
- `doc/sphinx/io.rst`
- `samples/high_throughput_with_dask/Readme.md`

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
- `src/core/cell_system/CellStructure.cpp` | Domain decomposition setup and constraints.
- `src/core/cell_system/RegularDecomposition.cpp` | Regular domain split behavior.
- `src/core/cell_system/HybridDecomposition.cpp` | Hybrid decomposition logic.
- `src/core/p3m/TuningAlgorithm.cpp` | Electrostatics tuning path for parallel runs.
- `src/core/electrostatics/p3m_heffte.cpp` | Distributed FFT-backed P3M behavior.
- `src/core/electrostatics/p3m_gpu_cuda.cu` | GPU P3M kernel implementation path.
- `src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp` | LB waLBerla setup at runtime.
- `src/walberla_bridge/src/lattice_boltzmann/lb_kernels.hpp` | LB kernel dispatch surface.
- `src/script_interface/walberla/LBFluid.cpp` | Python-facing LB fluid binding behavior.
- `src/python/espressomd/cell_system.py` | Python decomposition controls.
- `src/python/espressomd/electrostatics.py` | Python long-range solver setup APIs.
- `src/python/espressomd/lb.py` | Python LB setup and runtime hooks.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
