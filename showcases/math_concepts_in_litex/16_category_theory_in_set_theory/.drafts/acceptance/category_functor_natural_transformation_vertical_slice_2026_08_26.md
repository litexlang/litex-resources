# Category vertical-slice acceptance

## Before

The published module had flat category data, two finite category examples,
and no functor or natural-transformation interface.

```litex
# functor and natural-transformation settings absent
```

## After

The module now has one setting chain and checked constructions:

```litex
setting CategorySetting(...)
setting FunctorSetting(...)
setting NaturalTransformationSetting(...)

thm identity_functor_exists
thm composition_of_functors_exists
thm identity_natural_transformation_exists
thm vertical_composition_of_natural_transformations_exists
thm terminal_identity_functor_exists
```

`composition_is_associative_at` and `naturality_square_commutes` are named
mathematical properties, not proof-only adapters. The vertical-composition
proof uses local `let` names for the six object images, three arrow images,
and four components, with explicit bridges only at the public theorem
boundary.

## Boundary

The accepted stop line is categories, functors, natural transformations,
identity/composition, and a terminal-category consumer. Limits, colimits,
adjunctions, Yoneda, comma categories, monads, general functor categories,
proper classes, and universe hierarchies are excluded from this version.

## Verification

- release file runner: top-level `ok: true`, exit 0
- release module runner: top-level `ok: true`, exit 0
- direct `trust`, `axiom`, and `abstract_prop`: none added

Persistent framed sessions were attempted first. Deep expanded-setting traces
and one overlong PTY line hit bounded liveness/input limits; the exact
source-owned file was then checked by the release runner. The proof journal
preserves those failures and the accepted shapes.
