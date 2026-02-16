# ESPResSo source map: Getting Started

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `startup`
- `system`
- `particle`
- `integrator`
- `thermostat`
- `error`
- `import`
- `quickstart`

## Fast source navigation
- `rg -n "class System|System\(|time_step|cell_system" src/python/espressomd/system.py src/python/espressomd/cell_system.py`
- `rg -n "integrator|run|VelocityVerlet|SteepestDescent" src/python/espressomd/integrate.py src/script_interface/integrators src/core/integrators`
- `rg -n "RuntimeError|error|throw" src/core/error_handling src/python/espressomd`

## Function-level behavior checks
- Import/bootstrap path: `rg -n "import|from \.|_init" src/python/espressomd/__init__.py src/python/espressomd/_init.pyx`
- Minimal system path: `rg -n "class System|time_step|periodicity|cell_system" src/python/espressomd/system.py src/script_interface/system/System.cpp`
- Minimal integration path: `rg -n "def run|VelocityVerlet|SteepestDescent" src/python/espressomd/integrate.py src/script_interface/integrators/IntegratorHandle.cpp src/core/integrators/velocity_verlet_inline.hpp`
- Error surfacing path: `rg -n "RuntimeError|RuntimeErrorCollector|RuntimeErrorStream" src/core/error_handling`

## Suggested source entry points
- `src/python/espressomd/__init__.py` | role: package-level bootstrap and imports.
- `src/python/espressomd/_init.pyx` | role: low-level Cython initialization bridge.
- `src/python/espressomd/system.py` | role: first user-facing simulation object setup.
- `src/python/espressomd/particle_data.py` | role: initial particle creation and access methods.
- `src/python/espressomd/integrate.py` | role: integration API entry points for startup scripts.
- `src/python/espressomd/thermostat.py` | role: thermostat setup APIs commonly used early.
- `src/script_interface/system/initialize.cpp` | role: registration of system bindings.
- `src/script_interface/integrators/initialize.cpp` | role: registration of integrator bindings.
- `src/script_interface/integrators/IntegratorHandle.cpp` | role: bound integrator dispatch behavior.
- `src/core/integrators/velocity_verlet_inline.hpp` | role: default integration stepping logic.
- `src/core/error_handling/RuntimeErrorStream.cpp` | role: runtime error stream capture path.
- `src/core/error_handling/RuntimeErrorCollector.cpp` | role: runtime error aggregation behavior.
