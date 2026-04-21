# Doc-Driven Spec Workflow

[中文说明](./README_CN.md)

A docs-driven workflow skill set for AI coding agents.

This repository packages a reusable workflow for keeping implementation work aligned with project documentation. It is useful for repositories that organize work around architecture docs, task roadmaps, task-local specs, optional plans, and explicit readiness checkpoints before code changes.

> Opinionated workflow skill set
>
> This project is intentionally focused on docs-driven repositories. It is not a general replacement for every agent development workflow; it is a lightweight way to make agents respect architecture docs, task tracking, roadmap decomposition, spec approval, and branch readiness before implementation.

## Workflow Overview

These skills are not parallel alternatives. They are different stages of one docs-driven delivery workflow:

`docs-delivery-workflow -> brainstorming -> milestone-planning -> doc-driven-spec-workflow`

Not every request uses every stage:

- Start with `docs-delivery-workflow` when the main question is which stage comes next.
- Use `brainstorming` only when goals, scope, or success criteria are still unclear.
- Use `milestone-planning` when the roadmap shape is unclear and you need to decide milestones, modules, and tasks.
- Use `doc-driven-spec-workflow` after the current concrete task is chosen and you want to write the task-local spec and move toward implementation.

## Skill Responsibilities

This repository currently contains three workflow skills plus one optional upstream clarification skill:

| Skill | Responsibility | Stop Point |
| --- | --- | --- |
| `docs-delivery-workflow` | Route work to the right workflow stage | When the next stage is clear |
| `milestone-planning` | Decompose scope into `Milestone -> optional Module -> Task` | When roadmap docs are updated or the current task is selected |
| `doc-driven-spec-workflow` | Execute the current task via `spec -> optional plan -> readiness -> implementation` | When the current task checkpoint and branch closing are resolved |
| `brainstorming` | Clarify ambiguous intent before planning or spec work | When scope and success criteria are clear enough to continue |

Roadmap planning and task reshaping are docs governance work. They do not automatically authorize spec writing or code changes.

## Quick Start

Install this repository as a skill set:

```bash
npx skills add Adol1111/doc-driven-spec-workflow
```

