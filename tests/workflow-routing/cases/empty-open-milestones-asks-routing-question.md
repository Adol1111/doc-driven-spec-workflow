# Empty Open Milestones Asks Routing Question

## Prompt

Use doc-driven-spec-workflow.

`docs/tasks/index.md` currently shows `Open Milestones: None`. Can you help me decide what we should do next?

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that an empty `Open Milestones` list is only a routing signal.
- Treats the situation as ambiguous because the prompt does not say whether a concrete short-term target already exists.
- Uses the first response to ask a routing question that distinguishes `roadmap alignment` from `direct decomposition`.
- Waits for the user's answer before recommending `superpowers:brainstorming` or decomposition.

## Expected File Changes

None.

## Must Not

- Must not immediately recommend `superpowers:brainstorming` as the next step.
- Must not immediately propose a new milestone, module, or task structure.
- Must not route directly to `task-spec-execution`.
- Must not start implementation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
