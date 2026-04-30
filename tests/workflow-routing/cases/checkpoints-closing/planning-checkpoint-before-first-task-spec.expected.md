# Planning Checkpoint Before First Task Spec

## Expected Skill

`doc-driven-spec-workflow`, with correct review-pause sequencing across `milestone-planning` and `task-spec-execution`.

## Expected Behavior

- Explains that the first `continue` should accept the reviewed planning docs and move into task-local `spec.md` drafting for `01-login-session`.
- Makes clear that the planning-docs commit, if used, is part of that same first continuation rather than a separately approved gate.
- Explains that the second `continue` should approve the reviewed `spec.md` and move to the next routine task-execution step.
- Makes clear that the second `continue` should not jump straight into coding if a plan trigger, branch-isolation step, or other non-destructive operational step still comes first.
- Does not need to output the full completed `spec.md`; it is enough to state that drafting `spec.md` is the correct second-step action.
- Keeps implementation safety rules intact behind later plan/isolation/readiness steps as needed.

## Expected File Changes

None. This case checks checkpoint sequencing only; the prompt explicitly says not to draft the document body.

## Must Not

- Must not require a separate approval step whose only purpose is committing the reviewed planning docs.
- Must not require a third `continue` before starting `spec.md`.
- Must not say that the first `continue` should start implementation.
- Must not say that the second `continue` should perform destructive cleanup.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
