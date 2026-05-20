# Empty Open Milestones Asks Routing Question

## Expected Skill

`doc-driven-spec-workflow` asking the minimal routing question, or `milestone-planning` handling the same routing question after handoff.

## Expected Behavior

- Recognizes that an empty `Open Milestones` list is only a routing signal.
- Treats the situation as ambiguous because the prompt does not say whether a concrete short-term target already exists.
- Uses the first response to ask a routing question that distinguishes `roadmap alignment` from `direct decomposition`.
- Allows the thin root router to ask that question directly before naming a downstream stage.
- Waits for the user's answer before recommending `planning-clarification` or decomposition.

## Expected File Changes

None.

## Must Not

- Must not immediately recommend `planning-clarification` as the next step.
- Must not immediately propose a new milestone, module, or task structure.
- Must not route directly to `task-preparation`.
- Must not start implementation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
