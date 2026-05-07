# Implementation Complete Commits Before Review

## Expected Skill

`task-execution-simple`

## Expected Behavior

- Recognizes that implementation execution has reached the post-verification commit point.
- Commits the verified implementation work on the dedicated task branch before asking for implementation review.
- Treats implementation review as review of the committed task branch or merge diff, not as permission to make an ordinary task commit.
- Does not ask the user for routine commit approval when there is no unrelated user work, failed verification, or hard gate.
- Stops after the commit for implementation review, before merge or destructive cleanup.

## Expected File Changes

None.

## Must Not

- Must not leave verified implementation work uncommitted while asking for review.
- Must not route back to `task-preparation`.
- Must not start another task.
- Must not merge, delete branches, or remove worktrees before implementation review.
- Must not commit unrelated user changes.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
