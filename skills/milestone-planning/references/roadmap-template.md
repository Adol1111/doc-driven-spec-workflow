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

## Conventions

- Each milestone directory has its own `index.md`
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
- ...

## Modules
- [Some Module [1/3]](./some-module/index.md)

## Tasks
- [01 Some Task](./01-some-task/task.md)

## Status
- Current milestone: yes/no/next/later
- Roadmap confirmed: yes/no

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

## Recommended Order
1. [01 Some Task](./01-some-task/task.md)

## Dependency Notes
- `01-some-task`: ...

## Open Tasks
- `planned`: [01 Some Task](./01-some-task/task.md)

## Completed Tasks
- [02 Done Task](./02-done-task/task.md)
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

## Rules

- `docs/tasks/index.md` lists only `Open Milestones` and `Completed Milestones`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- Milestone confirmation should be explicit in each milestone `Status` section. Use `Roadmap confirmed: no` for provisional placeholder milestones and flip it to `yes` when the user confirms continuing on that path.
- Starting a task in a later milestone requires two checks first: the earlier milestone is intentionally still active or explicitly closed, and the later milestone has `Roadmap confirmed: yes`.
- `Handoff Notes` is optional. Use it only for follow-up findings discovered during the milestone that should be carried into a later milestone.
- Do not use `Handoff Notes` to restate open task status, explain the next task, or duplicate `Open Tasks`, `Completed Tasks`, `Goal`, or `Exit Criteria`.
- `Handoff Notes` is a temporary transfer queue. Once an item is attached to a later milestone or backlog, remove it from `Handoff Notes`.
- `Handoff Notes` must be empty before milestone closure. If a handoff item still exists here, the handoff is not finished.
- If a finding means the current milestone is not actually complete, express that through `Exit Criteria` or open task state instead of treating it as handoff-only information.
- Modules are optional durable capability areas, not one-off buckets.
- If a proposed module has fewer than three likely tasks, merge it unless it has a distinct long-term domain, owner, lifecycle, risk profile, release boundary, or acceptance boundary.
- `Open Tasks` lists only `planned`, `in_progress`, and `blocked`.
- `Completed Tasks` lists only `completed`.
- Numeric prefixes imply default order, not strict serialization.
- Do not create tasks for implementation or verification sub-steps such as code review, tests, migrations, single files, or refactor slices.
- Do not create standalone tasks for routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, or small docs reorganization.
- Cross-milestone sequencing belongs in milestone-level notes or exit criteria, not repeated task-level `Depends on` links.
