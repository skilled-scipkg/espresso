# ESPResSo source map: Sphinx

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `interactions`
- `constraints`
- `system`
- `magnetostatics`
- `nonbonded`
- `bonded`
- `dipolar`
- `manual`

## Fast source navigation
- `rg -n "NonBonded|Bonded|set_params|bond" src/python/espressomd/interactions.py src/script_interface/interactions`
- `rg -n "Constraint|ShapeBasedConstraint|ExternalField|HomogeneousMagneticField" src/script_interface/constraints src/python/espressomd/constraints.py`
- `rg -n "DipolarP3M|DipolarLayerCorrection|DipolarDirectSum" src/script_interface/magnetostatics src/python/espressomd/magnetostatics.py`

## Function-level behavior checks
- Non-bonded/bonded setup path: `rg -n "NonBondedInteraction|BondedInteraction|initialize" src/script_interface/interactions/initialize.cpp src/script_interface/interactions/NonBondedInteraction.hpp src/script_interface/interactions/BondedInteraction.hpp`
- Constraint path: `rg -n "ShapeBasedConstraint|Constraint|ExternalField|initialize" src/script_interface/constraints/initialize.cpp src/script_interface/constraints/ShapeBasedConstraint.hpp`
- System-manipulation path: `rg -n "box|periodicity|volume|cell_system" src/script_interface/system/System.cpp src/python/espressomd/system.py`
- Magnetostatics path: `rg -n "DipolarP3M|DipolarLayerCorrection|DipolarDirectSum|initialize" src/script_interface/magnetostatics/initialize.cpp src/script_interface/magnetostatics/DipolarP3M.hpp src/python/espressomd/magnetostatics.py`

## Suggested source entry points
- `src/script_interface/interactions/initialize.cpp` | role: registration of interaction bindings.
- `src/script_interface/interactions/NonBondedInteraction.hpp` | role: non-bonded interaction binding surface.
- `src/script_interface/interactions/BondedInteraction.hpp` | role: bonded interaction binding surface.
- `src/python/espressomd/interactions.py` | role: user-facing interaction API wrappers.
- `src/script_interface/constraints/initialize.cpp` | role: constraint binding registration.
- `src/script_interface/constraints/ShapeBasedConstraint.hpp` | role: shape-based constraint wrapper behavior.
- `src/script_interface/constraints/ExternalField.hpp` | role: external-field constraint wrapper behavior.
- `src/script_interface/system/System.cpp` | role: system-manipulation binding methods.
- `src/script_interface/system/initialize.cpp` | role: system module registration path.
- `src/script_interface/magnetostatics/initialize.cpp` | role: magnetostatics registration path.
- `src/script_interface/magnetostatics/DipolarP3M.hpp` | role: dipolar P3M wrapper behavior.
- `src/script_interface/magnetostatics/DipolarLayerCorrection.hpp` | role: dipolar layer-correction wrapper behavior.
- `src/python/espressomd/magnetostatics.py` | role: user-facing magnetostatics API wrappers.
