# Doc-Driven Spec Workflow

A docs-driven spec workflow skill for AI coding agents.

This repository packages a reusable workflow for keeping implementation work aligned with project documentation. It is useful for repositories that organize work around architecture docs, task roadmaps, task-local specs, optional plans, and explicit readiness checkpoints before code changes.

## What It Does

- Treats `docs/tasks/` as the source of truth for concrete implementation work.
- Requires task-local specs before implementation and optional plans for complex work.
- Keeps architecture, task tracking, specs, and status updates aligned.
- Separates docs governance from implementation permission.
- Enforces readiness checkpoints before code edits, including branch or worktree isolation.
- Provides compact templates for architecture docs, task indexes, specs, plans, and context notes.

## Repository Layout

```text
.
├── README.md
└── skills/
    └── doc-driven-spec-workflow/
        ├── SKILL.md
        ├── agents/
        │   └── openai.yaml
        └── references/
            ├── architecture-template.md
            ├── context-template.md
            ├── index-template.md
            ├── plan-template.md
            ├── spec-template.md
            └── tasks-template.md
```

The installable skill is located at `skills/doc-driven-spec-workflow/`.

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

### Install With `npx skills`

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

## Recommended GitHub Description

```text
A docs-driven spec workflow skill for AI coding agents.
```
