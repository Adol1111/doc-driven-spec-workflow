# Planning Inbox Ready To Decompose

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that `Open Milestones` is empty but `planning-inbox.md` contains a candidate marked `ready to decompose`.
- Routes directly to `milestone-planning`.
- Treats the inbox candidate as a concrete short-term target for roadmap decomposition.
- Proposes or prepares to propose milestone/module/task boundaries with rationale.
- Does not detour into `superpowers:brainstorming` because the candidate is already ready for decomposition.

## Expected File Changes

None.

## Must Not

- Must not ask the generic planning mode question.
- Must not route to `superpowers:brainstorming`.
- Must not route directly to `task-preparation`.
- Must not write task-local `spec.md`.
- Must not start implementation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
