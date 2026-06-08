# Doc-Driven Spec Workflow

[中文说明](./README_CN.md) · [Workflow Structure](./WORKFLOW-STRUCTURE.md) · [Release Notes](./RELEASE-NOTES.md)

A docs-driven workflow methodology for AI coding agents.

This repository packages a reusable methodology for keeping implementation work aligned with project documentation. It is useful for repositories that organize work around architecture docs, task roadmaps, task-local specs, optional plans, and explicit readiness checks before code changes.

> Opinionated workflow methodology
>
> This project is intentionally focused on docs-driven repositories. It is not a general replacement for every agent development workflow; it is a lightweight way to make agents respect architecture docs, task tracking, roadmap decomposition, review pauses, and branch readiness before implementation.

## How It Works

This workflow is split into local stage skills. The root skill, `doc-driven-spec-workflow`, decides which stage comes next and where the agent must stop.

The stage chain is:

`doc-driven-spec-workflow -> docs-workflow-bootstrap -> planning-clarification -> milestone-planning -> task-preparation -> task-execution-simple`

Use each stage only when needed:

- Start with `doc-driven-spec-workflow` when the main question is which stage comes next.
- Use `docs-workflow-bootstrap` when the repository needs the minimum docs scaffold.
- Use `planning-clarification` only when goals, scope, or success criteria are still unclear.
- Use `milestone-planning` when the roadmap shape is unclear and you need to decide milestones, modules, and tasks.
- Use `task-preparation` after the current concrete task is selected from confirmed roadmap state and no prior hard gate still blocks task-local spec/plan work.
- Use `task-execution-simple` after task-local docs and review follow-up are complete and the task is ready for straightforward direct implementation.

The root skill only routes and hands off context. Stage skills own their own rules, templates, and stop points.

## Skills Library

This repository currently contains six local workflow skills:

| Skill | Responsibility | Stop Point |
| --- | --- | --- |
| `doc-driven-spec-workflow` | Route work to the right workflow stage | When the next stage is clear |
| `docs-workflow-bootstrap` | Initialize the minimum docs scaffold | When core docs entry points are created |
| `planning-clarification` | Clarify ambiguous planning direction before roadmap decomposition | When scope, stage boundaries, and first roadmap slice direction are clear enough to continue |
| `milestone-planning` | Decompose scope into `Milestone -> optional Module -> Task` | When roadmap docs are updated, or the current task is selected |
| `task-preparation` | Prepare a selected task via `spec -> optional plan -> review -> routine follow-up` | When task-local docs are ready to hand off into execution |
| `task-execution-simple` | Implement a prepared task through the simple direct execution path | When the current implementation review pause or any remaining hard gate is resolved |

Roadmap planning and task reshaping are docs governance work. They do not automatically authorize spec writing or code changes.

## Quick Start

Install this repository as a workflow skill set:

```bash
npx skills add Adol1111/doc-driven-spec-workflow
```

