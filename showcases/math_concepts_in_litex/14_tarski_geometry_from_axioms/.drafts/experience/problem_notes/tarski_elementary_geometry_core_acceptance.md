# Acceptance contract: elementary Tarski geometry core

Status: in progress

## Task context

- Task: implement the common elementary-geometry theorem families requested
  for the point-only Tarski showcase.
- Scope: public Litex source, handwritten Lean analogy, mathematical design,
  proof journal, dependency probes, and release gates.
- Related workspace:
  `showcases/math_concepts_in_litex/14_tarski_geometry_from_axioms`

## Confirmed decisions

- Keep `Point`, `Bet`, and `Cong` as the primitive mathematical data.
- Preserve GeoCoq's exact witness-based `CongA`, `Par_strict`, and inclusive
  `Par` meanings; do not replace them by coordinates, slopes, numerical
  angles, or SSS aliases.
- Keep the hierarchy additive: neutral, neutral with decidable equality, 2D,
  then Euclidean 2D.
- Admit no public `trust`, global `axiom`, `abstract_prop`, Lean `sorry`, or
  Lean `admit`.
- Build the theorem family in verified phases because the Chapter 6/11 angle
  transport chain is a real mathematical dependency, not administrative glue.

## Acceptance examples

The exact SSS bridge must verify without redefining angle congruence:

```litex
thm triangle_congruence_sss_gives_angles:
    ? forall [TarskiNeutralWithDecidableEqualitySetting], a, b, c, a2, b2, c2 Point:
        a != b
        c != b
        $are_triangles_congruent(Point, Cong, a, b, c, a2, b2, c2)
        =>:
            $are_angles_congruent(Point, Bet, Cong, a, b, c, a2, b2, c2)
```

Central reflection must have a relational existence-and-uniqueness surface:

```litex
$is_point_reflection(Point, Bet, Cong, point, reflected1, center)
$is_point_reflection(Point, Bet, Cong, point, reflected2, center)
=>:
    reflected1 = reflected2
```

The Euclidean branch must expose a live dependency that is unavailable under
the upper-dimension plane setting alone:

```litex
$euclid_intersection_witness_exists(Point, Bet, a, b, c, e)
```

Chapter 12 must distinguish strict disjoint lines from GeoCoq's inclusive
parallel relation, which also admits coincident nondegenerate lines.

## Evidence required

- Every new Litex statement first passes a source-order release session in one
  literal outer `try:` block and is recorded in the JSON proof journal.
- Clean file and module runners return top-level `ok: true` and exit code `0`.
- `same_math_in_lean.lean` passes the real Lean kernel gate.
- Public Litex and Lean surfaces pass trust/proof-hole scans.
- Dependency weakening probes fail where expected.

## Checkpoint outcome

The current verified prefix includes exact SSS-to-angle, initial angle algebra,
triangle-congruence equivalence laws, same-ray algebra, fixed-ray segment
construction uniqueness, central-reflection existence and uniqueness,
perpendicular incidence projections, the 2D and Euclidean settings, exact
Chapter 12 parallel predicates, and the Euclid witness tracer. The remaining
angle-transport, vertical/supplementary-angle, ASA/AAS/RHS, general midpoint,
perpendicular-construction, and Playfair layers are tracked in the dated
project ledger and are not claimed complete here.

Checkpoint gates on 2026-08-18:

- Litex file runner: top-level `ok: true`, exit code `0`.
- Litex module runner: top-level `ok: true`, exit code `0`.
- Handwritten Lean analogy: `lake env lean` exit code `0`.
- JSON proof journal parse, trust/proof-hole scans, and `git diff --check`:
  all passed.
