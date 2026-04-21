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

本目录保存进入实现前的设计规格。

## Naming

- 使用 `YYYY-MM-DD-<topic>-design.md`
- `<topic>` 使用简短英文 kebab-case
- 示例：`2026-04-16-chat-fixed-user-context-design.md`

## Role

- spec 用于记录当前任务进入实现前的目标、边界、方案和验证方式
- task-local spec 的具体结构与写法以 `task-spec-execution` skill 及其 references 模板为准
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
- task-local plan 的具体结构与写法以 `task-spec-execution` skill 及其 references 模板为准

## Lifecycle

- plan 写完后先等用户确认，再开始编码

## Relationship To `docs/tasks/`

`docs/plans/` 是详细执行入口。`docs/tasks/` 只记录 milestone、module、任务状态、依赖关系和历史索引；如果某个项目任务有对应 plan，应在 task 的 `Source` 或 `Notes` 中链接到这里，而不是复制完整执行步骤。
```

## Rules

- `index.md` should explain what the directory is, what it contains, and how to use it.
- `index.md` is for navigation and conventions, not detailed implementation for a single task.
- Use `milestone-planning/references/roadmap-template.md` for `docs/tasks/index.md`, milestone indexes, and module indexes.