Install the full set by default. See [Installation](#installation) for single-stage installs, global agent targets, or manual copies.

## Bootstrap A Repository

To initialize the minimum docs scaffold in a repository, ask your agent:

```text
Use docs-workflow-bootstrap to initialize the docs workflow scaffold for this repository.
```

This should create the core entry points:

```text
docs/
├── index.md
├── architecture/
│   └── index.md
├── tasks/
│   ├── index.md
│   ├── planning-inbox.md
│   └── backlog.md
└── context/
    └── index.md
```

`docs/tasks/planning-inbox.md` keeps future goals and candidate milestones visible across fresh agent conversations. A goal is a desired future state, product outcome, opportunity, or phase direction; it is not just any future work item. `docs/tasks/backlog.md` keeps concrete deferred tasks available for milestone planning and confirmation.

The workflow does not create `docs/specs/` or `docs/plans/` by default. Task-local `spec.md` and `plan.md` files should be created under `docs/tasks/<milestone>/<task>/` when there is a concrete task. Global `docs/specs/` and `docs/plans/` are reserved for standalone or cross-task documents.

A plan trigger means execution sequencing is non-obvious: ordered multi-file changes, migrations, compatibility boundaries, cross-module coordination, phased rollout, verification-order risk, or a required spike.

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
Use docs-workflow-bootstrap to initialize the docs workflow scaffold for this repository. Write all generated docs in Chinese.
```

You can also fork this repository and translate the files under each skill's `references/` directory if you want the template headings themselves to be localized.

## Usage

After installation, ask your agent to use the root workflow skill when starting or continuing work in a docs-driven repository.

Recommended entry point when you are unsure which stage comes next:

```text
Use doc-driven-spec-workflow to decide whether this request needs bootstrap, planning clarification, milestone planning, task preparation, or simple task execution.
```

After entering through `doc-driven-spec-workflow`, you can usually keep moving stage by stage with any message that clearly expresses "go forward from here." The root skill should route to one stage skill at a time and carry forward handoff context. After a review pause, that forward-motion intent should mean "follow the recommended next step," including routine actions such as committing reviewed docs or creating branch isolation. Explicit confirmation is still reserved for hard gates such as keeping an explicitly unconfirmed roadmap shape, staying on a risky current branch, or deleting branches/worktrees.

Use the roadmap decomposition skill directly when the main question is milestone or task structure:

```text
Use milestone-planning to break this scope into milestones, modules, and tasks.
```

Use the task-preparation skill directly when the concrete task is selected from confirmed roadmap state and dependencies and prior hard gates are clear:

```text
Use task-preparation to prepare the selected task by writing the spec.
```

Use the simple execution skill directly when task-local docs are ready and the next work is direct implementation:

```text
Use task-execution-simple to implement the prepared task.
```

For Claude Code, you can also invoke the individual skills directly:

```text
/doc-driven-spec-workflow
/docs-workflow-bootstrap
/planning-clarification
/milestone-planning
/task-preparation
/task-execution-simple
```

These skills are designed for repositories that use `docs/architecture/`, `docs/tasks/`, `docs/context/`, task-local `spec.md`, and optional `plan.md` files.

## Example Workflow

1. Route the request with `doc-driven-spec-workflow`.
2. Use `docs-workflow-bootstrap` if the repository still needs the minimum docs scaffold.
3. Clarify ambiguous intent with `planning-clarification` when needed.
4. Use `milestone-planning` to decide milestone, module, and task structure when the roadmap shape is still unclear.
5. Select the current concrete task under `docs/tasks/`.
6. Use `task-preparation` to write or update the task-local `spec.md`.
7. Stop for review after `spec.md`, and after `plan.md` when needed.
8. When the user clearly asks to move forward, let `task-preparation` handle the routine next step such as committing reviewed docs.
9. Hand off to `task-execution-simple` for branch/worktree isolation, implementation, verification, and docs/status updates.
10. Stop again for implementation review, then resolve one explicit branch-closing outcome: merge and keep branch, merge and delete branch, or discard work.

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

Task directory names should be stable slugs, not order markers. Put tasks in the intended order in the milestone or module `index.md`; inserting or reordering work should not require renaming existing task directories.

## Notes

- `task-preparation` and `task-execution-simple` can run on their own once a concrete task is selected from confirmed roadmap state.
- Clarification, execution isolation, and simple branch-closing rules are local to this skill set.
- Do not start implementation on an unsafe current branch.
- Do not start a new task while branch closing is unresolved.
- Use Superpowers when you want a broader end-to-end methodology. Use this workflow when your main need is docs-driven planning, spec-first execution, and explicit checkpoints.

## Installation

### Install With `npx skills` (Recommended)

Install this repository as a workflow skill set:

```bash
npx skills add Adol1111/doc-driven-spec-workflow
```

Install all skills from the repo explicitly:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill '*'
```

Install a specific skill by name using the skill list above:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning
```

Add agent targets when needed:

```bash
npx skills add Adol1111/doc-driven-spec-workflow -g -a claude-code
npx skills add Adol1111/doc-driven-spec-workflow -g -a codex
```

Combine flags for a specific agent and skill:

```bash
npx skills add Adol1111/doc-driven-spec-workflow --skill milestone-planning -g -a codex
```

You can also install directly from a skill path:

```bash
npx skills add https://github.com/Adol1111/doc-driven-spec-workflow/tree/main/skills/docs-workflow-bootstrap
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
scripts/install-skill-from-github.py --repo Adol1111/doc-driven-spec-workflow --path skills/milestone-planning
```

### Manual Install For Claude Code

Claude Code discovers personal skills from `~/.claude/skills/`:

```bash
mkdir -p "$HOME/.claude/skills"
cp -R skills/<skill-name> "$HOME/.claude/skills/"
```

For a project-local Claude Code skill shared with a repository:

```bash
mkdir -p .claude/skills
cp -R skills/<skill-name> .claude/skills/
```

### Manual Install For Codex

Codex discovers skills from `$CODEX_HOME/skills`, or `~/.codex/skills` when `CODEX_HOME` is unset:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/<skill-name> "${CODEX_HOME:-$HOME/.codex}/skills/"
```

### Manual Install For Other Agents

If your agent uses a different skill directory, copy the installable skill folders into that directory:

```bash
cp -R skills/<skill-name> /path/to/agent/skills/
```

For example, in an environment that discovers skills from `~/.agents/skills`:

```bash
mkdir -p "$HOME/.agents/skills"
cp -R skills/<skill-name> "$HOME/.agents/skills/"
```

## When To Use

Use this skill when a repository has, or should have, a documentation-driven workflow based on:

- `docs/architecture/` for stable behavior and constraints.
- `docs/tasks/` for milestones, index-driven task order, status, and dependencies.
- `docs/context/` for supporting research.
- Task-local `task.md`, `spec.md`, and optional `plan.md` files.

It is most helpful when you want an agent to avoid jumping straight into code and instead follow a spec-first, checkpointed implementation process.
