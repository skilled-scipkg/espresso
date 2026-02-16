# Evidence: espresso-getting-started

## Primary docs
- `doc/tutorials/Readme.md`
- `doc/sphinx/introduction.rst`
- `samples/high_throughput_with_dask/Readme.md`
- `doc/tutorials/error_analysis/Readme.md`
- `doc/sphinx/particles.rst`
- `doc/sphinx/installation.rst`
- `doc/sphinx/appendix.rst`

## Primary source entry points
- `skills/espresso-getting-started/references/doc_map.md`
- `src/script_interface/cluster_analysis/ClusterStructure.hpp`
- `src/core/cluster_analysis/ClusterStructure.hpp`
- `src/core/cluster_analysis/ClusterStructure.cpp`
- `src/core/bond_error.hpp`
- `src/core/bond_error.cpp`
- `src/script_interface/cluster_analysis/initialize.hpp`
- `src/script_interface/cluster_analysis/initialize.cpp`
- `src/script_interface/cluster_analysis/CMakeLists.txt`
- `src/script_interface/cluster_analysis/Cluster.hpp`
- `src/script_interface/analysis/ObservableStat.hpp`
- `src/script_interface/analysis/ObservableStat.cpp`
- `src/script_interface/analysis/initialize.hpp`
- `src/script_interface/analysis/initialize.cpp`
- `src/script_interface/analysis/CMakeLists.txt`
- `src/script_interface/analysis/Analysis.hpp`
- `src/script_interface/analysis/Analysis.cpp`
- `src/python/espressomd/cluster_analysis.py`
- `src/core/observables/fetch_particles.hpp`
- `src/core/error_handling/RuntimeErrorStream.hpp`

## Extracted headings
- Tutorials for ESPResSo
- Overview
- Introductory tutorials
- Intermediate tutorials
- Advanced tutorials
- Using the tutorials
- Running the tutorials interactively
- Video lectures
- Introduction
- How to Use
- Technical Notes
- Tutorial: error analysis

## Executable command hints
- ./pypresso -c "import espressomd;print(espressomd.__version__)"
- Python environment tools may allow you to install a Python executable
- ./pypresso script.py
- mpirun -n 4 ./pypresso script.py
- ./pypresso

## Warnings and pitfalls
- * **Error analysis**
- * [Error Estimation in Time-Correlated Data](https://www.youtube.com/watch?v=I-HCxj9dUIU)
- In this section, a brief overview is given over the most important components
- become confusing and is thus error-prone. We therefore highly recommend using
- The probably most important choice is the length scale. A length of
- With regards to the stability of the Python interface, we have the following
- be extended. In important cases, the interface can change in such a way
- that using the old interface produces a clear error message and the
- These will go to the standard error stream.
- # Tutorial: error analysis
- confidence interval, standard error of the mean)
- * Integrate the ACF to determine the standard error of the mean
