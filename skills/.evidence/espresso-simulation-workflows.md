# Evidence: espresso-simulation-workflows

## Primary docs
- `doc/tutorials/electrodes/Readme.md`
- `doc/tutorials/langevin_dynamics/Readme.md`
- `samples/gibbs_ensemble/Readme.md`
- `doc/sphinx/reaction_methods.rst`
- `doc/sphinx/running.rst`
- `doc/sphinx/lb.rst`
- `doc/sphinx/integration.rst`
- `doc/sphinx/magnetodynamics.rst`
- `testsuite/python/data/dancing.txt`

## Primary source entry points
- `skills/espresso-simulation-workflows/references/doc_map.md`
- `src/script_interface/reaction_methods/ReactionEnsemble.hpp`
- `src/script_interface/reaction_methods/ConstantpHEnsemble.hpp`
- `src/core/reaction_methods/ReactionEnsemble.hpp`
- `src/core/reaction_methods/ConstantpHEnsemble.hpp`
- `src/script_interface/reaction_methods/WidomInsertion.hpp`
- `src/script_interface/reaction_methods/SingleReaction.hpp`
- `src/script_interface/reaction_methods/ReactionAlgorithm.hpp`
- `src/script_interface/reaction_methods/ReactionAlgorithm.cpp`
- `src/script_interface/reaction_methods/initialize.hpp`
- `src/script_interface/reaction_methods/initialize.cpp`
- `src/script_interface/reaction_methods/CMakeLists.txt`
- `src/python/espressomd/reaction_methods.py`
- `src/core/reaction_methods/WidomInsertion.hpp`
- `src/core/reaction_methods/utils.hpp`
- `src/core/reaction_methods/utils.cpp`
- `src/core/reaction_methods/SingleReaction.hpp`
- `src/core/reaction_methods/ReactionAlgorithm.hpp`
- `src/core/reaction_methods/ReactionAlgorithm.cpp`
- `src/core/reaction_methods/CMakeLists.txt`

## Extracted headings
- Tutorial: simulations of electrodes
- Physics learning objectives
- Part 1
- Part 2
- ESPResSo learning objectives
- Tutorial: Langevin dynamics
- Gibbs ensemble simulations using ESPResSo
- get the number of ranks
- re-assign the ranks
- create a VTK callback that automatically writes every 10 LB steps
- can be deactivated
- create a VTK callback that writes only when explicitly called

## Executable command hints
- python script for any task you want to perform with |es|. In this chapter,
- Python and Jupyter programs, although they are perfectly interchangeable
- Python script. To this end, the folder containing the python module
- ./pypresso simulation.py
- ./pypresso
- ./ipypresso console
- Python kernel stopped. If a cell takes too long to execute, you may interrupt
- Python IDE, namely the Python interpreter needs to be replaced.
- mpiexec -n 4 ./pypresso simulation.py
- ./pypresso script.py
- ./pypresso script.py 2>&1 | c++filt
- ./pypresso --tool script.py

## Warnings and pitfalls
- The value of the exclusion range does not affect the limiting result and it only affects the convergence and the stability of the integration.  For interacting systems,
- fatal error, it is necessary to use a debugger to investigate the issue.
- meaningful error messages, however these checks cannot always catch errors
- The resulting build will run slightly slower, but will produce an error
- names. If this is not sufficient to track down the source of the error,
- To catch a runtime error, use e.g. ``catch throw std::runtime_error``.
- The AddressSanitizer (ASAN) :cite:`serebryany12a` is a memory error detection
- Alternatively, one can use ``-D CMAKE_CXX_FLAGS="-fsanitize-undefined-trap-on-error"``
- Add option ``--error-exitcode 1`` to return an error code when issues are detected.
- is too high, the following warning will be emitted:
- Warning:
- (in terms of ``agrid``). This has important implications for the location of
