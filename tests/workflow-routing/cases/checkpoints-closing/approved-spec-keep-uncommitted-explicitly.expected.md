# Approved Spec Keep Uncommitted Explicitly

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that the user explicitly approved the allowed alternative to keep the approved task-local docs uncommitted.
- Treats the task spec checkpoint as resolved by explicit uncommitted approval.
- Reports which file remains uncommitted, such as the task-local `spec.md`.
- States which checkpoint gate that decision satisfies.
- Proceeds only to implementation readiness or branch/worktree isolation after making the uncommitted checkpoint state explicit.

## Expected File Changes

None.

## Must Not

- Must not demand a commit as the only possible checkpoint resolution.
- Must not silently carry uncommitted docs forward without reporting the affected files.
- Must not treat vague `continue` alone as this approval; the approval must be explicit.
- Must not start implementation before readiness and isolation gates.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
