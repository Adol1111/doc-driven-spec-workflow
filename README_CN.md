# Doc-Driven Spec Workflow

[English](./README.md) · [Workflow Structure](./WORKFLOW-STRUCTURE.md) · [Release Notes](./RELEASE-NOTES.md)

一套面向 AI coding agents 的 docs-driven workflow methodology。

这个仓库提供一套可复用的方法论，用来让 agent 在实现代码前先对齐项目文档。它适合使用 architecture docs、task roadmap、task-local specs、可选 plans，以及实现前 readiness check 的项目。

> 有明确立场的 workflow methodology
>
> 这个项目专注于 docs-driven repositories。它不是所有 agent 开发流程的通用替代品，而是一套轻量方式，用来让 agent 尊重 architecture docs、task tracking、roadmap decomposition、review pause 和 branch readiness，再进入实现。

## 工作方式

这个 workflow 拆成多个本地 stage skills。root skill `doc-driven-spec-workflow` 负责判断下一步阶段和停点。

阶段链路是：

`doc-driven-spec-workflow -> docs-workflow-bootstrap -> planning-clarification -> milestone-planning -> task-preparation -> task-execution-simple`

按需使用各阶段：

- 当你不确定现在该进入哪个阶段时，从 `doc-driven-spec-workflow` 开始。
- 当仓库还没有最小 docs scaffold 时，使用 `docs-workflow-bootstrap`。
- 当目标、范围或成功标准还不清楚时，才进入 `planning-clarification`。
- 当 roadmap shape 还不清楚，需要决定 milestones、modules 和 tasks 时，使用 `milestone-planning`。
- 当当前 concrete task 已从已确认 roadmap state 中选定，并且没有 prior hard gate 阻塞 task-local spec/plan 工作时，使用 `task-preparation`。
- 当 task-local docs 和 review follow-up 都准备好之后，使用 `task-execution-simple` 进行直接实现。

root skill 只负责路由和交接上下文。具体规则、模板和停止点由各 stage skill 负责。

## Skills Library

这个仓库目前包含六个本地 workflow skills：

| Skill | 负责内容 | 停止点 |
| --- | --- | --- |
| `doc-driven-spec-workflow` | 路由到正确的 workflow 阶段 | 当下一阶段已经明确 |
| `docs-workflow-bootstrap` | 初始化最小 docs scaffold | 当核心 docs 入口创建完成 |
| `planning-clarification` | 在 roadmap decomposition 前澄清 planning direction | 当 scope、阶段边界和 first roadmap slice direction 已足够清晰 |
| `milestone-planning` | 把范围拆成 `Milestone -> 可选 Module -> Task` | 当 roadmap docs 更新完成，或当前 task 已选出 |
| `task-preparation` | 通过 `spec -> 可选 plan -> review -> routine follow-up` 准备已选 task | 当 task-local docs 已准备好交给执行层 |
| `task-execution-simple` | 通过简单直接的执行路径实现已准备好的 task | 当当前 implementation review pause 或剩余 hard gate 处理完成 |

roadmap planning 和 task reshaping 都属于 docs governance，它们不会自动授权进入 spec 或代码实现。

## 快速开始

把这个仓库作为一套 workflow skill set 安装：

```bash
npx skills add Adol1111/doc-driven-spec-workflow
```

