# ESPResSo source map: Inputs and Modeling

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `system`
- `box`
- `cell_system`
- `checkpoint`
- `h5md`
- `mpiio`
- `observables`
- `analysis`

## Fast source navigation
- `rg -n "box_l|periodicity|cell_system|skin" src/python/espressomd/system.py src/python/espressomd/cell_system.py src/core/cell_system`
- `rg -n "Checkpoint|register|save|load|signal" src/python/espressomd/checkpointing.py src/core/io src/script_interface/h5md src/script_interface/mpiio`
- `rg -n "Observable|Correlator|statistics|tau" src/python/espressomd/observables.py src/script_interface/analysis src/core/analysis`

## Function-level behavior checks
- System/decomposition setup path: `rg -n "System\(|periodicity|node_grid|decomposition" src/python/espressomd/system.py src/python/espressomd/cell_system.py src/core/cell_system/CellStructure.cpp`
- Checkpoint path: `rg -n "class Checkpoint|register|save|load" src/python/espressomd/checkpointing.py src/core/io/writer/h5md_core.cpp src/script_interface/h5md/h5md.cpp`
- MPI-IO path: `rg -n "mpiio|read|write" src/core/io/mpiio/mpiio.cpp src/script_interface/mpiio/initialize.cpp src/script_interface/mpiio/mpiio.hpp`
- Observable statistics path: `rg -n "ObservableStat|statistics_chain|mean|error" src/script_interface/analysis/ObservableStat.cpp src/core/analysis/statistics_chain.hpp`

## Suggested source entry points
- `src/python/espressomd/system.py` | role: top-level system property API.
- `src/python/espressomd/cell_system.py` | role: decomposition and cell-system controls.
- `src/core/cell_system/CellStructure.cpp` | role: runtime decomposition implementation.
- `src/core/BoxGeometry.hpp` | role: geometry and periodic boundary representation.
- `src/python/espressomd/checkpointing.py` | role: checkpoint registration/save/load API.
- `src/core/io/writer/h5md_core.cpp` | role: H5MD write path implementation.
- `src/script_interface/h5md/h5md.cpp` | role: Python binding for H5MD writer.
- `src/core/io/mpiio/mpiio.cpp` | role: MPI-IO implementation details.
- `src/script_interface/mpiio/mpiio.hpp` | role: MPI-IO binding interface.
- `src/python/espressomd/observables.py` | role: observable API used in modeling checks.
- `src/script_interface/analysis/ObservableStat.cpp` | role: observable statistics binding behavior.
- `src/core/analysis/statistics_chain.hpp` | role: statistics chain logic for analysis windows.
