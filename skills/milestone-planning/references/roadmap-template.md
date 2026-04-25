# Roadmap Template

Use for roadmap-layer `docs/tasks/` documents before task-local spec work begins.

This template owns milestone, optional module, and task metadata shape. It does not define `spec.md`, `plan.md`, readiness, or implementation execution.

## `docs/tasks/index.md`

```md
# Tasks Index

This directory stores project-level task documents grouped by milestone, optional module, and task.

## Open Milestones

- [M1 Private Beta](./m1-private-beta/index.md)
- [M2 Limited Release](./m2-limited-release/index.md)

## Completed Milestones

- None

## Backlog

- Optional: [Backlog](./backlog.md)

## Conventions

- Each milestone directory has its own `index.md`
- `backlog.md` is optional and stores roadmap items that are not yet attached to a milestone
- Module directories are optional; use them only when a milestone has multiple meaningful capability areas
- Task directories contain `task.md`, task-local `spec.md`, and optional `plan.md`
- Milestones are frozen after completion; add follow-up work to a new open milestone
- Milestones do not use `[completed/total]`; module progress lives in milestone indexes
```

## `docs/tasks/<milestone>/index.md`

```md
# <Milestone Name>

## Goal
- ...

## Exit Criteria
- [ ] ...

## Modules
- [Some Module [1/3]](./some-module/index.md)

## Tasks
- [01 Some Task](./01-some-task/task.md)

## Status
- Current milestone: yes/no/next/later
- Roadmap confirmed: yes/no
- When `Roadmap confirmed: no`, treat listed tasks as candidate tasks only until milestone entry is explicitly confirmed.

## Handoff Notes
- ...

## Notes
- When complete, move this milestone from `Open Milestones` to `Completed Milestones`
- After completion, do not add new modules or tasks here
```

Use either `Modules` or `Tasks`. Do not create a single catch-all module when the milestone has only one real capability area.

## `docs/tasks/<milestone>/<module>/index.md`

```md
# <Module Name> Tasks

## Goals
- ...

## Open Tasks
- `planned`: [01 Some Task](./01-some-task/task.md)

## Completed Tasks
- [02 Done Task](./02-done-task/task.md)

## Notes
- Default order follows task numbering unless a task's own `Dependencies` says otherwise.
```

## `docs/tasks/<milestone>/<task>/task.md`

Use this shape when the milestone has no module layer:

```md
# Task: <Short Title>

## Placement
- Milestone: `<milestone>`
- Module: None

## Source
- Architecture: <path or link, if relevant>
- Request: <short request summary>

## Dependencies
- None

## Status
- [x] planned
- [ ] in_progress
- [ ] blocked
- [ ] completed

## Checklist
- [ ] Project-level acceptance point

## Notes
- Keep detailed implementation steps in task-local `spec.md` or optional `plan.md`.
```

Use this path when modules exist:

```md
docs/tasks/<milestone>/<module>/<task>/task.md
```

## `docs/tasks/backlog.md`

```md
# Backlog

This file stores candidate roadmap items that are not yet attached to a milestone.

## Items

- Some follow-up item
  Source: `M1` handoff note
  Notes: waiting for milestone assignment
```

## Rules

- `docs/tasks/index.md` lists `Open Milestones` and `Completed Milestones`; it may also link an optional `Backlog`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- `docs/tasks/backlog.md` is optional. Use it for roadmap items that are not yet attached to a milestone.
- Modules are optional durable capability areas, not one-off buckets.
- If a proposed module has fewer than three likely tasks, merge it unless it has a distinct long-term domain, owner, lifecycle, risk profile, release boundary, or acceptance boundary.
- Do not create tasks for implementation or verification sub-steps such as code review, tests, migrations, single files, or refactor slices.
- Do not create standalone tasks for routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, or small docs reorganization.
- Cross-milestone sequencing belongs in milestone-level notes or exit criteria, not repeated task-level `Depends on` links.
