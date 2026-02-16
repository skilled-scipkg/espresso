# Evidence: espresso-inputs-and-modeling

## Primary docs
- `doc/sphinx/visualization.rst`
- `doc/sphinx/system_setup.rst`
- `doc/sphinx/io.rst`
- `doc/sphinx/ek.rst`
- `doc/sphinx/analysis.rst`
- `doc/sphinx/advanced_methods.rst`

## Primary source entry points
- `skills/espresso-inputs-and-modeling/references/doc_map.md`
- `src/core/field_coupling/ForceField.hpp`
- `src/core/unit_tests/field_coupling_force_field_test.cpp`
- `src/script_interface/cluster_analysis/ClusterStructure.hpp`
- `src/core/cluster_analysis/ClusterStructure.hpp`
- `src/core/cluster_analysis/ClusterStructure.cpp`
- `src/core/cell_system/CellStructureType.hpp`
- `src/core/cell_system/CellStructure.hpp`
- `src/core/cell_system/CellStructure.cpp`
- `src/core/system/ResourceCleanup.hpp`
- `src/walberla_bridge/src/utils/boundary.hpp`
- `src/core/immersed_boundary/ImmersedBoundaries.hpp`
- `src/core/immersed_boundary/ImmersedBoundaries.cpp`
- `src/core/immersed_boundary/ibm_volcons.hpp`
- `src/core/immersed_boundary/ibm_triel.hpp`
- `src/core/immersed_boundary/ibm_triel.cpp`
- `src/core/immersed_boundary/ibm_tribend.hpp`
- `src/core/immersed_boundary/ibm_tribend.cpp`
- `src/core/immersed_boundary/ibm_common.hpp`
- `src/core/immersed_boundary/ibm_common.cpp`

## Extracted headings
- You may consider creating a video with ffmpeg:
- ffmpeg -f image2 -framerate 30 -i 'screenshot_%05d.png' output.mp4
- Particle type 0 is red, type 1 is blue (type 2 is red etc)..
- Particle type 0 is gold, type 1 is blue (type 2 is gold again etc).
- Registers timed calls of foo()
- Callbacks to control temperature
- Registers input-based calls with keys Y and H
- ... set system properties like time_step here ...
- ...
- signal.SIGINT: signal 2, is sent when ctrl+c is pressed
- ... add particles here
- show metadata only

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- allowed and result in an error. This behavior is inherited, so the same applies
- A runtime error will be triggered during integration when running a
- ranks) will throw an error.
- *WARNING*: Do not attempt to read these binary files on a machine
- necessarily throwing an error.
- On 1 MPI rank, the simulation will halt with a python runtime error.
- Important: these VTK files are written in multi-piece format, i.e. each MPI
- assuming the ``image_box`` values were properly set up. This is important to
- The implementation for computing averages and error estimates of a time series
- resulting in a non-negligible systematic error. A more general
- Here we set up a system and its most important parameters. The ``skin``
- depth tunes the system's performance. The one important thing a user needs to know
