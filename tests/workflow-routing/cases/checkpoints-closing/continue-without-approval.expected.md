# Continue Without Approval

## Expected Skill

`doc-driven-spec-workflow` routes back to the current approval gate, or `task-spec-execution` enforces the spec approval stop point.

## Expected Behavior

- Recognizes that `continue` is not explicit spec approval.
- Restates that implementation is blocked until the user approves `spec.md`.
- Asks for explicit approval or requested edits.
- Keeps the work at the spec approval gate.

## Expected File Changes

None.

## Must Not

- Must not start implementation.
- Must not create `plan.md` unless the user approved the spec and a plan trigger is present.
- Must not run readiness checks.
- Must not create a branch or worktree.
- Must not treat `continue` as approval for spec, plan, branch closing, or destructive cleanup.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
