# Uncertain Plan Trigger Asks Before Plan

## Prompt

Use doc-driven-spec-workflow.

The docs scaffold exists. `docs/tasks/m1-private-beta/index.md` says `Roadmap confirmed: yes`, and `docs/tasks/m1-private-beta/authentication/03-session-timeout-policy/task.md` is the selected current task with no blocking dependencies or prior checkpoints.

The task-local `spec.md` has been written and explicitly approved. The task might touch authentication middleware, browser session UI, and audit logging, but the docs do not yet make clear whether this is one straightforward policy change or cross-module coordination with non-obvious verification order.

The user now says:

continue
