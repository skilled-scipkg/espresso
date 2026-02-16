---
name: espresso-sphinx
description: This skill should be used when users ask about sphinx in ESPResSo; it prioritizes documentation references and then source inspection only for unresolved details.
---

# ESPResSo: Sphinx

## High-Signal Playbook
### Route conditions
- Use this skill when questions are anchored in Sphinx manual chapters: interactions, constraints, system manipulation, magnetostatics, and internals.
- Route onboarding and first-run setup to `espresso-getting-started`.
- Route run orchestration and restart sequencing to `espresso-simulation-workflows`.
- Route IO/checkpoint format decisions to `espresso-inputs-and-modeling`.
- Route tutorial selection by domain objective to `espresso-examples-and-tutorials`.

### Triage questions
1. Is the question about non-bonded, bonded, constraints, system manipulation, or magnetostatics?
2. Which compile-time features are required for the requested method?
3. What box geometry/periodicity is assumed (especially for dipolar solvers)?
4. Which particle types/interactions need to be active together?
5. Are shape-based constraints near periodic boundaries?
6. What target accuracy/tolerance is required for long-range solvers?
7. Is behavior mismatch at setup time, integration time, or post-processing time?

### Canonical workflow
1. Map the request to the exact chapter via `doc/sphinx/index.rst`, then open the matching chapter file (for example `doc/sphinx/inter_non-bonded.rst`).
2. Start from minimal setup snippets for the requested interaction/constraint type.
3. Check feature prerequisites before runtime (`doc/sphinx/inter_non-bonded.rst`, `doc/sphinx/magnetostatics.rst`).
4. Attach solver/constraints and run a short integration sanity loop.
5. Validate geometric assumptions (box shape, constraint placement, periodic image behavior).
6. Tune accuracy/cutoff/mesh only after the baseline run is stable.
7. Escalate to source entry points when docs leave API ambiguity.

### Minimal working example
```python
system.non_bonded_inter[0, 0].wca.set_params(epsilon=1., sigma=2.)
```

```python
import espressomd.shapes
import espressomd.magnetostatics as magnetostatics
wall = espressomd.shapes.Wall(normal=[0, 0, 1], dist=1.5)
system.constraints.add(shape=wall, particle_type=0)
p3m = magnetostatics.DipolarP3M(prefactor=1, mesh=32, accuracy=1E-4)
system.magnetostatics.solver = p3m
```

### Pitfalls and fixes
- Shapes extending outside the central box are truncated by box boundaries; place geometry intentionally (`doc/sphinx/constraints.rst`).
- Shape constraints do not interact with periodic images; keep shapes farther from boundaries than cutoff to avoid discontinuities (`doc/sphinx/constraints.rst`).
- Negative-distance violations with non-penetrable constraints stop simulations; inspect `min_dist` and geometry setup (`doc/sphinx/constraints.rst`).
- Harmonic/quartic bonds with cutoff report broken bonds and background errors when exceeded (`doc/sphinx/inter_bonded.rst`).
- Dipolar P3M does not support non-cubic boxes (`doc/sphinx/magnetostatics.rst`).
- Dipolar P3M tuned error estimates assume homogeneous systems; actual force/torque errors can be larger in inhomogeneous states (`doc/sphinx/magnetostatics.rst`).
- DLC requires a particle-free slab in `z`; entering particles trigger errors (`doc/sphinx/magnetostatics.rst`).
- Tabulated interaction tables must have matched `force`/`energy` lengths and sensible resolution to avoid poor interpolation/performance (`doc/sphinx/inter_non-bonded.rst`).

### Convergence and validation checks
- Interaction sanity: short-run energies/forces are finite and no immediate background errors occur.
- Constraint sanity: `min_dist` remains physically consistent for constrained particle types.
- Solver sanity: dipolar accuracy target is checked against a tighter-reference run on a small system.
- Geometry sanity: solver assumptions (cubic vs slab) match simulation box and active correction scheme.
- Table sanity: tabulated potentials reproduce expected analytical trend on sampled points.

## Scope
- Handle questions about documentation grouped under the 'sphinx' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `doc/sphinx/Readme.rst`
- `doc/sphinx/inter_non-bonded.rst`
- `doc/sphinx/inter_bonded.rst`
- `doc/sphinx/constraints.rst`
- `doc/sphinx/system_manipulation.rst`
- `doc/sphinx/magnetostatics.rst`
- `doc/sphinx/community.rst`
- `doc/sphinx/under_the_hood.rst`
- `doc/sphinx/bibliography.rst`

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
- `src/script_interface/constraints/initialize.cpp` | Registration of constraint classes in Python interface.
- `src/script_interface/constraints/ShapeBasedConstraint.hpp` | Shape-constraint binding behavior.
- `src/script_interface/constraints/ExternalField.hpp` | External-field constraint wrapper.
- `src/script_interface/constraints/HomogeneousMagneticField.hpp` | Homogeneous magnetic-field constraint wrapper.
- `src/script_interface/system/System.cpp` | System-level binding methods used across Sphinx examples.
- `src/script_interface/system/initialize.cpp` | System binding initialization and export.
- `src/script_interface/magnetostatics/initialize.cpp` | Magnetostatics binding registration.
- `src/script_interface/magnetostatics/DipolarP3M.hpp` | Dipolar P3M script-interface wrapper.
- `src/script_interface/magnetostatics/DipolarLayerCorrection.hpp` | DLC wrapper and parameters.
- `src/script_interface/magnetostatics/DipolarDirectSum.hpp` | Direct-sum magnetostatics wrapper.
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src`).
