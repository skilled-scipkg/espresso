---
name: espresso-simulation-workflows
description: This skill should be used when users ask about simulation workflows in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Simulation Workflows

## High-Signal Playbook
### Route conditions
- Use this skill for execution flow: launch mode, integrator/thermostat sequencing, MC/MD coupling, and restart handling.
- Route compile/configure/dependency issues to `espresso-build-and-install`.
- Route system definition, IO format, and checkpoint payload details to `espresso-inputs-and-modeling`.
- Route tutorial selection by physics domain to `espresso-examples-and-tutorials`.
- Route detailed interaction/solver manual semantics to `espresso-sphinx`.

### Triage questions
1. Are you running single-rank, MPI, or hybrid MPI+OpenMP?
2. Which integrator and thermostat pair is intended?
3. Are reaction methods involved (`ReactionEnsemble`, `ConstantpHEnsemble`, `WidomInsertion`)?
4. Is restart reproducibility required across checkpoint boundaries?
5. Are LB/EK VTK callbacks and field outputs part of the workflow?
6. Are failures numeric instabilities, runtime exceptions, or launch/tooling issues?
7. Is strong scaling expected from algorithms that may be rank-0 limited?

### Canonical workflow
1. Start from documented launch path (`./pypresso simulation.py`) and only then move to MPI syntax (`doc/sphinx/running.rst`).
2. Explicitly set integrator/thermostat pair and verify compatibility (`doc/sphinx/integration.rst`).
3. Use steepest descent for overlap removal, then switch back to velocity-Verlet (`doc/sphinx/integration.rst`).
4. Configure reaction methods with required bookkeeping/setup (`doc/sphinx/reaction_methods.rst`).
5. Couple MC reaction attempts and MD integration with a safe exclusion range for interacting systems (`doc/sphinx/reaction_methods.rst`).
6. Add optional LB/EK VTK callbacks for periodic/on-demand diagnostics (`doc/sphinx/lb.rst`, `doc/sphinx/ek.rst`).
7. On restart, reuse old forces when required by coupling/checkpoint semantics (`doc/sphinx/integration.rst`, `doc/sphinx/lb.rst`).
8. Validate workflow stability through short observables windows before long production runs.

### Minimal working example
```bash
./pypresso simulation.py
mpiexec -n 4 ./pypresso simulation.py
```

```python
import espressomd.reaction_methods as reaction_methods
cpH = reaction_methods.ConstantpHEnsemble(kT=1, exclusion_range=1., seed=77)
cpH.add_reaction(gamma=K_diss,
                 reactant_types=[0], reactant_coefficients=[1],
                 product_types=[1, 2], product_coefficients=[1, 1],
                 default_charges={0: 0, 1: -1, 2: +1})
```

### Pitfalls and fixes
- Reaction methods require energy support for all active interactions; unsupported interactions break MC moves (`doc/sphinx/reaction_methods.rst`).
- Reaction-method state is not checkpointable (RNG state limitation); design workflows accordingly (`doc/sphinx/reaction_methods.rst`).
- Particle creation/deletion in reactions can invalidate contiguous ID assumptions; avoid index==id logic (`doc/sphinx/reaction_methods.rst`).
- Runtime error `"particle type X is currently not tracked"` requires `system.setup_type_map(type_list=[X])` (`doc/sphinx/reaction_methods.rst`).
- Constant-pH assumptions can generate artifacts when reservoir interpretation is violated (`doc/sphinx/reaction_methods.rst`).
- Widom insertion implementation is canonical-ensemble specific; not directly valid for fluctuating-N or NpT formulas (`doc/sphinx/reaction_methods.rst`).
- Small `exclusion_range` in interacting systems can destabilize integration; set around particle diameter (`doc/sphinx/reaction_methods.rst`).
- Steepest descent with active thermostat is undefined and raises errors (`doc/sphinx/integration.rst`).
- LB restart without `reuse_forces=True` can break momentum conservation and induce COM drift (`doc/sphinx/lb.rst`).
- Some algorithms (for example reaction methods) are effectively rank-0 in parts of execution; do not over-assume MPI speedup (`doc/sphinx/running.rst`).

### Convergence and validation checks
- Stability check: no force/energy blow-ups after integrator and thermostat are activated.
- MC/MD coupling check: acceptance behavior and target observables stabilize after warmup.
- Restart check: post-restart observables agree with uninterrupted reference windows.
- Ensemble check: method assumptions (canonical vs constant-pH vs reaction ensemble) match study design.
- IO check: VTK/H5 outputs parse correctly and agree with in-memory samples for short runs.

## Scope
- Handle questions about simulation setup, execution flow, and runtime controls.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/tutorials/electrodes/Readme.md`
- `doc/tutorials/langevin_dynamics/Readme.md`
- `samples/gibbs_ensemble/Readme.md`
- `doc/sphinx/reaction_methods.rst`
- `doc/sphinx/running.rst`
- `doc/sphinx/lb.rst`
- `doc/sphinx/integration.rst`
- `doc/sphinx/magnetodynamics.rst`
- `testsuite/python/data/dancing.txt`

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
- `src/script_interface/reaction_methods/ReactionAlgorithm.cpp` | Script-interface dispatch for reaction algorithms.
- `src/script_interface/reaction_methods/ReactionEnsemble.hpp` | Python-facing reaction-ensemble API.
- `src/script_interface/reaction_methods/ConstantpHEnsemble.hpp` | Python-facing constant-pH API.
- `src/script_interface/reaction_methods/WidomInsertion.hpp` | Python-facing Widom insertion API.
- `src/script_interface/reaction_methods/SingleReaction.hpp` | Per-reaction setup objects.
- `src/script_interface/reaction_methods/initialize.cpp` | Registration of reaction-method bindings.
- `src/core/reaction_methods/ReactionAlgorithm.cpp` | Core MC reaction workflow implementation.
- `src/core/reaction_methods/ReactionEnsemble.hpp` | Core reaction-ensemble behavior.
- `src/core/reaction_methods/ConstantpHEnsemble.hpp` | Core constant-pH behavior.
- `src/core/reaction_methods/WidomInsertion.hpp` | Core Widom insertion calculations.
- `src/python/espressomd/reaction_methods.py` | High-level Python wrapper methods and defaults.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
