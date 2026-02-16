# ESPResSo source map: Examples and Tutorials

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `tutorial`
- `example`
- `lb`
- `reaction`
- `polymer`
- `electrostatics`
- `magnetostatics`
- `interactions`

## Fast source navigation
- `rg -n "LBFluid|walberla|vtk|grid" src/python/espressomd/lb.py src/walberla_bridge src/script_interface/walberla`
- `rg -n "ReactionEnsemble|ConstantpHEnsemble|WidomInsertion" src/python/espressomd/reaction_methods.py src/script_interface/reaction_methods src/core/reaction_methods`
- `rg -n "Lennard|WCA|set_params|NonBonded" src/python/espressomd/interactions.py src/script_interface/interactions`

## Function-level behavior checks
- LB tutorial path: `rg -n "class LBFluid|VTK|checkpoint" src/python/espressomd/lb.py src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp`
- Reaction tutorial path: `rg -n "add_reaction|ReactionAlgorithm|attempt" src/python/espressomd/reaction_methods.py src/script_interface/reaction_methods/ReactionAlgorithm.cpp src/core/reaction_methods/ReactionAlgorithm.cpp`
- Charged-system path: `rg -n "CoulombP3M|MMM1D|ReactionField" src/python/espressomd/electrostatics.py src/script_interface/electrostatics/CoulombP3M.hpp`
- Ferrofluid/magnetics path: `rg -n "DipolarP3M|DipolarDirectSum|DipolarLayerCorrection" src/python/espressomd/magnetostatics.py src/script_interface/magnetostatics/DipolarP3M.hpp`

## Suggested source entry points
- `src/python/espressomd/lb.py` | role: Python LB APIs used by LB tutorials.
- `src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp` | role: LB-waLBerla initialization path.
- `src/walberla_bridge/src/lattice_boltzmann/LBWalberlaImpl.hpp` | role: core waLBerla LB implementation hooks.
- `src/python/espressomd/reaction_methods.py` | role: reaction tutorial APIs and parameters.
- `src/script_interface/reaction_methods/ReactionAlgorithm.cpp` | role: script-interface reaction dispatch behavior.
- `src/core/reaction_methods/ReactionAlgorithm.cpp` | role: core reaction move implementation.
- `src/python/espressomd/interactions.py` | role: interaction setup used across many tutorials.
- `src/script_interface/interactions/NonBondedInteraction.hpp` | role: non-bonded interaction binding surface.
- `src/python/espressomd/electrostatics.py` | role: electrostatics APIs for charged-system workflows.
- `src/script_interface/electrostatics/CoulombP3M.hpp` | role: Coulomb P3M binding class.
- `src/python/espressomd/magnetostatics.py` | role: magnetostatics APIs used in ferrofluid tutorials.
- `src/script_interface/magnetostatics/DipolarP3M.hpp` | role: dipolar P3M binding surface.
