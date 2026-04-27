# Complex Selected Task Needs Plan

## Prompt

Use doc-driven-spec-workflow.

The docs scaffold exists. `docs/tasks/m1-private-beta/index.md` says `Roadmap confirmed: yes`, and `docs/tasks/m1-private-beta/api-compatibility/02-session-token-migration/task.md` is the selected current task with no blocking dependencies or prior checkpoints.

The task-local `spec.md` has already been written and explicitly approved. It requires changing a persisted session token format, migrating existing sessions, keeping old and new tokens valid during a transition, updating the public API response shape, and verifying old/new client compatibility in a specific order.

The user now says:

continue
