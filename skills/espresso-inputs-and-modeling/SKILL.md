---
name: espresso-inputs-and-modeling
description: This skill should be used when users ask about inputs and modeling in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Inputs and Modeling

## High-Signal Playbook
### Route conditions
- Use this skill for `System` setup, boundary/cell-system choices, IO/checkpoint formats, and analysis/correlator configuration.
- Route installation and compiler/toolchain issues to `espresso-build-and-install`.
- Route execution loop control (integrators, restart sequencing, MPI launch syntax) to `espresso-simulation-workflows`.
- Route broad interaction-model theory and solver internals to `espresso-sphinx`.
- Route tutorial selection to `espresso-examples-and-tutorials`.

### Triage questions
1. What are `box_l`, periodicity, and expected interaction cutoffs?
2. Are you writing restartable runs (checkpointing), and must they be deterministic?
3. Which output format is needed (`H5MD`, `MPI-IO`, `VTK`) and where will it be read?
4. How many MPI ranks will run compared to cutoff + skin constraints?
5. Are LB/EK fields involved (which need extra checkpoint handling)?
6. Are you optimizing physics accuracy, throughput, or both?

### Canonical workflow
1. Define `System` globals first: `box_l`, `time_step`, `cell_system.skin`, periodicity (`doc/sphinx/system_setup.rst`).
2. Set required global cutoffs and decomposition strategy before adding complex actors.
3. Validate rank/decomposition feasibility against cutoff + skin limits (`doc/sphinx/system_setup.rst`).
4. Choose portable output (`H5MD`) unless you explicitly need machine-specific MPI-IO (`doc/sphinx/io.rst`).
5. Register checkpointable objects/signals at global scope (`doc/sphinx/io.rst`).
6. For LB/EK, save/load lattice field checkpoints in addition to generic checkpoints (`doc/sphinx/io.rst`, `doc/sphinx/ek.rst`).
7. Run short integrations and compare key observables pre/post restart.
8. Add correlators/analysis only after baseline state transitions are stable (`doc/sphinx/analysis.rst`).

### Minimal working example
```python
import espressomd
system = espressomd.System(box_l=[10., 10., 10.])
system.time_step = 0.01
system.cell_system.skin = 0.4
system.periodicity = [True, True, True]
```

```python
import signal
import espressomd.checkpointing
checkpoint = espressomd.checkpointing.Checkpoint(
    checkpoint_id="mycheckpoint", checkpoint_path=".")
checkpoint.register("system")
checkpoint.register_signal(signal.SIGINT)
checkpoint.save()
# on restart with thermostat/LB coupling:
system.integrator.run(2, reuse_forces=True)
```

### Pitfalls and fixes
- Component-wise writes to vector properties (`box_l`, `periodicity`) are invalid; reassign full vectors (`doc/sphinx/system_setup.rst`).
- Non-periodic axes do not confine particles by themselves; add constraints for physical walls (`doc/sphinx/system_setup.rst`).
- Excess MPI ranks for chosen box/cutoff/skin can trigger runtime errors during integration; increase box size or reduce cutoff/skin (`doc/sphinx/system_setup.rst`).
- Generic checkpoint restore requires same MPI rank count (`doc/sphinx/io.rst`).
- Checkpoints are not portable across ESPResSo versions or arbitrary Python environments (`doc/sphinx/io.rst`).
- Checkpointed objects must be global-scope; local-scope objects are skipped (`doc/sphinx/io.rst`).
- LB/EK generic checkpoints do not include full lattice fields; call lattice-specific save/load methods (`doc/sphinx/io.rst`, `doc/sphinx/ek.rst`).
- MPI-IO binary format is machine-dependent and can silently misread on different architectures (`doc/sphinx/io.rst`).
- Parallel VTK outputs are multi-piece; use `espressomd.io.vtk.VTKReader` for correct topology reconstruction (`doc/sphinx/ek.rst`).

### Convergence and validation checks
- Decomposition check: rank count is consistent with box length and `cutoff + skin` constraints.
- Restart check: observables do not jump/drift after checkpoint restore (`doc/sphinx/io.rst`).
- Determinism check: first post-restore integration uses `reuse_forces=True` when required.
- IO round-trip check: H5MD/VTK data readback matches in-memory values on a small test case.
- Correlator check: `tau_lin`/compression settings are chosen to limit systematic bias (`doc/sphinx/analysis.rst`).

## Scope
- Handle questions about inputs, system setup, models, and physical parameterization.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/sphinx/visualization.rst`
- `doc/sphinx/system_setup.rst`
- `doc/sphinx/io.rst`
- `doc/sphinx/ek.rst`
- `doc/sphinx/analysis.rst`
- `doc/sphinx/advanced_methods.rst`

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
- `src/core/cell_system/CellStructure.hpp` | Core cell decomposition state and operations.
- `src/core/cell_system/CellStructure.cpp` | Cell decomposition/runtime behavior details.
- `src/core/cell_system/CellStructureType.hpp` | Cell-structure mode/type semantics.
- `src/script_interface/system/System.cpp` | Python binding layer for global system properties.
- `src/script_interface/system/initialize.cpp` | Registration/init of system-level script interface classes.
- `src/core/field_coupling/ForceField.hpp` | Field-coupling model definitions.
- `src/core/unit_tests/field_coupling_force_field_test.cpp` | Expected force-field behavior in tests.
- `src/core/immersed_boundary/ImmersedBoundaries.cpp` | Immersed-boundary state updates.
- `src/core/immersed_boundary/ibm_common.cpp` | Shared immersed-boundary helpers.
- `src/walberla_bridge/src/utils/boundary.hpp` | waLBerla-side boundary utility logic.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
