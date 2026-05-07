# Plan Commit Points Natural Boundaries

## Prompt

Use doc-driven-spec-workflow.

The docs scaffold exists. `docs/tasks/m1-private-beta/index.md` says `Roadmap confirmed: yes`, and `docs/tasks/m1-private-beta/api-compatibility/session-token-migration/task.md` is the selected current task with no blocking dependencies or prior checkpoints.

The task-local `spec.md` has already been written and explicitly approved. It requires six implementation sections: token parser compatibility, new token writer, persisted session migration, API response update, old-client compatibility verification, and cleanup of temporary compatibility notes.

The user now says:

continue and include sensible commit points in the plan
