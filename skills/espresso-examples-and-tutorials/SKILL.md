---
name: espresso-examples-and-tutorials
description: This skill should be used when users ask about examples and tutorials in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Examples and Tutorials

## High-Signal Playbook
### Route conditions
- Use this skill to choose the right tutorial track by physics objective and quickly start a realistic simulation pattern.
- Route environment/build blockers to `espresso-build-and-install` or `espresso-getting-started`.
- Route production execution flow, restart policy, and integrator sequencing to `espresso-simulation-workflows`.
- Route deep method/solver semantics to `espresso-sphinx` or `espresso-inputs-and-modeling`.

### Triage questions
1. Which physical problem class are you targeting (LJ, LB, ferrofluid, constant pH, Widom, GCMC, polymers, MLIP, charged systems)?
2. Do you need interactive notebooks or script-first execution?
3. Which methods must be included (electrostatics, reaction methods, LB, virtual sites)?
4. Which observable is the acceptance target (RDF, diffusion, magnetization, chemical potential, cluster statistics)?
5. How much runtime budget is available for sampling/equilibration?
6. Do you need uncertainty estimates corrected for correlation time?

### Canonical workflow
1. Map objective through `doc/tutorials/Readme.md`, then select a concrete topic README (for example `doc/tutorials/lennard_jones/Readme.md`).
2. Launch the tutorial notebook environment (`doc/tutorials/Readme.md`).
3. Run the baseline notebook/script unchanged to verify environment health.
4. Modify one parameter family at a time (interaction strength, pH, LB setup, etc.).
5. Track tutorial-specific observables and compare against stated physical expectations.
6. Use correlation-aware sampling windows where tutorials emphasize time-series statistics.
7. Port validated snippets into standalone scripts only after tutorial behavior is reproduced.

### Minimal working example
```bash
cd doc/tutorials
../../ipypresso lab
```

```python
import espressomd
import espressomd.lb
system = espressomd.System(box_l=[10, 20, 30])
system.time_step = 0.01
system.cell_system.skin = 0.4
lbf = espressomd.lb.LBFluid(agrid=1., density=1., kinematic_viscosity=1., tau=0.01)
system.lb = lbf
system.integrator.run(100)
```

### Pitfalls and fixes
- Ferrofluid dipole initialization can be biased if random orientation sampling is done incorrectly; use unbiased constructions described in `doc/tutorials/ferrofluid/Readme.md`.
- LJ overlap removal via steepest descent can stall in local minima; adapt convergence criterion and warmup strategy (`doc/tutorials/lennard_jones/Readme.md`).
- Treating correlated samples as independent underestimates uncertainty; estimate correlation times (`doc/tutorials/lennard_jones/Readme.md`, `doc/tutorials/polymers/Readme.md`).
- Constant-pH workflows have a limited safe regime; do not apply blindly across all pH values (`doc/tutorials/constant_pH/Readme.md`).
- For charged-system sweeps, remember ESPResSo supports one active system instance; reset relevant state between runs (`doc/tutorials/charged_system/Readme.md`).
- In constant-pH interpretation, neutralizing species is not always literal `H+`; keep chemistry mapping explicit (`doc/tutorials/constant_pH/Readme.md`).

### Convergence and validation checks
- Reproduce tutorial baseline plots/metrics before parameter sweeps.
- Ensure sampling intervals exceed correlation time for reported mean values.
- Compare measured trends against tutorial expectations (for example cluster trends, magnetization behavior, diffusion scaling).
- For coarse-graining tutorials, compare explicit-vs-effective model observables before accepting transferability.
- When using LB tutorials, verify profile/field outputs are consistent across repeated runs.

## Scope
- Handle questions about worked examples, tutorials, and cookbook usage.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
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

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `samples`
- `doc/tutorials`
- `testsuite/samples`
- `testsuite/tutorials`

## Test references
- `testsuite`
- `src/core/unit_tests`
- `src/instrumentation/tests`
- `src/particle_observables/tests`
- `src/script_interface/tests`
- `src/shapes/unit_tests`
- `src/utils/tests`
- `src/walberla_bridge/tests`
- `src/core/reaction_methods/tests`

## Optional deeper inspection
- `src`

## Source entry points for unresolved issues
- `src/walberla_bridge/src/lattice_boltzmann/lb_walberla_init.cpp` | LB module initialization used by tutorial-scale flows.
- `src/walberla_bridge/src/lattice_boltzmann/LBWalberlaImpl.hpp` | Main LB waLBerla implementation entry.
- `src/python/espressomd/reaction_methods.py` | Reaction-method APIs used in constant-pH/Widom/GCMC tutorials.
- `src/script_interface/reaction_methods/ReactionAlgorithm.cpp` | Script-interface reaction dispatch behavior.
- `src/core/reaction_methods/ReactionAlgorithm.cpp` | Core reaction move implementation path.
- `src/python/espressomd/interactions.py` | Interaction setup APIs reused across many tutorials.
- `src/script_interface/interactions/NonBondedInteraction.hpp` | Non-bonded interaction binding surface.
- `src/python/espressomd/electrostatics.py` | Electrostatics APIs used by charged-system tutorials.
- `src/script_interface/electrostatics/CoulombP3M.hpp` | Coulomb-P3M binding behavior.
- `src/python/espressomd/magnetostatics.py` | Magnetostatics APIs used in ferrofluid tutorials.
- `src/script_interface/magnetostatics/DipolarP3M.hpp` | Dipolar-P3M binding behavior.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
