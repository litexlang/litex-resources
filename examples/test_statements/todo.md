# Statement-suite issues

> **统一收尾入口：** [src收尾总清单.md](../../plan/src收尾总清单.md)（2026-10-04）。活动事项及跨来源去重在总清单维护；本页保留专项代码、决定和历史验收。新增进展应同步对应总清单ID，不能用旧快照覆盖新证据。

## Latest bounded repair — 2026-10-04

FN07's checked function-field preimage/range/indexed application omissions and
GEO03's nonzero-real square positivity search are repaired (category 2).
46 affected Rust tests, 22 CLI controls, one complete alias proof, seven file
tracers, 378 Stmt checks and 175 basic checks pass. A frozen one-file power-rule
comparison measures 56.470s to 10.623s on the original diagnostic prefix.
These are scoped gates; full release/geo/replay status is not replaced.
[Completed experience](experience/problem_notes/field-preimage-and-power-2026-10-04.md)
and [acceptance](../../tests/tooling/acceptance/field-preimage-and-power-2026-10-04.md).

## Earlier conversation retest — 2026-10-04

The strict cache bypass is fixed under the maintainer's no-trust confirmation.
Direct/transitive trusted false theorems reject after ordinary cache warmup;
valid imports and ordinary cache hits remain checked. Automatic ordinary/strong
induction now passes the original bare input following a concurrent checked
inference repair. The original geometry solution passes with four explicit
`release obj def` lines; its mathematical goal is unchanged.

Final stable Rust lib is 829/830, integration 1/1, module regressions 26/26.
That historical failed unused-K expectation is now closed by the maintainer:
the original expression remains executable as a positive, with genuinely
incompatible field-carrier/value controls. See the
[current solution and 955/955 full Rust gate](experience/problem_notes/unused-struct-parameter-test-cleanup-2026-10-05.md). Frozen CLI cebcd1898772…
executes 50 leaves / 378 checks / 0 mismatches / 0 gaps, basic 175/175 and 22/22
clarification controls. Build and these gates have no captured source drift.

Tooling 18/18, phase 871/871 and formal Markdown 225/225 belong to the earlier
[retest snapshot](../../tests/tooling/acceptance/conversation-closeout-retest-2026-10-04.md),
not a fresh full-release gate. Nested contra remains the previously known
feature limit; complete collector maintenance belongs to Codex testing work,
not six new maintainer semantic decisions. [Current acceptance](../../tests/tooling/acceptance/conversation-clarifications-2026-10-04.md).
The Oct3 checkpoint below is historical and does not override these runs.

The new source-owned routes are [ByInducStmt](bugs/by_induc_stmt/limitations.md),
[DefStructStmt](bugs/def_struct_stmt/limitations.md),
[strict import cache](../module_manager/strict_cache_policy/README.md), and
the existing by-contra/tooling notes. Completed consumer, authoring and error
forwarding repairs are in the [experience record](experience/problem_notes/conversation_retest_local_repairs_2026-10-04.md).

## Historical current-source checkpoint — 2026-10-03

The [conversation status recheck](../../docs/audits/conversation-issue-status-update-2026-10-03.md)
at source `c33784ee2fb188f6ef6b9184e2dfd116fde19602120887ea082a071fe0ece785`
has 356/377 expected outcomes, with 21 new failures around recursive function/algo
WD, templates, ordinary/strong induction and recursive evaluation. The previous
377-pass receipt and closed K-number findings below remain historical evidence,
not a current all-green claim. Actual workspace have_fn/by_induc files also fail.
Do not guess a common global-search cause from the count; locate the carrier/domain
proof owner before classifying repair scope. Exact sources and outputs are in the
[checkpoint journal](proof_journals/conversation_issue_status_update_2026-10-03.json).

## Task context

- Task: per-statement regression suite requested on 2026-10-01; issue organization requested on 2026-10-02.
- Scope: examples/test_statements.
- Related workspace: golitex.

