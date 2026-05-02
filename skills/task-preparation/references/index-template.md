# Index Template

Use for non-roadmap `docs/` index files to explain directory purpose, entry points, and usage.

Roadmap-layer `docs/tasks/` indexes belong to `skills/milestone-planning/references/roadmap-template.md`.

## `docs/index.md`

```md
# Documentation Index

`docs/` is the main documentation entry point, organized by stable design, task tracking, task-local specs/plans, and context references.

## Sections

- [Architecture](./architecture/index.md)
  Stable design documents and behavior boundaries.
- [Tasks](./tasks/index.md)
  Project-level milestones, modules, task status, dependencies, history, and task-local specs/plans.
- [Context](./context/index.md)
  Research notes, samples, references, and conclusions that are not yet stable.

## Usage

- Read `architecture/` first when you need stable system behavior.
- Read `tasks/` first when you need roadmap, task status, or next-step guidance.
- Read `context/` for research notes or external references.
- Write task-local `spec.md` and optional `plan.md` inside the selected task directory under `tasks/`.
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

## Rules

- `index.md` should explain what the directory is, what it contains, and how to use it.
- `index.md` is for navigation and conventions, not detailed implementation for a single task.
- Use `skills/milestone-planning/references/roadmap-template.md` for `docs/tasks/index.md`, milestone indexes, and module indexes.