默认安装整套。若要单独安装某一阶段、安装到特定 agent，或手动复制，请看下方的[安装](#安装)部分。

## 初始化项目 Docs

要在一个仓库里初始化最小 docs scaffold，可以这样要求 agent：

```text
Use docs-workflow-bootstrap to initialize the docs workflow scaffold for this repository.
```

默认会创建核心入口：

```text
docs/
├── index.md
├── architecture/
│   └── index.md
├── tasks/
│   ├── index.md
│   └── planning-inbox.md
└── context/
    └── index.md
```

`docs/tasks/planning-inbox.md` 用来保存还没有进入 milestone 的目标、机会和 roadmap candidates，避免新会话丢失这些 planning 信号；后续可以把它们提升到 milestone、移入 backlog，或明确丢弃。

默认不会创建 `docs/specs/` 或 `docs/plans/`。当存在具体 task 时，task-local `spec.md` 和 `plan.md` 应该创建在 `docs/tasks/<milestone>/<task>/` 下。全局 `docs/specs/` 和 `docs/plans/` 只用于 standalone 或 cross-task 文档。

Plan trigger 指执行顺序不显然：多文件顺序修改、migration、兼容性边界、跨模块协作、分阶段 rollout、验证顺序风险，或实现前必须先做 spike。

## 模板语言

这个 skill 自带的模板是英文，但生成到项目里的文档可以使用任意语言。

对于 Codex，最简单的项目级约定是在 `AGENTS.md` 里加一句：

```md
Write all generated project documentation in Chinese unless the user explicitly asks for another language.
```

对于 Claude Code，把同样的规则写进 `CLAUDE.md` 或 `.claude/CLAUDE.md`：

```md
Write all generated project documentation in Chinese unless the user explicitly asks for another language.
```

如果一个仓库同时给 Codex 和 Claude Code 使用，可以同时保留 `AGENTS.md` 和 `CLAUDE.md`，内容保持一致。

也可以在单次请求里直接指定语言：

```text
Use docs-workflow-bootstrap to initialize the docs workflow scaffold for this repository. Write all generated docs in Chinese.
```

如果你希望模板标题本身也变成本地化语言，可以 fork 这个仓库，并翻译各个 skill 的 `references/` 目录下的模板文件。

## 使用方式

安装后，在 docs-driven repository 中开始或继续工作时，优先要求 agent 使用 root workflow skill。

当你不确定现在应该进入哪个阶段时，推荐从总控 skill 开始：

```text
Use doc-driven-spec-workflow to decide whether this request needs bootstrap, planning clarification, milestone planning, task preparation, or simple task execution.
```

从 `doc-driven-spec-workflow` 进入后，只要用户明确表达了“从这里往前推进”的意思，通常就可以按阶段继续。root skill 应该一次只路由到一个阶段 skill，并携带 handoff context。在 review pause 之后，这种推进意图默认表示“按推荐路径继续”，包括需要的话先 commit 已 review 的文档、更新状态、创建 branch/worktree isolation。只有 hard gate 仍然需要单独显式确认，例如保持一个明确未确认的 roadmap 结构、留在有风险的当前分支，或删除 branch/worktree。

当主要问题是 milestone 或 task 结构时，可以直接使用 roadmap decomposition skill：

```text
Use milestone-planning to break this scope into milestones, modules, and tasks.
```

当 concrete task 已从已确认 roadmap state 中选定，并且 dependencies 和 prior hard gates 都清楚时，可以直接进入 task preparation skill：

```text
Use task-preparation to prepare the selected task by writing the spec.
```

当 task-local docs 已准备好，且下一步是直接实现时，可以直接进入 simple execution skill：

```text
Use task-execution-simple to implement the prepared task.
```

Claude Code 也可以直接调用各个已安装的 skill：

```text
/doc-driven-spec-workflow
/docs-workflow-bootstrap
/planning-clarification
/milestone-planning
/task-preparation
/task-execution-simple
```

这些 skills 主要面向使用 `docs/architecture/`、`docs/tasks/`、`docs/context/`、task-local `spec.md` 和可选 `plan.md` 的仓库。

## 示例流程

1. 用 `doc-driven-spec-workflow` 判断当前请求属于哪个阶段。
2. 如果仓库还没有最小 docs scaffold，使用 `docs-workflow-bootstrap` 初始化。
3. 需要时，用 `planning-clarification` 明确模糊意图。
4. 当 roadmap shape 还不清楚时，用 `milestone-planning` 决定 milestone、module 和 task 结构。
5. 在 `docs/tasks/` 下选定当前 concrete task。
6. 用 `task-preparation` 编写或更新 task-local `spec.md`。
7. 在 `spec.md` 后停下来给用户 review；如果需要 `plan.md`，也在它写完后停下来 review。
8. 用户只要明确表达“继续往前走”的意思，`task-preparation` 就默认处理后续常规动作，比如 commit 已 review 的文档。
9. 然后交给 `task-execution-simple` 做 branch/worktree isolation、实现、验证和 docs/status 更新。
10. 再次停下来做 implementation review，然后明确解决一种 branch-closing outcome：merge and keep branch、merge and delete branch，或 discard work。

## 期望的 Docs 结构

```text
docs/
├── index.md
├── architecture/
│   ├── index.md
│   └── <topic>.md
├── tasks/
│   ├── index.md
│   ├── <milestone>/
│   │   ├── index.md
│   │   └── <task>/
│   │       ├── task.md
│   │       ├── spec.md
│   │       └── plan.md
│   └── <milestone-with-modules>/
│       ├── index.md
│       └── <module>/
│           ├── index.md
│           └── <task>/
│               ├── task.md
│               ├── spec.md
│               └── plan.md
├── context/
│   ├── index.md
│   └── <research-note>.md
├── specs/
│   └── <standalone-or-cross-task-spec>.md
└── plans/
    └── <standalone-or-cross-task-plan>.md
```

默认情况下，task-local `spec.md` 和 `plan.md` 应该和 task 放在一起。只有 standalone 或 cross-task 文档才使用 `docs/specs/` 或 `docs/plans/`。

module 层是可选的。当 milestone 只有一个真实能力域时，使用 `docs/tasks/<milestone>/<task>/`。只有当 milestone 包含多个长期、有意义的能力域，并且它们有不同 ownership、dependencies、risk profiles、release boundaries 或 acceptance criteria 时，才使用 `docs/tasks/<milestone>/<module>/<task>/`。

task 目录名应该是稳定 slug，而不是顺序标记。把 task 按预期顺序放在 milestone 或 module 的 `index.md` 里；插入或重排任务时，不应该为了反映顺序而改名已有 task 目录。

## 说明

- `task-preparation` 和 `task-execution-simple` 在 concrete task 已从已确认 roadmap state 中选定后可以独立使用。
- 澄清、执行隔离和简单 branch closing 规则已内置到本地 skills。
- 不要在不安全的当前分支上开始实现。
- branch closing 未解决前，不应开始下一个 task。
- 如果你要更完整的端到端方法论，用 Superpowers；如果你主要要 docs-driven planning、spec-first execution 和明确 checkpoint，用这个 workflow。

## 安装

### 使用 `npx skills` 安装（推荐）

把这个仓库作为一套 workflow skill set 安装：

```bash
npx skills add Adol1111/doc-driven-spec-workflow
```

显式安装仓库中的全部 skills：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill '*'
```

也可以参考上方 skill 列表，按名称安装某一个 skill：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning
```

需要指定 agent 时，加上对应参数：

```bash
npx skills add Adol1111/doc-driven-spec-workflow -g -a claude-code
npx skills add Adol1111/doc-driven-spec-workflow -g -a codex
```

也可以组合参数，安装某个 skill 到指定 agent：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning -g -a codex
```

也可以直接从某个 skill 路径安装：

```bash
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/docs-workflow-bootstrap
```

如果你 fork 了这个仓库，把 `Adol1111/doc-driven-spec-workflow` 替换成你的 `<owner>/<repo>`。

### 使用 Codex Skill Installer

直接从仓库安装：

```bash
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow
```

或者按 skill 路径分别安装：

```bash
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/milestone-planning
```

### 手动安装到 Claude Code

个人 skill：

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/<skill-name> "$HOME/.claude/skills/"
```

项目级共享 skill：

```bash
mkdir -p .claude/skills
cp -R skills/<skill-name> .claude/skills/
```

### 手动安装到 Codex

Codex 会从 `$CODEX_HOME/skills` 发现 skills；如果未设置 `CODEX_HOME`，默认使用 `~/.codex/skills`：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/<skill-name> "${CODEX_HOME:-$HOME/.codex}/skills/"
```

## 什么时候使用

当一个仓库已经有、或希望建立如下 docs-driven workflow 时使用：

- `docs/architecture/`：稳定行为和约束。
- `docs/tasks/`：milestones、由 index 驱动的 task 顺序、status 和 dependencies。
- `docs/context/`：支持性 research。
- Task-local `task.md`、`spec.md` 和可选 `plan.md`。

当你希望 agent 不要直接跳进代码，而是先遵循 spec-first、checkpointed implementation process 时，这个 skill 最有用。
