---
name: docs-workflow-bootstrap
description: Initializes minimum docs-driven workflow entry points for a repository before roadmap planning or task-local execution docs exist. Use when repository is missing core docs scaffold files.
---

# Docs Workflow Bootstrap

## Quick start

Create only minimum docs scaffold. This skill does not own roadmap decomposition, task creation, task-local specs/plans, implementation, or branch closing. Stop after reporting created or changed files.

## Workflows

Create when missing:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- `docs/context/index.md`

Default content:

- `docs/index.md`: entry point + links
- `docs/architecture/index.md`: stable design boundaries
- `docs/tasks/index.md`: roadmap/task tracking + `Open Milestones` + `Completed Milestones` + planning inbox link
- `docs/tasks/planning-inbox.md`: unconfirmed goals/opportunities/candidates
- `docs/context/index.md`: research/supporting context

## Mandatory rules

- MUST keep bootstrap work in docs governance mode.
- MUST create only the minimum docs entry points unless the user explicitly asks for more.
- MUST NOT create implementation tasks during bootstrap.
- If the user provides actual roadmap or task content during bootstrap, record it only as compact `planning-inbox.md` candidate context when explicitly requested, then hand off to `milestone-planning`.
- MUST NOT create `docs/specs/`, `docs/plans/`, or task-local `spec.md` / `plan.md` by default.
- MUST report created or changed files and stop.
- Use repository doc language rules when available. Else follow current user language.

## Advanced features

After bootstrap, return to `doc-driven-spec-workflow` so it can choose the next stage. Continue directly only when the user explicitly asks:

- `milestone-planning` for milestone/module/task planning
- `task-preparation` for a concrete selected task in confirmed roadmap state with dependencies and prior hard gates clear

Otherwise stop after reporting the bootstrap result.
