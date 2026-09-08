---
name: skill-manager
description: 実行証拠から再利用可能な汎用 multi-agent skill guidance を抽出し、global skill の監査・候補化・最終検証・承認済み変更を管理する。実行logからskill候補を探す、既存skillを最適化する、または新規skillをsemantic・behavioralに検証するときに使う。product architecture、backlog、CentralDockyard 固有の task-service/runtime-service/system assertion、repo-local tests/runner は対象外。
---

# Skill Manager

Preserve confirmed agent lessons as concise, durable skill guidance. Follow the
active repository and host instructions; this skill does not replace them.

## Modes

- `log-skill-discovery`: inspect execution evidence for repeated behavior,
  prompt boilerplate, missing guidance, and reusable workflow lessons.
- `existing-skill-optimization`: inspect a current skill for unnecessary prose,
  duplicated mechanics, misplaced resources, and context-heavy read paths.
  Read [refactor-placement.md](references/refactor-placement.md) before changing
  placement.
- `new-skill-final-check`: after a new skill is drafted and mechanically valid,
  verify its behavior and side effects before reporting it complete.

Stop at a proposal when the finding belongs to product architecture, backlog
shaping, runtime implementation, or another system owner.

## Stage contract

- `DISCOVERY`: inspect and report evidence-backed findings; stop without a gate
  or edit when no exact candidate is requested.
- `CANDIDATE`: define one exact bundle and separate mechanical validation,
  semantic/behavioral gate, and human approval. Gate success is not approval.
- `APPLY`: edit only after unambiguous approval for that exact bundle.
- `FINAL-CHECK`: run mechanical checks, then semantic/behavioral validation,
  then any repository-local governance checks.

## Workflow

1. Read the target skill, its direct references, applicable repository
   instructions, and the evidence that exposed the problem. State missing
   sources rather than filling them with assumptions.
2. Group findings into a small set of reusable themes. Separate skill guidance
   from scripts, runtime changes, product work, and one-off local corrections.
3. Prepare one exact candidate bundle with affected paths, evidence, expected
   impact, risk, and validation.
4. For `existing-skill-optimization`, run `$instruction-validity-gate` on the
   exact candidate before approval or application. Mechanical validation does
   not replace semantic/behavioral validation or human approval.
5. Propose only an `APPLY` bundle. Obtain text approval that unambiguously
   refers to it before editing, unless the current user request already grants
   that exact authority.
6. Apply only the approved skill changes. Do not create a parallel approval
   store or silently expand the bundle.
7. For `new-skill-final-check`, run the system `quick_validate.py` on the draft,
   then run `$instruction-validity-gate` before finalization. After a
   gate-driven rewrite, rerun both in that order.
8. Rerun the gate when applied text differs materially from the passing
   candidate. Material changes may alter trigger, scope, authority, workflow,
   success or stop conditions, dependencies, or observed behavior; formatting
   and spelling alone are not material.
9. Treat `HOLD` as unfinished and report missing evidence. For `REJECT`, make a
   bounded rewrite within the gate's retry limit or discard the candidate. If
   the gate cannot be loaded, stop at `HOLD`; do not copy its protocol here.
10. Run focused validation and every applicable repository governance check.
    Commit only when the user and repository workflow authorize it.

## Placement

Read [refactor-placement.md](references/refactor-placement.md) for placement
decisions. Keep repository-specific commands, paths, role routing, and service
policy in repository instructions or references, not in this global skill.

## Validation

Use system `skill-creator` guidance for skill changes. Validate every changed
folder containing `SKILL.md` with:

```text
cmd /c py -3 -X utf8 C:\Users\sedho\.codex\skills\.system\skill-creator\scripts\quick_validate.py <skill-folder>
```

`quick_validate.py` is mechanical validation only; keep semantic/behavioral
validation, human approval, and repository-local governance checks separate.
For shared references, validate each consuming skill. For executable helpers,
run the smallest direct syntax or behavior check. Read
[agent-guidance-test-policy.md](references/agent-guidance-test-policy.md) before
adding or changing agent-guidance tests.
