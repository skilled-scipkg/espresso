---
name: espresso-index
description: This skill should be used when users ask how to use ESPResSo and the correct generated documentation skill must be selected before going deeper into source code.
---

# ESPResSo Skills Index

## Route the request
- Classify the request into one of the generated topic skills listed below.
- Prefer abstract, workflow-level guidance for large scientific packages; do not attempt full function-by-function coverage unless explicitly requested.

## Generated topic skills
- `espresso-build-and-install`: Build and Install (build, installation, compilation, and environment setup)
- `espresso-examples-and-tutorials`: Examples and Tutorials (worked examples, tutorials, and cookbook usage)
- `espresso-simulation-workflows`: Simulation Workflows (simulation setup, execution flow, and runtime controls)
- `espresso-getting-started`: Getting Started (initial setup, quickstarts, and core concepts)
- `espresso-inputs-and-modeling`: Inputs and Modeling (inputs, system setup, models, and physical parameterization)
- `espresso-api-and-scripting`: API and Scripting (language bindings, APIs, and programmatic interfaces)
- `espresso-parallel-hpc`: Parallel and HPC (MPI/OpenMP/GPU execution, scaling, and batch systems)
- `espresso-sphinx`: Sphinx (documentation grouped under the 'sphinx' theme)

## Documentation-first inputs
- `doc`

## Tutorials and examples roots
- `samples`
- `doc/tutorials`
- `testsuite/samples`
- `testsuite/tutorials`

## Test roots for behavior checks
- `testsuite`
- `src/core/unit_tests`
- `src/instrumentation/tests`
- `src/particle_observables/tests`
- `src/script_interface/tests`
- `src/shapes/unit_tests`
- `src/utils/tests`
- `src/walberla_bridge/tests`
- `src/core/reaction_methods/tests`

## Escalate only when needed
- Start from topic skill primary references.
- If those references are insufficient, open the selected skill's doc map (for example `skills/espresso-simulation-workflows/references/doc_map.md`).
- If documentation still leaves ambiguity, open the selected skill's source map (for example `skills/espresso-simulation-workflows/references/source_map.md`) and inspect the suggested source entry points.
- Use targeted symbol search while inspecting source (e.g., `rg -n "<symbol_or_keyword>" src`).

## Source directories for deeper inspection
- `src`
