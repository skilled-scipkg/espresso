# ESPResSo source map: Parallel and HPC

Generated from source roots:
- `src`

Use this map only after exhausting the topic docs in `doc_map.md`.

## Topic query tokens
- `mpi`
- `openmp`
- `gpu`
- `decomposition`
- `p3m`
- `walberla`
- `scaling`
- `performance`

## Fast source navigation
- `rg -n "MPI|OpenMP|omp|rank|domain|decomposition" src/core src/script_interface src/python/espressomd`
- `rg -n "P3M|tune|mesh|accuracy|heffte" src/core/p3m src/core/electrostatics src/python/espressomd/electrostatics.py`
- `rg -n "LBFluid|walberla|lattice_boltzmann" src/walberla_bridge src/script_interface/walberla src/python/espressomd/lb.py`

## Function-level behavior checks
- Decomposition checks: `rg -n "decomposition|node_grid|set_regular_decomposition|set_hybrid_decomposition" src/core/cell_system/CellStructure.cpp src/python/espressomd/cell_system.py`
- Electrostatics scaling path: `rg -n "tune|accuracy|mesh|heffte" src/core/p3m/TuningAlgorithm.cpp src/core/electrostatics/p3m_heffte.cpp src/python/espressomd/electrostatics.py`
- LB parallel path: `rg -n "LBFluid|checkpoint|vtk|kernel" src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp src/walberla_bridge/src/lattice_boltzmann/lb_kernels.hpp src/script_interface/walberla/LBFluid.cpp`

## Suggested source entry points
- `src/core/cell_system/CellStructure.cpp` | role: decomposition/state orchestration across ranks.
- `src/core/cell_system/RegularDecomposition.cpp` | role: regular decomposition policy.
- `src/core/cell_system/HybridDecomposition.cpp` | role: hybrid decomposition policy.
- `src/core/p3m/TuningAlgorithm.cpp` | role: P3M tuning and parameter search behavior.
- `src/core/electrostatics/p3m_heffte.cpp` | role: distributed FFT electrostatics path.
- `src/core/electrostatics/p3m_gpu_cuda.cu` | role: GPU electrostatics kernel path.
- `src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp` | role: waLBerla LB initialization and wiring.
- `src/walberla_bridge/src/lattice_boltzmann/lb_kernels.hpp` | role: LB kernel dispatch declarations.
- `src/script_interface/walberla/LBFluid.cpp` | role: Python-facing LB fluid binding behavior.
- `src/script_interface/walberla/LatticeModel.hpp` | role: lattice model binding surface for walberla-backed paths.
- `src/python/espressomd/cell_system.py` | role: Python controls for decomposition configuration.
- `src/python/espressomd/electrostatics.py` | role: Python long-range solver APIs.
- `src/python/espressomd/lb.py` | role: Python LB APIs and runtime callbacks.
