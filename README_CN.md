# Doc-Driven Spec Workflow

[English](./README.md)

一个面向 AI coding agents 的 docs-driven spec workflow skill。

这个仓库提供一套可复用的工作流，用来让 agent 在实现代码前先对齐项目文档。它适合使用 architecture docs、task roadmap、task-local specs、可选 plans，以及实现前 readiness checkpoint 的项目。

> 有明确立场的 workflow skill
>
> 这个项目专注于 docs-driven repositories。它不是所有 agent 开发流程的通用替代品，而是一套轻量方式，用来让 agent 尊重 architecture docs、task tracking、spec approval 和 branch readiness，再进入实现。

## 快速开始

使用 open agent skills CLI 安装：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow
```

全局安装到 Claude Code：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code
```

全局安装到 Codex：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a codex
```

安装后重启 agent，让它发现新 skill。

## 初始化项目 Docs

要在一个仓库里初始化最小 docs scaffold，可以这样要求 agent：

```text
Use doc-driven-spec-workflow to initialize the docs workflow scaffold for this repository.
```

默认会创建核心入口：

```text
docs/
├── index.md
├── architecture/
│   └── index.md
├── tasks/
│   └── index.md
└── context/
    └── index.md
```

默认不会创建 `docs/specs/` 或 `docs/plans/`。当存在具体 task 时，task-local `spec.md` 和 `plan.md` 应该创建在 `docs/tasks/<milestone>/<task>/` 下。全局 `docs/specs/` 和 `docs/plans/` 只用于 standalone 或 cross-task 文档。

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
Use doc-driven-spec-workflow to initialize the docs workflow scaffold for this repository. Write all generated docs in Chinese.
```

如果你希望模板标题本身也变成本地化语言，可以 fork 这个仓库，并翻译 `skills/doc-driven-spec-workflow/references/` 下的模板文件。

## 使用方式

安装后，在 docs-driven repository 中开始或继续实现工作时，可以这样要求 agent 使用该 workflow：

```text
Use doc-driven-spec-workflow to pick the next task and write the spec.
```

Claude Code 也可以直接调用：

```text
/doc-driven-spec-workflow
```

这个 skill 主要面向使用 `docs/architecture/`、`docs/tasks/`、`docs/context/`、task-local `spec.md` 和可选 `plan.md` 的仓库。

## 示例流程

1. 用 `brainstorming` 或等价澄清流程明确模糊意图。
2. 阅读相关 architecture、task 和 context docs。
3. 在 `docs/tasks/` 下选择或创建具体 task。
4. 编写或更新 task-local `spec.md`。
5. 停下来等待用户批准，不直接进入实现。
6. 只有任务确实复杂时才创建 `plan.md`。
7. 运行 readiness checkpoint，并用 branch 或 worktree 隔离实现工作。
8. 实现、验证、更新 docs/status，并处理 branch closing。

## 它做什么

- 把 `docs/tasks/` 作为具体实现工作的 source of truth。
- 实现前要求 task-local spec，复杂任务可选 plan。
- 保持 architecture、task tracking、spec 和 status updates 对齐。
- 区分 docs governance 和 implementation permission。
- 在写代码前执行 readiness checkpoint，包括 branch/worktree isolation。
- 提供 architecture docs、task indexes、specs、plans 和 context notes 的紧凑模板。

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

## 兼容说明

这个 skill 可以独立使用，但会引用 [obra/superpowers](https://github.com/obra/superpowers) 中两个可选 workflow skills：

- `brainstorming`：在选择具体 task 或写 spec 前，澄清模糊的 feature、behavior 或 task intent。
- `using-git-worktrees`：当 workspace dirty、shared、风险较高或可能冲突时，创建安全的 branch/worktree isolation。

如果你的 agent 环境没有这些 skills，请使用等价的 clarification 和 git isolation workflows。需要保留相同安全规则：在锁定 spec 前澄清不明确意图，不要在不安全的当前分支上开始具体实现，不要在没有明确 closing decision 的情况下删除或合并 branches/worktrees。

## 为什么不直接使用 Superpowers？

Superpowers 是更完整的软件开发方法论，包含 brainstorming、planning、TDD、subagents、code review、verification、branch finishing 等一组可组合 skills。这个 workflow 刻意更窄：

- 它围绕项目长期文档结构组织：`docs/architecture/`、`docs/tasks/`、`docs/context/`、task-local `spec.md` 和可选 `plan.md`。
- 它把 `docs/tasks/` 当作选择具体工作、追踪 milestone 状态的 source of truth，避免 agent 直接从 architecture notes 发明实现任务。
- 它区分 docs governance 和 implementation permission，因此 architecture edits、roadmap reshaping 和 index maintenance 不会自动授权写代码。
- 它不强制 TDD、heavyweight planning 或 subagent workflows，更适合只想采用 spec-first coordination、但不想引入完整 Superpowers 方法论的项目。
- 它仍然可以和 Superpowers 组合使用，尤其是模糊 spec 前的 `brainstorming`，以及高风险实现前的 `using-git-worktrees`。

如果你想要完整的端到端 agentic development methodology，使用 Superpowers。如果你的主要目标是让 agent 对齐 docs-driven architecture、task roadmap 和 spec approval process，使用这个 workflow。

## 安装

### 使用 `npx skills` 安装（推荐）

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow
```

全局安装到 Claude Code：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code
```

全局安装到 Codex：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a codex
```

同时全局安装到 Claude Code 和 Codex：

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code -a codex
```

也可以直接从 skill 路径安装：

```bash
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/doc-driven-spec-workflow
```

如果你 fork 了这个仓库，把 `Adol1111/doc-driven-spec-workflow` 替换成你的 `<owner>/<repo>`。

### 使用 Codex Skill Installer

```bash
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/doc-driven-spec-workflow
```

### 手动安装到 Claude Code

个人 skill：

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/doc-driven-spec-workflow "$HOME/.claude/skills/"
```

项目级共享 skill：

```bash
mkdir -p .claude/skills
cp -R skills/doc-driven-spec-workflow .claude/skills/
```

### 手动安装到 Codex

Codex 会从 `$CODEX_HOME/skills` 发现 skills；如果未设置 `CODEX_HOME`，默认使用 `~/.codex/skills`：

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/doc-driven-spec-workflow "${CODEX_HOME:-$HOME/.codex}/skills/"
```

安装后请重启 agent。

## 什么时候使用

当一个仓库已经有、或希望建立如下 docs-driven workflow 时使用：

- `docs/architecture/`：稳定行为和约束。
- `docs/tasks/`：milestones、task ordering、status 和 dependencies。
- `docs/context/`：支持性 research。
- Task-local `task.md`、`spec.md` 和可选 `plan.md`。

当你希望 agent 不要直接跳进代码，而是先遵循 spec-first、checkpointed implementation process 时，这个 skill 最有用。
