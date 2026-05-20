# Planning Checkpoint Before First Task Spec

## Expected Skill

`doc-driven-spec-workflow`, with correct review-pause sequencing across `milestone-planning` and `task-preparation`.

## Expected Behavior

- Explains that the first `continue` should accept the reviewed planning docs and perform the routine planning-doc checkpoint.
- Makes clear that the planning-doc commit is routine follow-up, not a separately approved hard gate.
- Makes clear that after that checkpoint, the workflow can move into `task-preparation` on the next forward-motion reply.
- Does not need to spell out the full second-step wording, but must not imply that another approval is needed only for the planning-doc commit.
- Does not need to output the full completed `spec.md`; it is enough to state that drafting `spec.md` is the correct second-step action.
- Keeps implementation safety rules intact behind later plan/isolation/readiness steps as needed.

## Expected File Changes

None. This case checks checkpoint sequencing only; the prompt explicitly says not to draft the document body.

## Must Not

- Must not require a separate approval step whose only purpose is committing the reviewed planning docs.
- Must not require a third `continue` before entering `task-preparation` and starting `spec.md`.
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
