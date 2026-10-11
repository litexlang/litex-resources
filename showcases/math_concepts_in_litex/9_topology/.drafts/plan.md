# Plan: Topology

## Reader promise

This project presents a topology as a collection of open subsets and uses
named settings to prove familiar theorems without packaging the ambient space
as a struct. The same setting bundles now supply parameters and laws to
predicates, theorem headers, and larger settings.

## First-version boundary

The first version covers:

- a candidate topology relation using native set objects and `family_union`;
- a `TopologicalSpaceSetting` for theorem-facing use;
- binary unions and three-way intersections of open sets;
- continuity defined by open preimages;
- a `ContinuousCompositionSetting` composed from three renamed topology
  bundles; and
- composition of continuous maps;
- closed subsets and both directions of the closed-preimage characterization
  of continuity;
- compact subsets via indexed open covers; and
- continuous images of compact subsets are compact.

It stops before bases, filters, separation axioms, subspace and product
topologies, connectedness, quotient spaces, and homotopy.

## Representation decision

The first version is settings-first. A topology is already an ordinary
`power_set(power_set(X))` object, while `is_topology_on` tests that candidate.
Settings provide the reusable ambient theorem context. A struct is reserved
for later work that must construct, transport, compare, or return entire
topological spaces.

## Acceptance

- `continuous_composition`, both closed-preimage directions, and
  `continuous_image_of_compact_is_compact` are checked without `trust`.
- Native set and function interfaces are used directly.
- The file and independent module release runners return top-level `ok: true`
  with exit code `0`.
