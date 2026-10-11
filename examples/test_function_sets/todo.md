# Function-set retained capability boundaries

> **统一收尾入口：** [src收尾总清单.md](../../plan/src收尾总清单.md)（2026-10-04）。活动事项及跨来源去重在总清单维护；本页保留专项代码、决定和历史验收。新增进展应同步对应总清单ID，不能用旧快照覆盖新证据。

## Current disposition

2026-10-06 user clarification: every well-defined Litex object satisfies
is_set, including 1, so power_set(1) is legitimate. The former input-domain
question is closed. The ten retained probes need definition/carrier tracing
at distinct consumers; five field probes fail WD before value search.
[Contract correction and inspected owners](experience/problem_notes/object-definition-carrier-contract-2026-10-06.md).

**2026-10-06 search-contract update:** Function/body/carrier/coordinate and analogous structural lookup is now restricted to declarations and exact-object properties. The current 85-case suite still matches; CAP_T05 accepts directly. Other original inputs remain observations, not mathematical rejection contracts. [Current implementation and gate record](experience/problem_notes/exact-property-structural-lookup-2026-10-06.md). The dated counts below describe the October 4 snapshot.

The user's 2026-10-04 decisions are implemented and verified. The supported
suite now matches **85/85 cases** (58 positives, 27 negatives), the 42 selected
Rust tests pass, and the old fn_set Obj file plus three negatives pass. The
nine explicit authoring routes are ordinary regression expectations. Their
original direct source and the exact field-premise source are ten independent
observations; all ten rejected in that October 4 snapshot, without being counted as mathematical
negative tests. No automatic kernel repair is scheduled for these boundaries.

Current evidence: [acceptance.md](acceptance.md),
[cleanup_2026-10-04.json](cleanup_2026-10-04.json),
[capabilities_2026-10-04.json](capabilities_2026-10-04.json),
[cleanup_tests_2026-10-04.json](cleanup_tests_2026-10-04.json) and
[proof_journals/cleanup_2026-10-04.json](proof_journals/cleanup_2026-10-04.json).
The earlier [explicit_proofs_2026-10-04.json](explicit_proofs_2026-10-04.json)
and [proof_journals/explicit_bridges_2026-10-04.json](proof_journals/explicit_bridges_2026-10-04.json)
remain historical 82-case receipts. The current observational disposition
supersedes the earlier provisional `kernel_problem` classification.

## Closed cleanup work

- Every existing failed-template result variant is projected to its actual
  child phase/reason in Normal and Detailed output; real stage/goal, failed
  publication, later-definition and Chinese-output tests pass. N26 checks
  `body_have_equal`, `membership` and `a $in Z` in the production CLI.
- The normal suite uses the supported explicit routes. Capability observations
  remain inventoried separately, with `matches: null` rather than PASS labels.
- Old fn_set.lit P04 uses a valid template-selected fixed-carrier family. N27
  preserves the invalid `let F = fn(x R) x` rejection; the separate
  dependent_codomain.lit migration was outside this task and has subsequently
  been accepted independently by Round14 (EX01 is now closed).

## Solved authoring routes

- T05: P01 verifies `shift_two(3) = \shift<2>(3) = 5`.
- H05: P03 verifies `add_two(3) = add(2)(3) = 5`.
- S02: P04 first identifies the anonymous callable field, then supplies its
  application as an intermediate object in the equality chain.
- T03/D05: P05 proves `\maps<R, Z> = fn(x R) Z` before membership and binding.
- D08/D09: P02/P06 expose the tuple, declare a typed local `&Box` object,
  identify its field function, and verify the numeric call. P06 also preserves
  the original final result-membership goal.
- S07/S08: P07/P08 verify the general `(f, 0) $in &Box` constructor fact for
  `f fn(x R) R` before defining the closure-valued template/function. They then
  use tuple equality and a typed local result to verify the callable field.
  No trust or carrier weakening was used.

N22–N24 reject false numeric values in the new equality chains. N25 rejects
an invalid struct tag even after the general constructor fact is checked.
All 27 negative controls remain rejected at their expected phase after
successful setup; all eight explicit positive routes and the P09 successful
template tracer verify.

## Observed boundaries; no automatic repair scheduled

### Immediate selected/returned struct field syntax

The user's exact source:

```litex
struct Box:
    op fn(x R) R
    tag N
have fn step(x R) R = x + 1
template<a R>:
    have box &Box = (step, 0)
\box<2> = (step, 0)
\box<2>.op(3) = step(3) = 4
```

Observed: the tuple equation succeeds; the final chain fails `well_defined`
because the receiver has no definition-time struct carrier for `op`. Both
`\box<2>.op = step` and `\box<2>.op $in fn(x R) R` fail before equality
search, including when membership comes first. Adding only downstream
numeric proof steps cannot solve that WD boundary. P02's typed binding is the
current working interface; it explicitly checks `selected.op $in fn(x R) R`
as well as the field equation. P06 supplies the corresponding function-result
interface. These proofs do not make the original immediate syntax legal.

If immediate syntax is requested later, establish the intended field-view
contract first. Do not infer a struct view from arbitrary later memberships,
add state, change protected AST shapes, or broaden search merely to erase this
probe failure. This follow-up does not decide whether automatic derivation of
the declared return view should be part of that contract.

### Historical closure-specific definition observations

The earlier S07 template `def_template` and S08 `body_in_return_set` failures
are historical. The Oct5 frozen-binary receipt shows both original setup
definitions succeeding; their first remaining failure is the subsequent
field WD. Do not keep those old definition failures as current blockers.
P07/P08's checked general constructor fact remains an accepted explicit route,
with the same closure and `&Box` carrier. This clarification identifies no new
binder-matching cause and makes no fresh live-source execution claim.

### Direct value and specialized-carrier search

T05/H05/S02 and T03/D05 still reject without their explicit equalities at
search_proof or have_equal. Their checked routes select the intended body or
carrier and preserve the original mathematical value. Under the user's proof
contract, automatic expansion of these paths is not required for successful
authoring. The earlier numeric enhancement remains accepted, with no broader
implicit-search commitment added by this follow-up.

## Test-entry observation

- **Test-entry correction:** the earlier name-reservation observation came
  from manually calling `parse` followed by `exec_stmt`. That helper bypasses
  the production `run_litex_code` parse-name transaction. The production owner
  rolls names back on soft failure and errors; existing binding-lifecycle
  tests cover retries. Do not list the helper's same-name ParseError as a
  confirmed CLI defect. A fresh template-specific CLI recheck was blocked by
  four concurrent eval/JSON compile errors; no old binary was substituted.

The previous stable 85/85 and 42-test receipts remain dated acceptance, not a
claim that later shared-source edits currently compile.
