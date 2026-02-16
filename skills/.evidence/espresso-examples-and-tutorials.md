# Evidence: espresso-examples-and-tutorials

## Primary docs
- `doc/tutorials/lattice_boltzmann/Readme.md`
- `doc/tutorials/ferrofluid/Readme.md`
- `doc/tutorials/raspberry_electrophoresis/Readme.md`
- `doc/tutorials/lennard_jones/Readme.md`
- `doc/tutorials/constant_pH/Readme.md`
- `doc/tutorials/widom_insertion/Readme.md`
- `doc/tutorials/polymers/Readme.md`
- `doc/tutorials/mlip/Readme.md`
- `doc/tutorials/grand_canonical_monte_carlo/Readme.md`
- `doc/tutorials/charged_system/Readme.md`
- `doc/tutorials/boltzmann_inversion/Readme.md`

## Primary source entry points
- `skills/espresso-examples-and-tutorials/references/doc_map.md`
- `src/walberla_bridge/src/lattice_boltzmann/InterpolateAndShiftAtBoundary.hpp`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/FieldAccessorsSinglePrecision.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/FieldAccessorsDoublePrecision.h`
- `src/walberla_bridge/src/lattice_boltzmann/ResetForce.hpp`
- `src/walberla_bridge/src/lattice_boltzmann/LBWalberlaImpl.hpp`
- `src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp`
- `src/walberla_bridge/src/lattice_boltzmann/lb_kernels.hpp`
- `src/walberla_bridge/src/lattice_boltzmann/CMakeLists.txt`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFSinglePrecisionCUDA.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFSinglePrecisionAVX.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFSinglePrecisionAVX.cpp`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFSinglePrecision.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFSinglePrecision.cpp`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFDoublePrecisionCUDA.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFDoublePrecisionAVX.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFDoublePrecisionAVX.cpp`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFDoublePrecision.h`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/UpdateVelFromPDFDoublePrecision.cpp`
- `src/walberla_bridge/src/lattice_boltzmann/generated_kernels/StreamCollideSweepThermalizedSinglePrecisionCUDA.h`

## Extracted headings
- Tutorial: lattice-Boltzmann
- Part 1: the lattice-Boltzmann method
- Physics learning objectives
- ESPResSo learning objectives
- Part 2: planar Poiseuille flow
- Part 3: sedimentation
- Tutorial: ferrofluids
- General Remarks
- Points to mention throughout the tutorial
- Tutorial: raspberry electrophoresis
- Tutorial: Lennard-Jones
- Tutorial: constant pH method

## Executable command hints
- (none extracted)

## Warnings and pitfalls
- - Importance of correct setup for non-biased results (especially important for magnetic systems!)
- * how to use an auto correlation function to estimate correlation times and how that affects error estimation
- Additionally the steepest descent algorithm can get trapped in local minima and the convergence criterion is system-dependent.
- * Estimating the correlation-corrected standard error of the mean of a time series
- * Name the three important regimes for polymer diffusion and the corresponding scaling laws
