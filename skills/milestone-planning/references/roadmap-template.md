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

## Planning Inbox

- [Planning Inbox](./planning-inbox.md)

## Conventions

- Each milestone directory has its own `index.md`
- `planning-inbox.md` stores unconfirmed goals, opportunities, and roadmap candidates until they are promoted into a milestone, moved to backlog, or discarded
- `backlog.md` is optional and stores deferred roadmap items that are concrete enough to keep, but not yet attached to a milestone
- Module directories are optional; use them only when a milestone has multiple meaningful capability areas
- Task directories use stable, unnumbered slugs and contain `task.md`, task-local `spec.md`, and optional `plan.md`
- Task order is the ordered-list order of task links in the relevant milestone or module `index.md`
- Milestones are frozen after completion; add follow-up work to a new open milestone
- Milestones do not use `[completed/total]`; module progress lives in milestone indexes
```

## `docs/tasks/<milestone>/index.md` with modules

```md
# <Milestone Name>

## Goal
- ...

## Exit Criteria
- [ ] ...

## Modules
- [Some Module [1/3]](./some-module/index.md)

## Status
- Current milestone: yes/no/next/later
- Roadmap confirmed: yes/no
- When `Roadmap confirmed: no`, treat listed tasks as candidate tasks only until milestone entry is explicitly confirmed.

## Handoff Notes
- ...

## Notes
- When complete, move this milestone from `Open Milestones` to `Completed Milestones`
- After completion, do not add new modules or tasks here
- Use `Handoff Notes` as a temporary queue for future work discovered during the milestone until each item is resolved to current-milestone work, a later milestone, `backlog.md`, `planning-inbox.md`, or removal
```

## `docs/tasks/<milestone>/index.md` without modules

```md
# <Milestone Name>

## Goal
- ...

## Exit Criteria
- [ ] ...

## Open Tasks
1. `planned`: [Some Task](./some-task/task.md)

## Completed Tasks
- [Done Task](./done-task/task.md)

## Status
- Current milestone: yes/no/next/later
- Roadmap confirmed: yes/no
- When `Roadmap confirmed: no`, treat listed tasks as candidate tasks only until milestone entry is explicitly confirmed.

## Handoff Notes
- ...

## Notes
- When complete, move this milestone from `Open Milestones` to `Completed Milestones`
- After completion, do not add new modules or tasks here
- Use `Handoff Notes` as a temporary queue for future work discovered during the milestone until each item is resolved to current-milestone work, a later milestone, `backlog.md`, `planning-inbox.md`, or removal
```

Choose one of the two milestone shapes above. Do not mix `Modules` with milestone-level task lists in the same file. Do not create a single catch-all module when the milestone has only one real capability area.

## `docs/tasks/<milestone>/<module>/index.md`

This template intentionally looks similar to the milestone index, but modules omit milestone-only governance fields such as `Status` and `Handoff Notes`.

```md
# <Module Name> Tasks

## Goals
- ...

## Open Tasks
1. `planned`: [Some Task](./some-task/task.md)

## Completed Tasks
- [Done Task](./done-task/task.md)

## Notes
- Default order follows this ordered list unless a task's own `Dependencies` says otherwise.
```

## `docs/tasks/<milestone>/<task>/task.md`

Use this shape when the milestone has no module layer:

```md
# Task: <Short Title>

## Placement
- Milestone: `<milestone>`
- Module: None

## Why
- Problem: <what user or operator problem this task solves>
- Outcome: <what becomes possible or better when this task is done>

## Who / When
- User or role: <who this is for>
- Scenario: <when this task matters>

## Scope
- In scope now:
  - <current scope item>
- Later / not in scope:
  - <later item or explicit non-goal>

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

## Success Signals
- <observable result that should be true when this task is complete>

## Notes
- Keep detailed design decisions in task-local `spec.md`.
- Keep detailed implementation sequencing in optional `plan.md`.
```

`Status` is a single-choice state marker. Exactly one of `planned`, `in_progress`, `blocked`, or `completed` should be checked at a time.

Use the task states this way:

- `planned`: decomposed and tracked, but active task-local work has not started yet
- `in_progress`: active preparation or execution work is underway
- `blocked`: the selected task cannot continue because of a real blocker that should be visible in docs or handoff context
- `completed`: implementation, verification, required docs/status updates, and closing are all resolved

Use this path when modules exist:

```md
docs/tasks/<milestone>/<module>/<task>/task.md
```

## `docs/tasks/backlog.md`

```md
# Backlog

This file stores deferred roadmap items that are concrete enough to keep, but are not yet attached to a milestone.

## Items

- Some follow-up item
  Source: `M1` handoff note
  Notes: waiting for milestone assignment
```

## `docs/tasks/planning-inbox.md`

```md
# Planning Inbox

Unconfirmed goals, opportunities, and roadmap candidates live here until they are aligned enough to become milestones, moved to backlog, or discarded.

## Candidates

### <Candidate Name>

- Status: needs alignment | ready to decompose | parked | discarded
- Source: <user request, research note, handoff, or other origin>
- Problem: <what need or opportunity this represents>
- Current question: <what must be decided next>
- Next routing: planning-clarification | milestone-planning | backlog | discard
```

## Rules

- `docs/tasks/index.md` lists `Open Milestones` and `Completed Milestones`; it should link `Planning Inbox` and may also link an optional `Backlog`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- `docs/tasks/planning-inbox.md` is the routing source for goals that are not yet milestone-shaped.
- `docs/tasks/planning-inbox.md` is for planning candidates and unresolved roadmap direction, not deferred tasks that are already well-shaped.
- `docs/tasks/backlog.md` is optional. Use it for deferred roadmap items that are concrete enough to keep, but are not yet attached to a milestone.
- Revisit `docs/tasks/planning-inbox.md` when the current question is direction, alignment, or whether a candidate is now ready to decompose.
- Revisit `docs/tasks/backlog.md` when the current planning pass, user request, or milestone reshaping may promote a deferred roadmap item into active milestone consideration.
- Record handoff items in the current milestone `index.md`, not in task-local `plan.md`.
- Keep a handoff item in the current milestone only when it is required for the current milestone's exit criteria.
- Move a handoff item to a later milestone when it is clearly future milestone work.
- Move a handoff item to `docs/tasks/backlog.md` when it is already a recognizable roadmap item, but not yet assigned to a milestone.
- Move a handoff item to `docs/tasks/planning-inbox.md` when it still needs alignment or is not yet milestone-shaped.
- Treat `task.md` as a lightweight product brief for one concrete task: enough problem, user, scope, and success context to justify the later `spec.md`, but not a full implementation design.
- Task `Status` checkboxes are mutually exclusive. Exactly one of `planned`, `in_progress`, `blocked`, or `completed` should be checked at a time; do not treat them as a checklist of completed phases.
- Modules are optional durable capability areas, not one-off buckets.
- If a proposed module has fewer than three likely tasks, merge it unless it has a distinct long-term domain, owner, lifecycle, risk profile, release boundary, or acceptance boundary.
- Task directory slugs are stable identifiers, not ordering controls; do not add numeric prefixes.
- Reorder tasks by editing the relevant `index.md` list order and dependency links, not by renaming task directories.
- Do not create tasks for implementation or verification sub-steps such as code review, tests, migrations, single files, or refactor slices.
- Do not create standalone tasks for routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, or small docs reorganization.
- Cross-milestone sequencing belongs in milestone-level notes or exit criteria, not repeated task-level `Depends on` links.
