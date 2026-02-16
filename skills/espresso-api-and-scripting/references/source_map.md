# ESPResSo source map: API and Scripting

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `api`
- `binding`
- `script_interface`
- `system`
- `particle`
- `interactions`
- `wrapper`
- `python`

## Fast source navigation
- `rg -n "<symbol_or_keyword>" src/python/espressomd src/script_interface src/core`
- `rg -n "script_interface_register|_so_name|_so_bind_methods" src/python/espressomd`
- `rg -n "initialize\(|do_call_method|AutoParameters" src/script_interface`

## Function-level behavior checks
- Python system API path: `rg -n "class System|def __init__|def volume" src/python/espressomd/system.py src/script_interface/system/System.cpp`
- Particle API path: `rg -n "class ParticleHandle|def add|def by_id|def remove" src/python/espressomd/particle_data.py src/script_interface/particle_data/ParticleHandle.cpp`
- Interaction binding path: `rg -n "NonBonded|Bonded|set_params|add_bond" src/python/espressomd/interactions.py src/script_interface/interactions/initialize.cpp`
- Reaction binding path: `rg -n "ReactionEnsemble|ConstantpHEnsemble|WidomInsertion" src/python/espressomd/reaction_methods.py src/script_interface/reaction_methods/initialize.cpp`

## Suggested source entry points
- `src/python/espressomd/script_interface.pyx` | role: Cython bridge to script-interface objects.
- `src/python/espressomd/system.py` | role: high-level `System` API and module state access.
- `src/python/espressomd/particle_data.py` | role: particle CRUD and per-particle handle behavior.
- `src/python/espressomd/interactions.py` | role: non-bonded and bonded wrapper APIs.
- `src/script_interface/ScriptInterface.hpp` | role: script-interface base abstractions.
- `src/script_interface/system/System.cpp` | role: bound system methods and parameter plumbing.
- `src/script_interface/particle_data/ParticleHandle.cpp` | role: per-particle method dispatch.
- `src/script_interface/particle_data/ParticleList.cpp` | role: particle-list iteration and query behavior.
- `src/script_interface/particle_data/ParticleSlice.cpp` | role: vectorized/slice particle operations.
- `src/script_interface/interactions/initialize.cpp` | role: interaction class registration.
- `src/script_interface/reaction_methods/initialize.cpp` | role: reaction-method class registration.
- `src/python/espressomd/code_info.py` | role: build-feature introspection for API availability checks.
