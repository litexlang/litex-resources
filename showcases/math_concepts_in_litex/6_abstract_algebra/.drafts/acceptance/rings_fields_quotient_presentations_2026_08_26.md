# Abstract-algebra vertical-slice acceptance

## Before

The published module ended with the group-homomorphism kernel-normality
theorem. Ring, ideal, quotient-presentation, domain, and field interfaces were
absent.

## After

The group slice remains intact. The new checked chain is:

```litex
setting CommutativeRingSetting(...)
setting RingHomomorphismSetting(...)
prop is_ideal(...)
prop is_prime_ideal(...)
setting QuotientRingPresentationSetting(...)

thm ring_homomorphism_kernel_is_ideal
thm prime_ideal_gives_integral_domain_quotient
thm integral_domain_quotient_gives_prime_ideal
thm integers_form_a_commutative_ring
```

The quotient is deliberately a supplied presentation: a surjective ring
homomorphism whose kernel is exactly `I`. No equivalence-class carrier or
quotient-existence claim is smuggled into the interface. The two flagship
theorems prove the prime-ideal/domain characterization in both directions.

## Boundary

The accepted stop line excludes a general quotient construction,
maximal-ideal/quotient-field correspondence, finite-field classification,
polynomial/PID/UFD theory, modules, field extensions, and Galois theory.
Algebraic geometry, homological algebra, representation theory, model theory,
and universal algebra are collection non-goals.

## Verification

- release file runner: top-level `ok: true`, exit 0
- release module runner: top-level `ok: true`, exit 0
- direct `trust`, `axiom`, and `abstract_prop`: none added

Persistent framed sessions were attempted first and hit a repeatable liveness
limit while serializing deeply expanded settings. The identical source passed
the release file runner; the journal records the fallback and the one repaired
fact-shape issue (`neg(zero)=zero` moved out of an irrelevant universal
binder).
