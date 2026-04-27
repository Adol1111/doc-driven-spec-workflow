# Planning Checkpoint Before First Task Spec

## Expected Skill

`doc-driven-spec-workflow`, with correct checkpoint sequencing across `milestone-planning` and `task-spec-execution`.

## Expected Behavior

- Explains that the first `continue` should resolve the task-planning docs checkpoint by committing the newly created planning docs.
- Explains that the second `continue` should move into task-local `spec.md` drafting for `01-login-session`.
- Makes clear that the second `continue` should begin drafting `spec.md` only, not commit `spec.md`, create `plan.md`, or start coding.
- Does not need to output the full completed `spec.md`; it is enough to state that drafting `spec.md` is the correct second-step action.
- Keeps implementation gated behind later spec approval.

## Expected File Changes

None. This case checks checkpoint sequencing only; the prompt explicitly says not to draft the document body.

## Must Not

- Must not skip the task-planning docs checkpoint on the first `continue`.
- Must not say that the second `continue` should commit `spec.md`.
- Must not say that the second `continue` should create or propose `plan.md`.
- Must not say that the second `continue` should start implementation.
- Must not require a third `continue` before starting `spec.md`.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
