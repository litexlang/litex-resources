# Plan: Abstract Algebra

## Reader promise

This project shows how ordinary theorems can be proved in an arbitrary group
without turning the ambient group into a field-projection exercise. Named
settings keep the carrier, operations, and laws visible as the reusable
theorem context.

## First-version boundary

The first version covers:

- a candidate group law relation on a supplied carrier and operations;
- a `GroupSetting` for theorem-facing use;
- cancellation and uniqueness of identity and inverse;
- a candidate group-homomorphism relation;
- a `GroupHomomorphismSetting` for two groups and a supplied map; and
- preservation of identity and inverse by a group homomorphism;
- subgroup and normal-subgroup predicates over the existing group setting; and
- the flagship theorem that a group homomorphism's kernel is normal.

It stops before cosets, quotient groups, group actions, rings, ideals, fields,
modules, presentations, and classification theorems.

## Representation decision

The first version is settings-first. `is_group` and
`is_group_homomorphism` test supplied data; settings expose those facts as
fresh universal theorem contexts. A `struct` becomes appropriate only when a
later theorem constructs, transports, compares, or returns a whole algebraic
system as a value.

## Acceptance

- `kernel_is_normal_subgroup` is checked without `trust`.
- Every public relation has a theorem-facing settings consumer.
- The file and independent module release runners return top-level `ok: true`
  with exit code `0`.
