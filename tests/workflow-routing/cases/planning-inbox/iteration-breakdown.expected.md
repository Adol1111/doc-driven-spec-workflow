# Iteration Breakdown

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the near-term delivery target is already concrete.
- Routes to `milestone-planning` instead of `superpowers:brainstorming`.
- Treats the request as direct decomposition of the current iteration.
- Proposes milestone/module/task boundaries with rationale.
- Stops after roadmap structure or task selection unless the user explicitly asks to continue.

## Expected File Changes

None.

## Must Not

- Must not route to `superpowers:brainstorming` just because roadmap details beyond this iteration are not discussed.
- Must not write task-local `spec.md`.
- Must not write task-local `plan.md`.
- Must not start implementation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
