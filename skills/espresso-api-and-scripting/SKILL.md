---
name: espresso-api-and-scripting
description: This skill should be used when users ask about api and scripting in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: API and Scripting

## High-Signal Playbook
### Route conditions
- Use this skill for Python API usage, script-interface binding behavior, and symbol-level method semantics.
- Route compile/configure/dependency issues to `espresso-build-and-install`.
- Route first-run onboarding and minimal startup scripts to `espresso-getting-started`.
- Route workflow-level integration/restart sequencing to `espresso-simulation-workflows`.
- Route interaction/solver theory and Sphinx chapter interpretation to `espresso-sphinx`.

### Triage questions
1. Is the issue at Python API call-site, script-interface binding layer, or core implementation?
2. Which module is affected (`system`, `particle_data`, `interactions`, `reaction_methods`, `lb`, `electrostatics`)?
3. Is this an API usage error, a missing binding, or behavior mismatch between docs and runtime?
4. Does the failure happen on import, object creation, method call, or integration run?
5. Are you testing in serial only or under MPI as well?
6. Do you need minimal reproducible script behavior before deep source inspection?

### Canonical workflow
1. Start from API docs and examples in `doc/sphinx/introduction.rst`, `doc/sphinx/system_setup.rst`, and `doc/sphinx/particles.rst`.
2. Reproduce the behavior in a minimal `./pypresso` script before touching source.
3. If Python-layer behavior is unclear, inspect wrappers in `src/python/espressomd/*.py` and `src/python/espressomd/script_interface.pyx`.
4. If binding semantics are unclear, inspect `src/script_interface/*` entry points and registration files.
5. If still unresolved, inspect core implementation tied to the binding call chain.
6. Use symbol search to anchor on the exact class/method name instead of scanning directories.

### Minimal working example
```bash
./pypresso -c "import espressomd;print(espressomd.__version__)"
./pypresso -c "import espressomd.code_info as ci;print(ci.build_type(), len(ci.features()))"
```

```python
import espressomd
system = espressomd.System(box_l=[10.0, 10.0, 10.0])
system.time_step = 0.01
system.cell_system.skin = 0.4
p = system.part.add(pos=[1.0, 1.0, 1.0], type=0)
system.integrator.run(1)
print(p.id, system.time)
```

### Pitfalls and fixes
- API wrappers often require full-vector assignment for vector properties; component-wise writes can fail (`doc/sphinx/system_setup.rst`).
- Runtime wrappers may accept objects but fail later when required features were not compiled in; confirm active features first (`src/python/espressomd/code_info.py`).
- Some methods are bound through script-interface registration and are unavailable if the registration path is not loaded (`src/script_interface/*/initialize.cpp`).
- Errors can surface at integration time rather than object-creation time; always run a short `integrator.run(...)` check.

### Convergence and validation checks
- Minimal script imports `espressomd`, creates a `System`, adds one particle, and runs one integration step.
- Target API call works in a standalone script before being embedded in a larger workflow.
- If behavior differs from docs, map call chain Python wrapper -> script interface -> core symbol and verify each layer.
- When investigating module-level APIs, validate under both serial and MPI launch for parity.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/sphinx/introduction.rst`
- `doc/sphinx/system_setup.rst`
- `doc/sphinx/particles.rst`
- `doc/sphinx/running.rst`
- `doc/sphinx/reaction_methods.rst`
- `doc/sphinx/io.rst`
- `doc/sphinx/under_the_hood.rst`

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
- `src/python/espressomd/script_interface.pyx` | Python<->C++ dispatch and method binding glue.
- `src/python/espressomd/system.py` | High-level `System` API behavior.
- `src/python/espressomd/particle_data.py` | Particle creation/query/update API surface.
- `src/python/espressomd/interactions.py` | Python interaction-object wrappers.
- `src/script_interface/ScriptInterface.hpp` | Core script-interface helper mechanics.
- `src/script_interface/system/System.cpp` | Bound system methods and parameter exposure.
- `src/script_interface/particle_data/ParticleHandle.cpp` | Single-particle method bindings.
- `src/script_interface/particle_data/ParticleList.cpp` | Collection/list operations and iteration bindings.
- `src/script_interface/particle_data/ParticleSlice.cpp` | Slice access/update behavior in bindings.
- `src/script_interface/interactions/initialize.cpp` | Interaction registration into script interface.
- `src/script_interface/reaction_methods/initialize.cpp` | Reaction-method registration and exported symbols.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
