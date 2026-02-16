---
name: espresso-getting-started
description: This skill should be used when users ask about getting started in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Getting Started

## High-Signal Playbook
### Route conditions
- Use this skill for first-run setup, version checks, and minimal runnable scripts.
- Route compiler/dependency failures to `espresso-build-and-install`.
- Route system modeling, boundary, and IO/checkpoint design to `espresso-inputs-and-modeling`.
- Route execution control, restart strategy, and MPI/OpenMP runtime behavior to `espresso-simulation-workflows`.
- Route deep interaction and solver semantics to `espresso-sphinx`.

### Triage questions
1. Are you launching with `./pypresso`/`./ipypresso` from a build directory, or via an installed package?
2. Do you need CLI script execution, notebook execution, or both?
3. Is your blocker at import time (`import espressomd`) or during integration (`integrator.run`)?
4. Are you targeting single-rank startup or immediate MPI launch?
5. Do you want tutorial-first onboarding (`doc/tutorials`) or a minimal custom script?
6. Are you planning throughput batching with Dask (`samples/high_throughput_with_dask`)?

### Canonical workflow
1. Confirm prerequisites and launch style from `doc/sphinx/installation.rst` and `doc/sphinx/running.rst`.
2. Verify the runtime version using the command shown in `doc/sphinx/introduction.rst`.
3. Start with a one-system script using `box_l`, `time_step`, and `cell_system.skin` (`doc/sphinx/introduction.rst`).
4. Run 1-10 integration steps before adding interactions/analysis.
5. Launch tutorials via `ipypresso` as documented in `doc/tutorials/Readme.md`.
6. Scale to MPI only after serial smoke tests pass (`doc/sphinx/running.rst`).
7. For uncertainty reporting, use the error-analysis tutorial (`doc/tutorials/error_analysis/Readme.md`).
8. For parallel parameter sweeps, follow `samples/high_throughput_with_dask/Readme.md`.

### Minimal working example
```bash
./pypresso -c "import espressomd;print(espressomd.__version__)"
cd doc/tutorials
../../ipypresso lab
```

```python
import espressomd
system = espressomd.System(box_l=[10, 10, 10])
system.time_step = 0.01
system.cell_system.skin = 0.4
system.integrator.run(1)
print(system.time)
```

### Pitfalls and fixes
- Creating multiple `System` instances fails; keep one system object and reset state (`doc/sphinx/introduction.rst`).
- Component-wise edits like `system.box_l[0] = ...` are invalid; reassign full vectors or copy first (`doc/sphinx/system_setup.rst`).
- Tutorial kernels fail when not launched via wrappers; use `pypresso`/`ipypresso` paths from `doc/sphinx/running.rst`.
- `dask.distributed.LocalCluster` is not supported; use scheduler/worker mode (`samples/high_throughput_with_dask/Readme.md`).
- In Dask workflows, plain `print()` in simulation code can break transport format; use `logging` for status (`samples/high_throughput_with_dask/Readme.md`).
- Reporting IID-style uncertainty on correlated MD time series is misleading; use correlation-aware analysis (`doc/tutorials/error_analysis/Readme.md`).

### Convergence and validation checks
- Version check succeeds and one-step script runs without import/runtime errors.
- `system.time` advances monotonically across repeated `integrator.run(...)` calls.
- The same minimal script runs both serially and under MPI launch.
- For time-series claims, verify error bars with correlation-aware estimators (`doc/tutorials/error_analysis/Readme.md`).

## Scope
- Handle questions about initial setup, quickstarts, and core concepts.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/tutorials/Readme.md`
- `doc/sphinx/introduction.rst`
- `samples/high_throughput_with_dask/Readme.md`
- `doc/tutorials/error_analysis/Readme.md`
- `doc/sphinx/particles.rst`
- `doc/sphinx/installation.rst`
- `doc/sphinx/appendix.rst`

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
- `src/python/espressomd/__init__.py` | Package bootstrap imports for startup behavior.
- `src/python/espressomd/_init.pyx` | Cython bootstrap path for initializing the Python extension.
- `src/python/espressomd/system.py` | Core system object APIs used in minimal startup scripts.
- `src/python/espressomd/particle_data.py` | Particle creation/access APIs used in first simulations.
- `src/python/espressomd/integrate.py` | Integrator controls used in one-step smoke tests.
- `src/script_interface/system/initialize.cpp` | Registration of system bindings.
- `src/script_interface/integrators/initialize.cpp` | Registration of integrator bindings.
- `src/script_interface/integrators/IntegratorHandle.cpp` | Integrator call dispatch in bindings.
- `src/core/integrators/velocity_verlet_inline.hpp` | Core integration stepping behavior.
- `src/core/error_handling/RuntimeErrorStream.cpp` | Runtime error stream plumbing.
- `src/core/error_handling/RuntimeErrorCollector.cpp` | Runtime error aggregation and surfacing.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
