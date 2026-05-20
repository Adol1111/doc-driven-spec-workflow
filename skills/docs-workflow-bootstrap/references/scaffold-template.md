# Scaffold Template

Use for the minimum docs-driven workflow scaffold only.

Create only the missing entry-point docs:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- `docs/context/index.md`

Keep bootstrap docs minimal, navigational, and easy for later stages to reshape.

## `docs/index.md`

```md
# Documentation Index

`docs/` is the main documentation entry point for workflow state, stable design, and supporting context.

## Sections

- [Architecture](./architecture/index.md)
- [Tasks](./tasks/index.md)
- [Context](./context/index.md)
```

## `docs/architecture/index.md`

```md
# Architecture Index

This directory stores stable design documents and long-lived system boundaries.

## Documents

- None yet
```

## `docs/tasks/index.md`

```md
# Tasks Index

This directory stores milestone, task, and task-local execution documents.

## Open Milestones

- None yet

## Completed Milestones

- None yet

## Planning Inbox

- [Planning Inbox](./planning-inbox.md)
```

## `docs/tasks/planning-inbox.md`

```md
# Planning Inbox

Unconfirmed goals and roadmap candidates live here until they are aligned, decomposed, deferred, or discarded.

## Candidates

- None yet
```

If the user explicitly asks to preserve roadmap-like content during bootstrap, replace `None yet` with one compact candidate block.

Recommended candidate shape:

```md
### <Candidate Name>

- Status: needs alignment | ready to decompose | parked | discarded
- Source: <user request, handoff, or other origin>
- Problem: <what need or opportunity this represents>
- Current question: <what must be decided next>
- Next routing: planning-clarification | milestone-planning | backlog | discard
```

## `docs/context/index.md`

```md
# Context Index

This directory stores supporting research notes, references, and unstable findings.

## Current Research

- None yet
```

## Rules

- Bootstrap creates only entry-point docs, not roadmap structure or task-local execution docs.
- Keep content minimal. Do not preload detailed architecture, milestones, or task breakdown.
- Use repository doc language rules when available; otherwise follow the current user language.
