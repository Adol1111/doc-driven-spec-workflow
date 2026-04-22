# Release Notes

User-facing workflow, installation, and migration changes are documented here.

This project follows Conventional Commits for commit history, but release notes focus on what users need to know when adopting or upgrading the workflow.

## v0.2.1

### Fixes

- `task-spec-execution` now treats branch closing as unresolved until a merged task branch is explicitly deleted or explicitly kept, even after worktree cleanup.
- `task-spec-execution` now points to `finishing-a-development-branch` for merge, PR, keep, discard, and cleanup decisions after implementation is complete.

### Notes

- Removing a worktree does not remove its merged task branch.
- If implementation is complete and Git integration remains, prefer using `task-spec-execution` together with `finishing-a-development-branch`.

## v0.2.0

### Features

- The workflow moved from one combined skill to a staged model:

  ```text
  doc-driven-spec-workflow -> docs-workflow-bootstrap -> brainstorming -> milestone-planning -> task-spec-execution
  ```

- Added `docs-workflow-bootstrap` for minimum docs scaffold initialization.
- Added `milestone-planning` for roadmap decomposition and task selection.
- Added `task-spec-execution` for task-local spec, optional plan, readiness, implementation governance, verification, and branch closing.
- `doc-driven-spec-workflow` became the public root entry point and stage router.
- The repository split stage ownership more clearly:
  - `docs-workflow-bootstrap` initializes the minimum docs scaffold.
  - `milestone-planning` owns roadmap decomposition.
  - `task-spec-execution` owns task-local spec/plan/readiness/execution flow.
- Template ownership moved out of the root skill:
  - roadmap templates live under `skills/milestone-planning/references/`
  - execution templates live under `skills/task-spec-execution/references/`

### Breaking Changes

- The old execution-stage meaning of `doc-driven-spec-workflow` moved to `task-spec-execution`.
- Replace old root-skill execution usage of `doc-driven-spec-workflow` with `task-spec-execution`.
- Do not use `task-spec-execution` to invent or reshape roadmap structure; use `milestone-planning` first.
- If you referenced `skills/doc-driven-spec-workflow/references/` directly, update those template paths.

## v0.1.0

Initial public docs-driven spec workflow baseline.
