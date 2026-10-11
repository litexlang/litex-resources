# Closed Sets and Compactness Acceptance

## Before

The topology showcase stopped at composition of continuous maps. Continuity
was stated directly over two topology-setting bundles, so later theorems had
no single reusable setting for a map between two spaces.

## Now

- `TopologicalMapSetting` composes the source topology, target topology, and
  function.
- `ContinuousMapSetting` adds the open-preimage law, and `is_continuous`
  consumes that setting while retaining its flat external parameters.
- `continuous_map_has_closed_preimages` and
  `closed_preimages_imply_continuous` prove the two directions of the standard
  closed-set characterization.
- `is_compact_subset` uses indexed open covers and finite index subsets.
- `continuous_image_of_compact_is_compact` proves that
  `fn_range(fn(x K) Y {f(x)})` is compact whenever `K` is compact and `f` is
  continuous.

## Boundary

The language currently rejects a named theorem whose target itself is a
`forall ... <=>:` fact. The closed-set characterization is therefore exposed
as two adjacent named directional theorems. No `trust`, local axiom, custom
preimage constructor, or custom union constructor was added.

## Evidence

`target/release/litex -compact -runner -f showcases/math_concepts_in_litex/topology/main.lit`
returns exit code `0` and top-level `ok: true`.
