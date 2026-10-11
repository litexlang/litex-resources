# Field-first linear algebra acceptance

Registered implementation:
`showcases/math_concepts_in_litex/5_linear_algebra/main.lit`.

## Before

The public linear-map interface fixed both carriers and all operations to one
coordinate example:

```litex
# prop is_linear_map_R2_to_R(T fn(v cart(R, R)) R):
#     forall u, v cart(R, R):
#         T(vector_add(u, v)) = T(u) + T(v)
#     forall a R, v cart(R, R):
#         T(scalar_mul(a, v)) = a * T(v)
```

Former limitation: field and vector-space structure were absent from the
executable API, so the kernel theorems were statements only about
`cart(R,R) -> R`.

## Now

The executable public order is now field-first and carrier-generic:

```litex
struct Field<K nonempty_set>:
    zero K
    one K
    add fn(x, y K) K
    neg fn(x K) K
    mul fn(x, y K) K
    inv fn(x K) K
    <=>:
        # field laws

struct VectorSpace<K, V nonempty_set>:
    field &Field<K>
    zero V
    add fn(x, y V) V
    smul fn(a K, x V) V
    <=>:
        # LADR vector-space laws

thm linear_map_sends_zero_to_zero:
    ? forall K, V, W nonempty_set,
        source &VectorSpace<K, V>, target &VectorSpace<K, W>,
        T fn(v V) W:
        $is_linear_map(K, V, W, source, target, T)
        =>:
            T(source.zero) = target.zero
```

The same abstract layer proves kernel closure and both directions of
`injective iff kernel = zero_subspace`. The final consumer is the checked
`projection_x_axis : cart(R,R) -> cart(R,R)` over `real_field` and
`real_plane`; its kernel is nontrivial and it is not injective.

## Boundary

The migration changes this standalone showcase's mathematical interfaces; it
does not add Litex syntax, kernel rules, a shared `std` hierarchy, bases,
dimension, or rank-nullity.

## Evidence

```sh
target/release/litex -compact -runner -f showcases/math_concepts_in_litex/5_linear_algebra/main.lit
target/release/litex -compact -runner -r showcases/math_concepts_in_litex/5_linear_algebra
lean showcases/math_concepts_in_litex/5_linear_algebra/same_math_in_lean.lean
```

- Release file runner: top-level `ok: true`, exit code 0.
- Release module runner: top-level `ok: true`, exit code 0.
- Prelude-only Lean analogy: exit code 0.
- Published Litex/Lean sources: no direct `trust`, local `axiom`, `sorry`, or
  `admit` (anchored declaration scan returned no matches).
- Proof-liveness audit: zero preservation reaches `add_left_cancel`; kernel
  closure reaches `scalar_times_zero_vector`; the forward injectivity theorem
  uses `by extension`; the reverse theorem constructs `vector_sub`, proves its
  kernel membership, and cancels; the concrete projection invokes the generic
  kernel-subspace theorem.
