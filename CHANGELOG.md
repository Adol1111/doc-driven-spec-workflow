# Changelog

All notable changes to this project are documented here.

This project follows Conventional Commits for commit history. Version headings describe user-facing workflow and installation changes, not every internal edit.

## 0.2.0 - Unreleased

Compared with `0.1.0` / remote baseline `3f104aa`, this release reorganizes the repository from a single workflow skill into a staged docs-driven skill set.

### Breaking Changes

- `docs-delivery-workflow` has been removed.
- `doc-driven-spec-workflow` is now the public root/router skill and should be used as the default workflow entry point.
- The former execution-stage meaning of `doc-driven-spec-workflow` has moved to `task-spec-execution`.
- Templates moved out of the root skill. Consumers that referenced `skills/doc-driven-spec-workflow/references/` directly should update paths.

### Migration Notes

- Use `doc-driven-spec-workflow` when you are unsure which workflow stage should run next.
- Replace direct usage of `docs-delivery-workflow` with `doc-driven-spec-workflow`.
- Replace direct current-task execution usage of `doc-driven-spec-workflow` with `task-spec-execution`.
- Keep installation commands pointed at the repository name: `Adol1111/doc-driven-spec-workflow`.
- If you copied templates manually, move execution templates to `skills/task-spec-execution/references/` and roadmap templates to `skills/milestone-planning/references/`.

### Added

- Added `milestone-planning` as a dedicated roadmap decomposition skill for deciding milestone boundaries, optional modules, task breakdown, delivery order, and task selection.
- Added `docs-workflow-bootstrap` for initializing the minimum docs scaffold before roadmap planning or current-task execution.
- Added `task-spec-execution` as the dedicated current-task execution skill for task-local specs, optional plans, readiness checks, implementation governance, verification, and branch closing.
- Added `skills/milestone-planning/references/roadmap-template.md` for roadmap-layer `docs/tasks/` documents.
- Added `skills/task-spec-execution/references/task-execution-template.md` for selected task directories and task-local metadata.

### Changed

- Reworked the public workflow chain to:

  ```text
  doc-driven-spec-workflow -> docs-workflow-bootstrap -> brainstorming -> milestone-planning -> task-spec-execution
  ```

- Updated README installation guidance to treat this repository as a multi-skill set.
- Simplified installation examples so users install from the repository and optionally select a skill by name.
- Clarified that users can enter through `doc-driven-spec-workflow` and then continue stage by stage when no approval gate is outstanding.
- Split template ownership by stage: roadmap templates belong to `milestone-planning`; execution templates belong to `task-spec-execution`; root routing owns no templates.

### Removed

- Removed `skills/docs-delivery-workflow/` after its routing responsibility moved to `skills/doc-driven-spec-workflow/`.
- Removed the old combined `tasks-template.md` to avoid mixing roadmap planning and current-task execution responsibilities.

## 0.1.0

Initial public docs-driven spec workflow baseline.