No K-number execution/verifier reproduction remains open. K005 now has a checked explicit by-contra proof and [durable acceptance](experience/problem_notes/K005-classified-negative-existence-contra.md). K004 now uses the user's [explicit arithmetic chain](experience/problem_notes/K004-explicit-recursive-increment-chain.md); K010's [finite numeric carrier fix](experience/problem_notes/K010-finite-numeric-carrier.md) and D001's [display/replay fix](experience/problem_notes/D001-trust-have-display.md) have been removed from the open records. K001/K002 and the statement-boundary repairs have separate acceptance records. K003 is a user-classified capability limitation. K008 is explicitly excluded by the user; its decision lives in [K008-cart-excluded.md](experience/problem_notes/K008-cart-excluded.md).

## Repair ownership (maintainer instruction, 2026-10-02)

Plans use two execution categories: **1 — improve Litex authoring**, and **2 — repair bounded local Rust semantics**. Codex completes authorized work in both categories, including verification and open-record cleanup, without another maintainer permission or code-review round. Changes to nonlocal contracts require discussion before implementation. An unknown cause/scope stays provisional while Codex investigates it; category, cause, and acceptance status are distinct.

### 1 — Litex authoring improvement

No confirmed open authoring-only issue remains in this suite. K003/K004 are accepted examples: the explicit chain `f(1) = f(1 - 1) + 1 = 0 + 1 = 1` preserves the original goal. Their successful fixtures and rejection controls remain in ordinary coverage; they are not Rust-repair requests.

### 2 — Local Rust semantic repairs and follow-on feature work

K005 is closed: enumeration, explicit NotExist contradiction and final citation
pass without trust. False goals, real witnesses, wrong carriers, missing
exclusion evidence and witness-scope controls remain checked. The original
bare shortcut is an expected-failure automatic-search limitation. See the
[solution](experience/problem_notes/K005-classified-negative-existence-contra.md).

The later all-fact feature request is tracked separately in
[ByContraStmt](bugs/by_contra_stmt/limitations.md) and
[the plan](../../plan/迁移的plan/by-contra-all-facts.md). Existing classified
routes, including ExistUnique/QF iff constructions, are implemented and
focused tests pass. The concrete impossible-field change was authorized and
implemented; its final gate status is in the linked plan. Nested quantified
Fact representation still requires discussion. Unified NotFact was rejected
and is withdrawn.

K010 remains another accepted category-2 example.

## Rechecked internal control

The formerly failing `stored_facts_and_zero_depth_strategy_calculation_remain_available` test now passes (1 passed, 0 failed, exit 0). Its stale open folder has been removed; the prior failure and exact recheck are preserved in the [recheck note](experience/problem_notes/known-only-control-recheck.md) and journal. This task established no causal repair attribution and did not rerun all seven builtin-policy tests.

## Related Stmt migration plan

The broader [50-leaf Stmt audit](../../plan/迁移的plan/stmt-execution-legacy-parity-audit.md#修复分工与当前待办2026-10-02) separately records B18 and B20–B23, with the same execution categories and discussion boundary. Its implementation/acceptance checkpoints are not additional confirmed native-input gaps in this suite.

Current restrictions, strict-policy boundaries, authoring mistakes, and tooling drift are in the matching `limitations.md` notes linked by the index. They are not counted as additional confirmed bugs. The original organization task did not repair problems. The subsequent K001 special-property redesign promoted that unchanged reproduction to ordinary success coverage.

```bash
python3 examples/test_statements/run.py --require-no-gaps
```

This gate remains failing while any manifest gap is open. D001's completed acceptance includes displayed-statement replay, beyond the execution success flag. No trust was inserted to discharge unresolved cases. See the local proof journals for chronological authoring, comparisons, and structured verification evidence.

## Broader gate findings

The [additional gate records](bugs/README.md#additional-kernel-gate-observations-2026-10-03) retain historical WD and detailed-node observations. The squared-i example is now closed by the maintainer's accepted explicit chain; its original automatic-route observations remain historical evidence, not a pending Rust request. Current acceptance and surviving decisions are maintained in the canonical closeout list.
