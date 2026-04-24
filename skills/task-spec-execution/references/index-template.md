# Index Template

Use for non-roadmap `docs/` index files to explain directory purpose, entry points, and usage.

Roadmap-layer `docs/tasks/` indexes belong to `milestone-planning/references/roadmap-template.md`.

## `docs/index.md`

```md
# Documentation Index

`docs/` is the main documentation entry point, organized by stable design, working specs, optional plans, task tracking, and context references.

## Sections

- [Architecture](./architecture/index.md)
  Stable design documents and behavior boundaries.
- [Specs](./specs/index.md)
  Working specs for the current task before implementation.
- [Plans](./plans/index.md)
  Optional implementation plans for genuinely complex tasks.
- [Tasks](./tasks/index.md)
  Project-level milestones, modules, task status, dependencies, and history.
- [Context](./context/index.md)
  Research notes, samples, references, and conclusions that are not yet stable.

## Usage

- Read `architecture/` first when you need stable system behavior.
- Read `tasks/` first when you need roadmap, task status, or next-step guidance.
- Read `context/` for research notes or external references.
- Read or write `specs/` before starting implementation.
- Create `plans/` only when the task is genuinely complex or multi-step.
```

## `docs/architecture/index.md`

```md
# Architecture Index

This directory stores long-lived design documents that define system behavior and implementation boundaries.

## Documents

- [Some Topic](./some-topic.md)
  Explain which behavior boundaries the document covers.

## Notes

- Prefer stable design here rather than temporary research or task status.
```

## `docs/context/index.md`

```md
# Context Index

This directory stores research notes, validation notes, and references.

## Current Research

- [Some Research](./some-research.md)
  Explain the purpose of this research note.

## Maintenance Rules

- Move stable conclusions to `docs/architecture/`
- Do not write current task status here
```

## `docs/specs/index.md`

```md
# Working Specs

This directory stores design specs created before implementation begins.

## Naming

- Use `YYYY-MM-DD-<topic>-design.md`
- Use short English kebab-case for `<topic>`
- Example: `2026-04-16-chat-fixed-user-context-design.md`

## Role

- Use specs to record goals, boundaries, approach, and verification before implementation.
- Follow the `task-spec-execution` skill and its reference templates for task-local spec structure and writing guidance.
- Move stable long-term constraints into `docs/architecture/`.

## Lifecycle

- Create new specs before implementation starts, and get user approval before coding.
- Create a corresponding `docs/plans/` document only when the task is genuinely complex or multi-step.
```

## `docs/plans/index.md`

```md
# Working Plans

This directory stores detailed implementation plans for complex tasks.

## Naming

- Use `YYYY-MM-DD-<feature-name>.md`
- Use short English kebab-case for `<feature-name>`
- Example: `2026-04-16-chat-fixed-user-context.md`

## Role

- Create plans only when the task is genuinely complex or multi-step.
- Use plans to break down implementation slices, file scope, and verification without repeating the approved spec.
- Follow the `task-spec-execution` skill and its reference templates for task-local plan structure and writing guidance.

## Lifecycle

- Wait for user approval after writing the plan before starting implementation.

## Relationship To `docs/tasks/`

`docs/plans/` is the detailed execution entry point. `docs/tasks/` records milestone, module, task status, dependencies, and historical indexing only. If a project task has a corresponding plan here, link to it from the task's `Source` or `Notes` instead of copying the full execution steps.
```

## Rules

- `index.md` should explain what the directory is, what it contains, and how to use it.
- `index.md` is for navigation and conventions, not detailed implementation for a single task.
- Use `milestone-planning/references/roadmap-template.md` for `docs/tasks/index.md`, milestone indexes, and module indexes.