Use interactive selection by default. See [Installation](#installation) for installing all skills, single stages, global agent targets, or manual copies.

## Bootstrap A Repository

To initialize the minimum docs scaffold in a repository, ask your agent:

```text
Use doc-driven-spec-workflow to initialize the docs workflow scaffold for this repository.
```

This should create the core entry points:

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

The workflow does not create `docs/specs/` or `docs/plans/` by default. Task-local `spec.md` and `plan.md` files should be created under `docs/tasks/<milestone>/<task>/` when there is a concrete task. Global `docs/specs/` and `docs/plans/` are reserved for standalone or cross-task documents.

## Template Language

The bundled templates are written in English, but generated project docs can use any language.

For Codex, the simplest project-level convention is to add a short rule to `AGENTS.md`:

```md
Write all generated project documentation in Chinese unless the user explicitly asks for another language.
```

For Claude Code, add the same rule to `CLAUDE.md` or `.claude/CLAUDE.md`:

```md
Write all generated project documentation in Chinese unless the user explicitly asks for another language.
```

For repositories used by both Codex and Claude Code, keep the language rule in both `AGENTS.md` and `CLAUDE.md`.

You can also specify the language directly in a request:

```text
Use doc-driven-spec-workflow to initialize the docs workflow scaffold for this repository. Write all generated docs in Chinese.
```

You can also fork this repository and translate the files under `skills/doc-driven-spec-workflow/references/` if you want the template headings themselves to be localized.

## Usage

After installation, ask your agent to use the workflow when starting or continuing work in a docs-driven repository.

Recommended entry point when you are unsure which stage comes next:

```text
Use docs-delivery-workflow to decide whether this request needs clarification, milestone planning, or current-task spec execution.
```

After entering through `docs-delivery-workflow`, you can usually keep moving stage by stage with messages like `continue`. Explicit approval points still require explicit confirmation, such as roadmap confirmation when needed, `spec.md` approval, `plan.md` approval, and branch-closing decisions.

Use the roadmap decomposition skill directly when the main question is milestone or task structure:

```text
Use milestone-planning to break this scope into milestones, modules, and tasks.
```

Use the current-task execution skill directly when the concrete task is already chosen:

```text
Use doc-driven-spec-workflow to pick the next task and write the spec.
```

For Claude Code, you can also invoke the individual skills directly:

```text
/docs-delivery-workflow
/milestone-planning
/doc-driven-spec-workflow
```

These skills are designed for repositories that use `docs/architecture/`, `docs/tasks/`, `docs/context/`, task-local `spec.md`, and optional `plan.md` files.

## Example Workflow

1. Route the request with `docs-delivery-workflow`.
2. Clarify ambiguous intent with `brainstorming` or an equivalent clarification flow when needed.
3. Use `milestone-planning` to decide milestone, module, and task structure when the roadmap shape is still unclear.
4. Select the current concrete task under `docs/tasks/`.
5. Use `doc-driven-spec-workflow` to write or update the task-local `spec.md`.
6. Stop for user approval before implementation.
7. Create `plan.md` only when the task is genuinely complex.
8. Run the readiness checkpoint and isolate work with a branch or worktree.
9. Implement, verify, update docs/status, and resolve branch closing.

## What It Does

- Treats `docs/tasks/` as the source of truth for roadmap and concrete implementation work.
- Separates workflow routing, roadmap decomposition, and current-task execution into distinct skills.
- Requires task-local specs before implementation and optional plans for complex work.
- Keeps architecture, task tracking, specs, and status updates aligned.
- Separates docs governance from implementation permission.
- Enforces readiness checkpoints before code edits, including branch or worktree isolation.
- Provides compact templates for architecture docs, task indexes, specs, plans, and context notes.

## Expected Docs Layout

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

Task-local `spec.md` and `plan.md` files should live with the task by default. Use `docs/specs/` or `docs/plans/` only for standalone or cross-task documents that do not belong to one concrete task.

The module layer is optional. Use `docs/tasks/<milestone>/<task>/` when a milestone has one real capability area. Use `docs/tasks/<milestone>/<module>/<task>/` only when a milestone has multiple durable capability areas with different ownership, dependencies, risk profiles, release boundaries, or acceptance criteria.

## Compatibility Notes

The current-task execution skill can work on its own, but this repository is designed to compose with optional clarification and execution-safety skills from [obra/superpowers](https://github.com/obra/superpowers):

- `brainstorming`: Clarifies ambiguous feature, behavior, or task intent before roadmap decomposition or current-task spec work.
- `using-git-worktrees`: Creates safe branch/worktree isolation when a workspace is dirty, shared, risky, or likely to conflict.

If your agent environment does not have these skills, use equivalent clarification and git isolation workflows instead. Preserve the same safety rules: clarify unclear intent before locking roadmap structure or specs, do not start concrete implementation on an unsafe current branch, and do not delete or merge branches/worktrees without an explicit closing decision.

## Why Not Just Use Superpowers?

Superpowers is a broader software development methodology with many composable skills for brainstorming, planning, TDD, subagents, code review, verification, and branch finishing. This workflow is intentionally narrower:

- It is organized around a repository's durable documentation structure: `docs/architecture/`, `docs/tasks/`, `docs/context/`, task-local `spec.md`, and optional `plan.md`.
- It treats `docs/tasks/` as the source of truth for both roadmap decomposition and selecting concrete work.
- It separates docs governance from implementation permission, so architecture edits, roadmap reshaping, and index maintenance do not automatically authorize code changes.
- It splits workflow routing, roadmap planning, and current-task execution into separate skills instead of collapsing them into one oversized instruction file.
- It keeps TDD, heavyweight planning, and subagent workflows optional instead of mandatory, which makes it easier to use in projects that want spec-first coordination without adopting the full Superpowers methodology.
- It can still compose with Superpowers where useful, especially `brainstorming` before ambiguous scope and `using-git-worktrees` before risky implementation work.

Use Superpowers when you want the full end-to-end agentic development methodology. Use this workflow when your main need is to keep agents aligned with a docs-driven architecture, task roadmap, and spec approval process.

## Installation

### Install With `npx skills` (Recommended)

Install this repository as a skill set:

```bash
npx skills add Adol1111/doc-driven-spec-workflow
```

Install all skills from the repo explicitly:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill '*'
```

Or install the full workflow one skill at a time:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill docs-delivery-workflow
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow
```

For a global Claude Code install:

```bash
npx skills add Adol1111/doc-driven-spec-workflow -g -a claude-code
npx skills add Adol1111/doc-driven-spec-workflow --skill '*' -g -a claude-code
```

Or target Claude Code one skill at a time:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill docs-delivery-workflow -g -a claude-code
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning -g -a claude-code
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code
```

For a global Codex install:

```bash
npx skills add Adol1111/doc-driven-spec-workflow -g -a codex
npx skills add Adol1111/doc-driven-spec-workflow --skill '*' -g -a codex
```

Or target Codex one skill at a time:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill docs-delivery-workflow -g -a codex
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning -g -a codex
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a codex
```

If you only want one stage, install just that skill by name.

You can also install directly from each skill path:

```bash
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/docs-delivery-workflow
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/milestone-planning
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/doc-driven-spec-workflow
```

If you fork this repository, replace `Adol1111/doc-driven-spec-workflow` with your fork's `<owner>/<repo>` name.

Restart your agent after installation so it can discover the new skills.

### Install With Codex Skill Installer

Install from the repository path directly:

```bash
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow
```

Or install each skill by pointing the installer at its path:

```bash
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/docs-delivery-workflow
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/milestone-planning
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/doc-driven-spec-workflow
```

Restart your agent after installation so it can discover the new skills.

### Manual Install For Claude Code

Claude Code discovers personal skills from `~/.claude/skills/`:

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/docs-delivery-workflow "$HOME/.claude/skills/"
cp -R skills/milestone-planning "$HOME/.claude/skills/"
cp -R skills/doc-driven-spec-workflow "$HOME/.claude/skills/"
```

For a project-local Claude Code skill shared with a repository:

```bash
mkdir -p .claude/skills
cp -R skills/docs-delivery-workflow .claude/skills/
cp -R skills/milestone-planning .claude/skills/
cp -R skills/doc-driven-spec-workflow .claude/skills/
```

Claude Code also supports invoking each installed skill directly as `/docs-delivery-workflow`, `/milestone-planning`, or `/doc-driven-spec-workflow`.

### Manual Install For Codex

Codex discovers skills from `$CODEX_HOME/skills`, or `~/.codex/skills` when `CODEX_HOME` is unset:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/docs-delivery-workflow "${CODEX_HOME:-$HOME/.codex}/skills/"
cp -R skills/milestone-planning "${CODEX_HOME:-$HOME/.codex}/skills/"
cp -R skills/doc-driven-spec-workflow "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Restart Codex after copying the skill.

### Manual Install For Other Agents

If your agent uses a different skill directory, copy the installable skill folders into that directory:

```bash
cp -R skills/docs-delivery-workflow /path/to/agent/skills/
cp -R skills/milestone-planning /path/to/agent/skills/
cp -R skills/doc-driven-spec-workflow /path/to/agent/skills/
```

For example, in an environment that discovers skills from `~/.agents/skills`:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R skills/docs-delivery-workflow "$HOME/.agents/skills/"
cp -R skills/milestone-planning "$HOME/.agents/skills/"
cp -R skills/doc-driven-spec-workflow "$HOME/.agents/skills/"
```

Restart the agent after installation.

## When To Use

Use this skill when a repository has, or should have, a documentation-driven workflow based on:

- `docs/architecture/` for stable behavior and constraints.
- `docs/tasks/` for milestones, task ordering, status, and dependencies.
- `docs/context/` for supporting research.
- Task-local `task.md`, `spec.md`, and optional `plan.md` files.

It is most helpful when you want an agent to avoid jumping straight into code and instead follow a spec-first, checkpointed implementation process.
