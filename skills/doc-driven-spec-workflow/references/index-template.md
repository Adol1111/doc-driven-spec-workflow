# Index Template

Use for `docs/` index files to explain directory purpose, entry points, and usage.

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

## `docs/tasks/index.md`

```md
# Tasks Index

This directory stores project-level task documents grouped by milestone, module, and task.

## Open Milestones

- [M1 Private Beta](./m1-private-beta/index.md)
- [M2 Limited Release](./m2-limited-release/index.md)

## Completed Milestones

- None

## Conventions

- Each milestone directory has its own `index.md`
- Module directories are optional; use them only when a milestone has multiple meaningful capability areas
- Module indexes use `Open Tasks` and `Completed Tasks` sections
- Task directories contain `task.md`, task-local `spec.md`, and optional `plan.md`
- `task.md` tracks status, dependencies, sources, and acceptance points
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

## Status
- Current milestone: yes/no/next/later

## Current Gaps
- ...

## Notes
- When complete, move this milestone from `Open Milestones` to `Completed Milestones`
- After completion, do not add new modules or tasks here
```

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

Additional rules:

- `docs/tasks/index.md` lists only `Open Milestones` and `Completed Milestones`.
- Milestone `index.md` lists modules and module progress.
- Completed milestones are frozen.
- Modules should be durable capability areas, not one-off buckets for one or two tasks.
- If a milestone has only one real capability area, use `Milestone -> tasks` and place task directories directly under the milestone instead of creating a single catch-all module.
- If a proposed module has fewer than three likely tasks, merge it unless it has a distinct long-term domain, owner, lifecycle, risk profile, release boundary, or acceptance boundary.
- Module `index.md` should prefer `Open Tasks` and `Completed Tasks` sections.
- `Open Tasks` lists only `planned`, `in_progress`, and `blocked`.
- `Completed Tasks` lists only `completed`.
- Module `index.md` should explain both recommended order and task dependencies.
- Numeric prefixes imply default order, not strict serialization.
- Do not create tasks for implementation or verification sub-steps such as code review, tests, migrations, single files, or refactor slices; keep those in `spec.md`, optional `plan.md`, or checklist items.
- Do not create standalone tasks for routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, or small docs reorganization; handle them inline with the current work round.
- Create a pure cleanup/governance/clarification task only when it is complex, cross-cutting, independently reviewable, or needs project-level execution tracking.
- Cross-milestone sequencing belongs in milestone-level notes or exit criteria, not repeated task-level `Depends on` links.

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

本目录保存进入实现前的设计规格。

## Naming

- 使用 `YYYY-MM-DD-<topic>-design.md`
- `<topic>` 使用简短英文 kebab-case
- 示例：`2026-04-16-chat-fixed-user-context-design.md`

## Role

- spec 用于记录当前任务进入实现前的目标、边界、方案和验证方式
- task-local spec 的具体结构与写法以 `doc-driven-spec-workflow` skill 及其 references 模板为准
- 当结论成为长期系统约束时，应迁移或沉淀到 `docs/architecture/`

## Lifecycle

- 新规格应在开始实现前创建，并在进入代码阶段前得到用户确认。
- 只有任务确实复杂或多步骤时，才创建对应的 `docs/plans/` 计划文档。
```

## `docs/plans/index.md`

```md
# Working Plans

本目录保存复杂任务需要的详细实施计划。

## Naming

- 使用 `YYYY-MM-DD-<feature-name>.md`
- `<feature-name>` 使用简短英文 kebab-case
- 示例：`2026-04-16-chat-fixed-user-context.md`

## Role

- plan 只在任务确实复杂或多步骤时创建
- plan 用来拆实现切片、文件范围和验证方式，不重复已经确认的 spec
- task-local plan 的具体结构与写法以 `doc-driven-spec-workflow` skill 及其 references 模板为准

## Lifecycle

- plan 写完后先等用户确认，再开始编码

## Relationship To `docs/tasks/`

`docs/plans/` 是详细执行入口。`docs/tasks/` 只记录 milestone、module、任务状态、依赖关系和历史索引；如果某个项目任务有对应 plan，应在 task 的 `Source` 或 `Notes` 中链接到这里，而不是复制完整执行步骤。
```

## Rules

- `index.md` should explain what the directory is, what it contains, and how to use it.
- `index.md` is for navigation and conventions, not detailed implementation for a single task.
