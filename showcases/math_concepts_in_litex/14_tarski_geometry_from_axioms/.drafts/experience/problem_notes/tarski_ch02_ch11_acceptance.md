# Acceptance: Tarski Chapters 2–11 foundation

## Task context

- Task: Build the GeoCoq Chapters 2–11 foundation and prove isosceles base
  angles in Litex.
- Scope: Showcase 14 public Litex file, handwritten Lean analogy, local design
  notes, proof journal, and release gates.
- Related workspace: `showcases/math_concepts_in_litex/14_tarski_geometry_from_axioms`

## Before

The showcase exposes the SST axiom hierarchy, proves segment-congruence
reflexivity and symmetry, and defines collinearity and midpoint. It has no angle
relation and cannot state Euclid I.5 in its source-faithful form.

## Intended behavior

- Keep `Point`, `Bet`, and `Cong` as the only primitive mathematical data.
- Add source-aligned relations corresponding to GeoCoq Chapters 2–11.
- Prove only the minimal neutral theorem chain needed to reach Euclid I.5;
  definition-use probes are sufficient for Chapter 5, 8, 9, and 10 interfaces.
- Define angle congruence by GeoCoq Definition 11.2, not by an SSS abbreviation.
- Check `isosceles_triangle_has_equal_base_angles` under
  `TarskiNeutralDimensionlessSetting`; it must not require the 2D or Euclidean
  extensions.
- Construct the exact angle witnesses directly with segment construction and
  five-segment. General midpoint existence is a later Chapter 8 result and is
  not required by this tracer.
- Keep the public implementation in one chapter-marked `main.lit` and mirror
  the mathematical statements in `same_math_in_lean.lean`.

## Explicit non-goals

- Complete theorem parity with every GeoCoq Chapter 2–11 file.
- Coordinates, numerical lengths or angles, circles, continuity, and parallel
  theory.
- A selected midpoint function before existence and uniqueness support it.
- Any new Litex kernel rule or global axiom.

## Evidence required

- Persistent-session proof journal contains every candidate proof block.
- `target/release/litex -compact -runner -f .../main.lit` succeeds.
- `target/release/litex -compact -runner -r .../14_tarski_geometry_from_axioms`
  succeeds.
- The Lean analogy compiles with the repository's configured Lean gate.
- Source and Lean analogy contain no `trust`, global `axiom`, `abstract_prop`,
  `sorry`, or `admit`.
- A liveness audit removes at least one real dependency from the final tracer
  and observes verification failure.

## Compatibility boundary

Existing predicate and setting names remain stable. New relations are additive.
The public claim is a minimal foundation corresponding to the chapter sequence,
not a port of the complete GeoCoq library.

## Outcome

Accepted on 2026-08-18. The source-ordered Chapter 2–11 interface and exact
`are_angles_congruent` relation are materialized in the single public
`main.lit`. `isosceles_triangle_has_equal_base_angles` verifies under only
`TarskiNeutralDimensionlessSetting`. Three sequential fresh file gates and one
fresh module gate returned `ok=true`; the handwritten Lean analogy also passed
`lake env lean`. Removing the final `five_segment` selection caused the exact
four-witness congruence clause to remain unknown, confirming that the final
mathematical dependency is live.

## Solved verifier experience: name the whole conditional rule

The first cold-replay form left the five-segment implication anonymous inside
the setting. Even after naming only its conclusion, repeated fresh runs could
alternate between success and:

```text
unknown result: $five_segment_result(Point, Cong, q5, q7, q6, q8)
```

The stable active formulation packages the complete implication:

```litex
prop satisfies_five_segment(Point set, Bet power_set(cart(Point, Point, Point)), Cong power_set(cart(Point, Point, Point, Point))):
    forall q1, q2, q3, q4, q5, q6, q7, q8 Point:
        $are_segments_congruent(Point, Cong, q1, q3, q2, q4)
        $are_segments_congruent(Point, Cong, q3, q5, q4, q6)
        $are_segments_congruent(Point, Cong, q1, q7, q2, q8)
        $are_segments_congruent(Point, Cong, q3, q7, q4, q8)
        $is_between(Point, Bet, q1, q3, q5)
        $is_between(Point, Bet, q2, q4, q6)
        q1 != q3
        =>:
            $are_segments_congruent(Point, Cong, q5, q7, q6, q8)
```

`TarskiNeutralDimensionlessSetting` carries this transparent proposition, and
the public `five_segment` theorem selects it. This does not strengthen the
source axiom; it gives the same universally quantified implication a stable
name. Acceptance used three sequential fresh file runs and one module run:

```bash
target/release/litex -compact -runner -f showcases/math_concepts_in_litex/14_tarski_geometry_from_axioms/main.lit
target/release/litex -compact -runner -r showcases/math_concepts_in_litex/14_tarski_geometry_from_axioms
```

Reusable lesson: when an anonymous conditional primitive replays
nondeterministically, name the entire transparent implication rather than only
its conclusion.
