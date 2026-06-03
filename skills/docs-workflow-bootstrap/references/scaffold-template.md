# Scaffold Template

Use for the minimum docs-driven workflow scaffold only.

Create only the missing entry-point docs:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- `docs/tasks/backlog.md`
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

## Backlog

- [Backlog](./backlog.md)
```

## `docs/tasks/planning-inbox.md`

```md
# Planning Inbox

Future goals and candidate milestones live here until they are promoted into open milestone planning or discarded.

## Goals

- None yet
```

If the user explicitly asks to preserve roadmap-like content during bootstrap, replace `None yet` with one compact goal block.

Recommended goal shape:

```md
### <Goal Name>

- Status: needs alignment | ready for milestone planning | parked | discarded
- Horizon: short-term | mid-term | long-term
- Source: <user request, handoff, or other origin>
- Goal: <what future outcome or phase this represents>
- Why not in open milestones: <why this goal is not active yet>
- Promotion trigger: <what makes this goal ready to plan as a milestone>
```

## `docs/tasks/backlog.md`

```md
# Backlog

Concrete deferred tasks live here until they are promoted into a milestone, discarded, or superseded.

## Deferred Tasks

- None yet
```

Recommended task shape:

```md
### <Task Name>

- Status: deferred | candidate for next milestone | promoted | discarded
- Fits goal: <planning-inbox goal or milestone name>
- Task shape: <what concrete outcome this task would deliver>
- Why deferred: <why this is not assigned to an open milestone now>
- Promotion trigger: <when to reconsider this task>
- Source: <handoff note, user request, or other origin>
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
