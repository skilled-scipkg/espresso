# ESPResSo source map: Simulation Workflows

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `integrator`
- `thermostat`
- `reaction`
- `restart`
- `checkpoint`
- `lb`
- `workflow`
- `run`

## Fast source navigation
- `rg -n "integrator|run|VelocityVerlet|SteepestDescent" src/python/espressomd/integrate.py src/script_interface/integrators src/core/integrators`
- `rg -n "ReactionEnsemble|ConstantpHEnsemble|WidomInsertion|ReactionAlgorithm" src/python/espressomd/reaction_methods.py src/script_interface/reaction_methods src/core/reaction_methods`
- `rg -n "checkpoint|save|load|reuse_forces|VTK" src/python/espressomd/checkpointing.py src/python/espressomd/lb.py src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp`

## Function-level behavior checks
- Integrator path: `rg -n "def run|set_vv|set_steepest_descent|IntegratorHandle" src/python/espressomd/integrate.py src/script_interface/integrators/IntegratorHandle.cpp src/script_interface/integrators/VelocityVerlet.cpp`
- Thermostat coupling path: `rg -n "thermostat|set_langevin|set_brownian" src/python/espressomd/thermostat.py src/script_interface/thermostat src/core/thermostats`
- Reaction workflow path: `rg -n "add_reaction|attempt|do_reaction|exclusion_range" src/python/espressomd/reaction_methods.py src/script_interface/reaction_methods/ReactionAlgorithm.cpp src/core/reaction_methods/ReactionAlgorithm.cpp`
- Restart/LB path: `rg -n "checkpoint|save|load|reuse_forces" src/python/espressomd/checkpointing.py src/python/espressomd/lb.py src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp`

## Suggested source entry points
- `src/python/espressomd/integrate.py` | role: user-facing integration control API.
- `src/script_interface/integrators/IntegratorHandle.cpp` | role: script-interface integrator dispatch.
- `src/script_interface/integrators/VelocityVerlet.cpp` | role: velocity-Verlet binding behavior.
- `src/script_interface/integrators/SteepestDescent.cpp` | role: steepest-descent binding behavior.
- `src/core/integrators/velocity_verlet_inline.hpp` | role: core velocity-Verlet integration step.
- `src/python/espressomd/thermostat.py` | role: thermostat configuration APIs.
- `src/python/espressomd/reaction_methods.py` | role: Python reaction workflow controls.
- `src/script_interface/reaction_methods/ReactionAlgorithm.cpp` | role: script-interface reaction dispatch.
- `src/core/reaction_methods/ReactionAlgorithm.cpp` | role: core MC reaction implementation.
- `src/python/espressomd/checkpointing.py` | role: restart state save/load APIs.
- `src/python/espressomd/lb.py` | role: LB callbacks and checkpoint interactions.
- `src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp` | role: LB waLBerla runtime wiring.
