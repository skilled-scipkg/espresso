# Evidence: espresso-sphinx

## Primary docs
- `doc/sphinx/Readme.rst`
- `doc/sphinx/inter_non-bonded.rst`
- `doc/sphinx/inter_bonded.rst`
- `doc/sphinx/constraints.rst`
- `doc/sphinx/system_manipulation.rst`
- `doc/sphinx/magnetostatics.rst`
- `doc/sphinx/community.rst`
- `doc/sphinx/under_the_hood.rst`
- `doc/sphinx/bibliography.rst`

## Primary source entry points
- `skills/espresso-sphinx/references/doc_map.md`
- `src/script_interface/constraints/HomogeneousMagneticField.hpp`
- `src/script_interface/constraints/fields.hpp`
- `src/script_interface/constraints/ExternalField.hpp`
- `src/script_interface/system/System.hpp`
- `src/script_interface/system/System.cpp`
- `src/script_interface/system/Leaf.hpp`
- `src/script_interface/system/initialize.hpp`
- `src/script_interface/system/initialize.cpp`
- `src/script_interface/system/CudaInitHandle.hpp`
- `src/script_interface/system/CudaInitHandle.cpp`
- `src/script_interface/system/CMakeLists.txt`
- `src/script_interface/magnetostatics/initialize.hpp`
- `src/script_interface/magnetostatics/initialize.cpp`
- `src/script_interface/magnetostatics/DipolarScafacos.hpp`
- `src/script_interface/magnetostatics/DipolarP3M.hpp`
- `src/script_interface/magnetostatics/DipolarLayerCorrection.hpp`
- `src/script_interface/magnetostatics/DipolarDirectSum.hpp`
- `src/script_interface/magnetostatics/Container.hpp`
- `src/script_interface/magnetostatics/CMakeLists.txt`

## Extracted headings
- optional: plot tabulated values
- two parallel plates oriented such that particles can only be found
- on the z-axis in the range [1.5, box_l - 1.5]

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- calculations should be used with great caution.
- caution when performing energy calculations. However, you can often
- and a background error will be raised.
- a background error will be raised.
- it is important how the bond is created. Particles need to be mentioned
- .. warning::
- cause |es| to throw an error is any distances between interacting particles and
- It is important to note that the error estimates given in :cite:`cerda08d`
- size, an error will be thrown.
- around 128KB. This is important since modern processors can issue
