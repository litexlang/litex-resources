# Setting-first `main2.lit` design

## Goal

Add a parallel, registered `main2.lit` that develops the abstract beginning of
linear algebra without declaring or consuming any `struct`. The existing
`main.lit` remains the first-class-data presentation; `main2.lit` presents the
same mathematics as ambient theorem contexts.

## Central modeling decision

`FieldSetting` and `VectorSpaceSetting` are not mathematical objects that can
be stored or projected. They expand a theorem's ambient carriers, operations,
and laws into binders and assumptions. Consequently, theorem bodies use
`add_V(u, v)` and `smul_V(a, v)`, rather than `space.add(u, v)` and
`space.smul(a, v)`.

The nearest rejected design is a predicate-only API whose every theorem
manually repeats all carriers, operations, and laws. A predicate remains useful
for judgments such as `is_linear_map` and `is_subspace`, but settings carry the
reusable ambient context.

## Interface spine

```litex
setting FieldSetting(K nonempty_set, scalar_zero, scalar_one K, scalar_add fn(x, y K) K, scalar_neg fn(x K) K, scalar_mul fn(x, y K) K, scalar_inv fn(x K) K):
    scalar_zero != scalar_one
    forall x, y, z K:
        scalar_add(scalar_add(x, y), z) = scalar_add(x, scalar_add(y, z))
        scalar_mul(scalar_mul(x, y), z) = scalar_mul(x, scalar_mul(y, z))
        scalar_mul(x, scalar_add(y, z)) = scalar_add(scalar_mul(x, y), scalar_mul(x, z))
    forall x, y K:
        scalar_add(x, y) = scalar_add(y, x)
        scalar_mul(x, y) = scalar_mul(y, x)
    forall x K:
        scalar_add(scalar_zero, x) = x
        scalar_add(x, scalar_neg(x)) = scalar_zero
        scalar_mul(scalar_one, x) = x
    forall x K:
        x != scalar_zero
        =>:
            scalar_mul(x, scalar_inv(x)) = scalar_one

prop has_vector_space_laws(K, V nonempty_set, scalar_one K, scalar_add, scalar_mul fn(x, y K) K, zero_V V, add_V fn(x, y V) V, smul_V fn(a K, x V) V):
    forall x, y, z V:
        add_V(add_V(x, y), z) = add_V(x, add_V(y, z))
    forall x, y V:
        add_V(x, y) = add_V(y, x)
    forall x V:
        add_V(zero_V, x) = x
        exist y V st {add_V(x, y) = zero_V}
    forall a, b K, x V:
        smul_V(scalar_mul(a, b), x) = smul_V(a, smul_V(b, x))
        smul_V(scalar_add(a, b), x) = add_V(smul_V(a, x), smul_V(b, x))
    forall a K, x, y V:
        smul_V(a, add_V(x, y)) = add_V(smul_V(a, x), smul_V(a, y))
    forall x V:
        smul_V(scalar_one, x) = x

setting VectorSpaceSetting([FieldSetting(K, scalar_zero, scalar_one, scalar_add, scalar_neg, scalar_mul, scalar_inv)], V nonempty_set, zero_V V, add_V fn(x, y V) V, smul_V fn(a K, x V) V):
    $has_vector_space_laws(K, V, scalar_one, scalar_add, scalar_mul, zero_V, add_V, smul_V)

prop is_field_in_setting([FieldSetting])
prop is_vector_space_in_setting([VectorSpaceSetting])
```

`VectorSpacesSetting` deliberately binds one field followed by two vector
carriers and two operation triples. It cannot be expressed as two nested
`[VectorSpaceSetting(...)]` references while identifying their field binders:
explicit names in a setting reference currently introduce fresh binders, and
active-name collisions are rejected. One shared-field setting is therefore the
honest current Litex representation, not accidental duplication.

```litex
setting VectorSpacesSetting([FieldSetting(K, scalar_zero, scalar_one, scalar_add, scalar_neg, scalar_mul, scalar_inv)], V, W nonempty_set, zero_V V, add_V fn(x, y V) V, smul_V fn(a K, x V) V, zero_W W, add_W fn(x, y W) W, smul_W fn(a K, x W) W):
    $has_vector_space_laws(K, V, scalar_one, scalar_add, scalar_mul, zero_V, add_V, smul_V)
    $has_vector_space_laws(K, W, scalar_one, scalar_add, scalar_mul, zero_W, add_W, smul_W)

setting LinearMapSetting([VectorSpacesSetting], T fn(v V) W):
    forall u, v V:
        T(add_V(u, v)) = add_W(T(u), T(v))
    forall a K, v V:
        T(smul_V(a, v)) = smul_W(a, T(v))

prop is_linear_map_in_setting([LinearMapSetting])
```

## Tracer theorem

Ordinary proof spine:

1. Linearity gives `T(0 + 0) = T(0) + T(0)`.
2. Since `0 + 0 = 0`, cancel `T(0)` from
   `T(0) + T(0) = T(0) + 0`.

Former `struct`-oriented shape:

```litex
# forall source &VectorSpace<K, V>, target &VectorSpace<K, W>:
#     T(source.zero) = target.zero
# proof uses source.add, target.add, and projected zero fields
```

Setting-oriented target:

```litex
thm setting_linear_map_sends_zero_to_zero:
    ? forall [LinearMapSetting]:
        T(zero_V) = zero_W
```

The immediate use probe is the kernel:

```litex
template<V, W set, zero_W W, T fn(v V) W>:
    have setting_linear_kernel power_set(V) = {v V: T(v) = zero_W}

thm setting_linear_map_kernel_is_subspace:
    ? forall [LinearMapSetting]:
        $is_subspace_in_setting(..., \setting_linear_kernel<V, W, zero_W, T>)
```

## Implemented source-order proof blocks

1. `FieldSetting`.
2. `has_vector_space_laws`, `VectorSpaceSetting`, and the two judgment props.
3. `VectorSpacesSetting`, `LinearMapSetting`, and `is_linear_map`.
4. Left cancellation under `[VectorSpaceSetting]`, using a locally obtained
   additive inverse rather than publishing a negation selector.
5. Scalar-times-zero under `[VectorSpaceSetting]`.
6. Tracer theorem `setting_linear_map_sends_zero_to_zero`.
7. `is_subspace_in_setting`, `setting_linear_kernel`, and
   kernel-is-subspace.
8. Standalone real-field operations and their laws, without reusing a struct
   value from `main.lit`.
9. Standalone `R^2` operations and their vector-space laws.
10. X-axis projection, its linearity judgment, the instantiated
    kernel-is-subspace theorem, and kernel membership of `(0, 7)`.

The concrete layer also includes narrow operation-value theorems. Persistent
session failures showed that checked function definitions remained callable
but their defining equalities did not automatically replay inside deeper
nested claims. These theorems are verifier-facing bridges local to the concrete
instance; they do not alter the abstract Setting interface.

All exported names that could collide with `main.lit` use the `setting_`
prefix. Generic settings keep the conventional names `FieldSetting`,
`VectorSpaceSetting`, `VectorSpacesSetting`, and `LinearMapSetting` because no
such names currently exist in this showcase module.

## Acceptance and boundary

- `main2.lit` contains no `struct`, `trust`, or local `axiom`.
- `main.lit` remains unchanged.
- The focused release file runner returns top-level `ok: true`.
- The complete linear-algebra module runner returns top-level `ok: true` after
  registering `main2` after `main`.
- The example stops before bases, dimension, matrices, quotients, and
  rank-nullity.
- Settings are intentionally not advertised as replacements for first-class
  structures: they cannot be stored, returned, or projected as values.
