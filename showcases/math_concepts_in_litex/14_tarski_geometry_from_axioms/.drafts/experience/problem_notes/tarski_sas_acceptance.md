# Acceptance: direct obtain cleanup and SAS

## Task context

- Task: remove redundant existential echoes, record the general proof-style
  rule, and add side-angle-side triangle congruence.
- Scope: the Tarski showcase, its handwritten Lean analogy, its local design
  notes and proof journal, plus the `litex-proof-writer` skill.

## Before

Six witness constructions store an existential fact and immediately repeat
the same expression as the source of `obtain`. The Chapter 11 surface can state
angle congruence and prove Euclid I.5, but it does not yet expose the standard
SAS consequence.

## Intended behavior

- Use `obtain x from exist x T st {...}` directly when `obtain` is the sole
  consumer; do not keep the identical standalone existential.
- Add the same rule to `litex-proof-writer` and validate the updated skill.
- Follow GeoCoq's `cong2_conga_cong`: exact `CongA`, congruence of the two
  sides adjacent to the angle, and no hidden third-side premise imply
  congruence of the opposite sides.
- Expose the resulting three side equalities through the existing `Cong3`
  relation.
- Keep the primitive data and axiom settings unchanged. Reusable Chapter 2/4
  lemmas needed by the source proof are allowed; global axioms, `trust`, and
  kernel changes are not.

## Explicit non-goals

- Complete Chapter 4 or Chapter 11 theorem parity with GeoCoq.
- Replacing exact witness-based angle congruence with a numerical angle or an
  SSS abbreviation.
- Requiring the two-dimensional or Euclidean parallel axioms for SAS.

## Evidence required

- Persistent-session blocks verify every cleanup and new theorem before
  materialization.
- Clean Litex file and module gates pass, and the Lean analogy compiles.
- The Litex and Lean surfaces contain no trust or proof holes.
- A deletion probe demonstrates that the derived third side is live in the
  final `Cong3` theorem.

## Compatibility boundary

Existing declarations and theorem statements remain stable. The cleanup
changes proof bodies only; SAS and its reusable source-aligned foundations are
additive.

## Outcome

- Removed the redundant standalone existential echoes from
  `between_trivial`, `between_symmetric`, `degenerate_segments_congruent`, and
  all four I.5 witness constructions. Direct `obtain` forms pass the release
  verifier.
- Added and validated the corresponding direct-`obtain` rule in
  `litex-proof-writer`.
- Added `between_exchange`, `point_has_strict_extension`, exact IFSC,
  `segment_congruence_addition`, `inner_five_segment`,
  `side_angle_side_gives_third_side`, and `triangle_congruence_sas`.
- Kept I.5 neutral. SAS uses only the neutral axioms plus decidable point
  equality; neither upper dimension nor the Euclidean parallel axiom occurs in
  its setting prefix.
- Replayed all 64 source-order blocks through `inner_five_segment` in a fresh
  pre-SAS session. Folding `Cong3` without the derived third side then failed
  exactly at definition clause 2, `Cong(a,c,a2,c2)`, proving that the third-side
  derivation is live.
- Cold Litex file and module gates, the handwritten Lean compilation, skill
  validation, JSON validation, and trust/proof-hole scans all pass.
