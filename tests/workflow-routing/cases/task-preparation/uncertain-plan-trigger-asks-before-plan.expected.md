# Uncertain Plan Trigger Asks Before Plan

## Expected Skill

`task-preparation`

## Expected Behavior

- Recognizes that plan trigger status is uncertain.
- Names the suspected trigger, such as cross-module coordination or non-obvious verification order.
- Asks whether to create task-local `plan.md` before writing it.
- Does not start implementation or create branch/worktree isolation yet.
- Keeps the workflow at the plan-trigger decision gate.

## Expected File Changes

None.

## Must Not

- Must not silently skip `plan.md`.
- Must not create `plan.md` without asking when trigger status is uncertain.
- Must not start implementation.
- Must not create a branch or worktree.
- Must not treat `continue` as approval for the uncertain plan decision.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
