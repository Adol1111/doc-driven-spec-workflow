# Doc-Driven Spec Workflow

[中文说明](./README_CN.md)

A docs-driven spec workflow skill for AI coding agents.

This repository packages a reusable workflow for keeping implementation work aligned with project documentation. It is useful for repositories that organize work around architecture docs, task roadmaps, task-local specs, optional plans, and explicit readiness checkpoints before code changes.

> Opinionated workflow skill
>
> This project is intentionally focused on docs-driven repositories. It is not a general replacement for every agent development workflow; it is a lightweight way to make agents respect architecture docs, task tracking, spec approval, and branch readiness before implementation.

## Quick Start

Install with the open agent skills CLI:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow
```

For a global Claude Code install:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code
```

For a global Codex install:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a codex
```

Restart your agent after installation so it can discover the new skill.

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

After installation, ask your agent to use the workflow when starting or continuing implementation work in a docs-driven repository:

```text
Use doc-driven-spec-workflow to pick the next task and write the spec.
```

For Claude Code, you can also invoke it directly:

```text
/doc-driven-spec-workflow
```

The skill is designed to activate when a repository uses `docs/architecture/`, `docs/tasks/`, `docs/context/`, task-local `spec.md`, and optional `plan.md` files.

## Example Workflow

1. Clarify ambiguous intent with `brainstorming` or an equivalent clarification flow.
2. Read the relevant architecture, task, and context docs.
3. Select or create the concrete task under `docs/tasks/`.
4. Write or update the task-local `spec.md`.
5. Stop for user approval before implementation.
6. Create `plan.md` only when the task is genuinely complex.
7. Run the readiness checkpoint and isolate work with a branch or worktree.
8. Implement, verify, update docs/status, and resolve branch closing.

## What It Does

- Treats `docs/tasks/` as the source of truth for concrete implementation work.
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

This skill can work on its own, but it references two optional workflow skills from [obra/superpowers](https://github.com/obra/superpowers):

- `brainstorming`: Clarifies ambiguous feature, behavior, or task intent before selecting a concrete task or writing a spec.
- `using-git-worktrees`: Creates safe branch/worktree isolation when a workspace is dirty, shared, risky, or likely to conflict.

If your agent environment does not have these skills, use equivalent clarification and git isolation workflows instead. Preserve the same safety rules: clarify unclear intent before locking a spec, do not start concrete implementation on an unsafe current branch, and do not delete or merge branches/worktrees without an explicit closing decision.

## Why Not Just Use Superpowers?

Superpowers is a broader software development methodology with many composable skills for brainstorming, planning, TDD, subagents, code review, verification, and branch finishing. This workflow is intentionally narrower:

- It is organized around a repository's durable documentation structure: `docs/architecture/`, `docs/tasks/`, `docs/context/`, task-local `spec.md`, and optional `plan.md`.
- It treats `docs/tasks/` as the source of truth for selecting concrete work, tracking milestone status, and preventing agents from inventing implementation tasks directly from architecture notes.
- It separates docs governance from implementation permission, so architecture edits, roadmap reshaping, and index maintenance do not automatically authorize code changes.
- It keeps TDD, heavyweight planning, and subagent workflows optional instead of mandatory, which makes it easier to use in projects that want spec-first coordination without adopting the full Superpowers methodology.
- It can still compose with Superpowers where useful, especially `brainstorming` before ambiguous specs and `using-git-worktrees` before risky implementation work.

Use Superpowers when you want the full end-to-end agentic development methodology. Use this workflow when your main need is to keep agents aligned with a docs-driven architecture, task roadmap, and spec approval process.

## Installation

### Install With `npx skills` (Recommended)

Install the skill with the open agent skills CLI:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow
```

For a global Claude Code install:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code
```

For a global Codex install:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a codex
```

For a global install to both Claude Code and Codex:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill doc-driven-spec-workflow -g -a claude-code -a codex
```

You can also install directly from the skill path:

```bash
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/doc-driven-spec-workflow
```

If you fork this repository, replace `Adol1111/doc-driven-spec-workflow` with your fork's `<owner>/<repo>` name.

Restart your agent after installation so it can discover the new skill.

### Install With Codex Skill Installer

Install it by pointing the installer at the skill path:

```bash
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/doc-driven-spec-workflow
```

Restart your agent after installation so it can discover the new skill.

### Manual Install For Claude Code

Claude Code discovers personal skills from `~/.claude/skills/`:

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/doc-driven-spec-workflow "$HOME/.claude/skills/"
```

For a project-local Claude Code skill shared with a repository:

```bash
mkdir -p .claude/skills
cp -R skills/doc-driven-spec-workflow .claude/skills/
```

Claude Code also supports invoking the skill directly as `/doc-driven-spec-workflow` after it is installed.

### Manual Install For Codex

Codex discovers skills from `$CODEX_HOME/skills`, or `~/.codex/skills` when `CODEX_HOME` is unset:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/doc-driven-spec-workflow "${CODEX_HOME:-$HOME/.codex}/skills/"
```

Restart Codex after copying the skill.

### Manual Install For Other Agents

If your agent uses a different skill directory, copy the installable skill folder into that directory:

```bash
cp -R skills/doc-driven-spec-workflow /path/to/agent/skills/
```

For example, in an environment that discovers skills from `~/.agents/skills`:

```bash
mkdir -p "$HOME/.agents/skills"
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
