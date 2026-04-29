# Release Notes

User-facing workflow, installation, and migration changes are documented here.

This project follows Conventional Commits for commit history, but release notes focus on what users need to know when adopting or upgrading the workflow.

## v0.5.0

### Features

- The minimum docs scaffold now includes `docs/tasks/planning-inbox.md` so unconfirmed goals, opportunities, and roadmap candidates survive across fresh agent conversations.
- `milestone-planning` now treats `docs/tasks/planning-inbox.md` as the routing source for goals that are not yet milestone-shaped.
- Workflow routing tests now document batch-run protocols that write all result files before reading any expected files, preventing expected-output context from leaking into simulated responses.

### Fixes

- `milestone-planning` now distinguishes an empty `Open Milestones` list with no routing evidence from one that has `planning-inbox.md`, docs, or prompt evidence for either a concrete short-term target or misaligned roadmap goals.
- Root routing and `task-spec-execution` now require concrete docs or prompt evidence before treating ambiguous intent as a `superpowers:brainstorming` case.
- `docs-workflow-bootstrap` now explicitly refuses to create implementation tasks; roadmap or task-like input belongs in planning inbox context and later `milestone-planning`.
- `task-spec-execution` now defines when a task is selectable for execution and replaces vague task complexity with explicit plan triggers for deciding when `plan.md` is justified.
- `task-spec-execution` now distinguishes author-ready versus handoff-ready compact specs by expected execution mode instead of requiring an explicit handoff request every time. Same-agent continuation may stay compact, while subagents, other agents/models, and fresh conversations now default to handoff-ready anchors inside the existing spec sections.
- Checkpoint semantics are now explicit: approved planning/spec/plan docs are committed by default, while uncommitted continuation requires explicit user approval and a file-level report.
- Selectable-task and explicit-approval semantics are now defined so vague replies like `ok`, `looks good`, or `go ahead` do not accidentally cross approval gates.

### Notes

- When execution mode is already clear, `task-spec-execution` should not ask a redundant route-selection question before drafting `spec.md`.
- Handoff-ready compact specs now require three concrete anchors when another execution context is expected:
  - preferred proof samples or evidence sources
  - preferred implementation surface or first modification target
  - case-level acceptance signals

## v0.4.0

### Features

- `milestone-planning` now treats roadmap decomposition as a clearer planning stage with explicit ownership over roadmap-layer `docs/tasks/` structure, milestone boundaries, module grouping, and planning-stage backlog/handoff governance.
- `milestone-planning` now separates core planning rules, anti-patterns, and roadmap templates more cleanly:
  - high-frequency routing and closure behavior stays in the main skill
  - anti-patterns live in `references/milestone-anti-patterns.md`
  - roadmap document shape lives in `references/roadmap-template.md`
- `task-spec-execution` now exposes more of its high-frequency execution behavior directly in the main skill, including docs boundaries, branch-closing expectations, and source-of-truth guidance.
- `task-spec-execution` now treats `references/task-execution-detailed-rules.md` as a low-frequency companion for stop conditions, edge cases, and template-loading guidance rather than as a hidden second main workflow document.

### Fixes

- `task-spec-execution` now makes it explicit that bootstrap-created docs may be maintained during execution, but bootstrap ownership still belongs to `docs-workflow-bootstrap`.
- `task-spec-execution` now clarifies that compact task specs still need enough boundary detail to prevent another agent from misreading implementation intent. Ambiguous tasks should capture allowed minimal implementation, forbidden shortcuts, and boundary decisions inside existing sections such as `Goals`, `Non-goals`, `Design`, and `Testing and Verification`.
- branch-closing guidance now explicitly covers the case where a user chooses merge plus cleanup and clarifies that deleting a worktree does not by itself resolve task-branch cleanup.
- `milestone-planning` template guidance now distinguishes document shape from workflow policy more clearly: milestone confirmation, `Handoff Notes`, closure gates, and task-list semantics are documented as rules rather than buried inside the template text.
- `task-spec-execution` now requires resolving the task-planning docs checkpoint before entering task-local `spec.md` work when `milestone-planning` has just created or reshaped roadmap/task docs and stopped with an unresolved checkpoint.
- When `milestone-planning` creates the first concrete task in a milestone, the resulting task docs are treated as planning-governance output first, not as automatic permission to draft the first task spec.
- Two `continue` steps are now required across the planning-to-execution handoff: first `continue` resolves the task-planning docs checkpoint (commit the new planning docs), second `continue` enters `task-spec-execution` and begins drafting `spec.md`.
- Reporting milestone-entry governance changes in `task-spec-execution` no longer substitutes for resolving the task-planning docs checkpoint created by `milestone-planning`.

### Notes

- This release is primarily a skill-boundary and discoverability refinement rather than a new workflow stage.
- Docs and tests now refer to upstream Superpowers skills by canonical names such as `superpowers:brainstorming`.
- The main intent is to make the high-frequency rules visible in each stage's primary `SKILL.md` while keeping low-frequency examples, anti-patterns, and templates in `references/`.
- In practice, this should reduce the chance that an agent loads a stage skill, misses a critical approval gate, and only discovers the real rule after diving into a reference file.
- `milestone-planning` is now closer to a stable split:
  - `SKILL.md` for planning decisions and handoff rules
  - `milestone-detailed-rules.md` for finer routing/closure policy
  - `roadmap-template.md` for file shape
- `task-spec-execution` remains the heaviest stage skill, but this release makes that weight more honest by putting the most frequently needed rules back in the main file instead of treating them as optional reference material.
- The test suite under `tests/workflow-routing/` has been restructured: each test case is now split into a `.prompt.md` (simulated user input) and a `.expected.md` (expected skill, behavior, file changes, and forbidden behaviors).
- Three new test cases were added: `first-task-in-new-milestone-needs-explicit-selection` (two-`continue` sequencing across planning checkpoint and spec drafting), `milestone-close-handoff-notes-blocked` (non-empty `Handoff Notes` blocks milestone closure), and `milestone-close-handoff-notes-cleared` (cleared `Handoff Notes` allows milestone closure).
- The existing test case `milestone-close-handoff-notes-gate` was removed; its coverage is now split across the two new handoff-notes cases above.

## v0.3.1

### Fixes

- `milestone-planning` now treats crossing from one milestone to the next as a separate governance decision instead of assuming "start the next task" authorizes direct task selection in the later milestone.
- `milestone-planning` now stops when the previous milestone still appears open or the target milestone is still marked `Roadmap confirmed: no`, and routes through milestone closure/confirmation first.
- `task-spec-execution` now blocks starting a task in `M(n+1)` when `M(n)` still has unresolved closure or the new milestone is not explicitly confirmed.
- milestones now treat `Exit Criteria` as persistent checklist items to verify at closure time instead of temporary text to remove after completion.
- milestone roadmap docs now use optional `Handoff Notes` instead of `Current Gaps` for carry-forward findings discovered during a completed milestone.
- `milestone-planning` now requires every retained handoff note to be explicitly attached to a later milestone or backlog before the current milestone can close.
- `milestone-planning` now treats `Handoff Notes` as a temporary transfer queue that must be empty before milestone closure.
- milestone roadmap docs now support an optional `docs/tasks/backlog.md` for roadmap items that are worth keeping but not yet attached to a milestone.
- tasks inside milestones marked `Roadmap confirmed: no` are now treated as candidate tasks only until milestone entry is explicitly confirmed.
- roadmap templates now simplify module indexes by removing standalone `Recommended Order` and `Dependency Notes` sections; default order follows task numbering and task-level `Dependencies`.
- execution-side index templates are now fully English again, matching the repository convention outside `README_CN.md`.

### Notes

- The workflow now distinguishes three separate checkpoints: previous task branch closing, previous milestone closure, and next milestone roadmap confirmation.
- A message like "continue" or "start the next task" should no longer be interpreted as permission to skip milestone closure and jump straight into a later milestone task.
- `Handoff Notes` is for later-milestone follow-up only; it should not duplicate task status or keep an otherwise-complete milestone artificially open.
- A handoff note is only valid if it has somewhere to go next; otherwise it is unresolved roadmap work, not a completed handoff.
- After a handoff item is moved to its destination, remove it from the source milestone instead of keeping it as historical residue.
- New follow-up discussion discovered during execution should land in the current milestone's `Handoff Notes` first, not jump directly into backlog.
- Before milestone closure, every `Handoff Notes` item must resolve into exactly one outcome: current-milestone open work, a later milestone, `docs/tasks/backlog.md`, or removal if it is no longer worth tracking.
- Backlog is now a deferred routing pool rather than a running history list: when an item is attached to a milestone or task, remove it from backlog instead of marking it completed there.
- Revisit backlog during roadmap planning and when changing `Roadmap confirmed: no` to `yes`; those are the main points where backlog items should be pulled into milestones or concrete tasks.
- `Roadmap confirmed: no` can still allow provisional task breakdown for planning, but those tasks are not formal execution tasks until the milestone is confirmed.
- `docs/tasks/<milestone>/index.md` now makes that candidate-task status explicit in the milestone `Status` section.
- Task dependencies should now live on concrete `task.md` files rather than being repeated in roadmap-layer indexes.

## v0.3.0

### Features

- `milestone-planning` now asks whether the user needs mid/long-term roadmap alignment or decomposition of an already-defined target before it proposes milestone structure.
- When `Open Milestones` is empty because roadmap goals are not aligned yet, `milestone-planning` now routes to `superpowers:brainstorming` first and prefers shaping at least three milestones before detailed decomposition.
- When the user already has a concrete short-term goal, especially in enterprise or iteration-driven scenarios with a clear case, `milestone-planning` now skips `superpowers:brainstorming` and decomposes the current iteration directly.
- `milestone-planning` now treats milestone confirmation as an explicit routing signal for task decomposition. Use `Roadmap confirmed: no` on a milestone to force a routing question before decomposing tasks, and flip it once the user confirms staying on that path.

### Notes

- An empty `Open Milestones` list is now treated as a decision point, not an automatic signal to decompose immediately.
- The new default is: first determine whether the user needs roadmap alignment or execution planning, then choose `superpowers:brainstorming` or direct milestone decomposition accordingly.
- Explicit unconfirmed milestones now behave like a guarded handoff: ask whether to re-evaluate the milestone structure or continue on the current route before task breakdown starts.

## v0.2.2

### Fixes

- `task-spec-execution` now requires an approved task-local docs checkpoint before branch/worktree isolation for implementation.
- `task-spec-execution` no longer defaults to carrying approved-but-uncommitted `spec.md` or `plan.md` into an implementation worktree or task branch.

### Notes

- Default flow is now `spec -> approval -> docs checkpoint -> implementation`.
- If a task-local `plan.md` exists, checkpoint it together with the approved `spec.md` before implementation isolation.

## v0.2.1

### Fixes

- `task-spec-execution` now treats branch closing as unresolved until a merged task branch is explicitly deleted or explicitly kept, even after worktree cleanup.
- `task-spec-execution` now points to `superpowers:finishing-a-development-branch` for merge, PR, keep, discard, and cleanup decisions after implementation is complete.

### Notes

- Removing a worktree does not remove its merged task branch.
- If implementation is complete and Git integration remains, prefer using `task-spec-execution` together with `superpowers:finishing-a-development-branch`.

## v0.2.0

### Features

- The workflow moved from one combined skill to a staged model:

  ```text
  doc-driven-spec-workflow -> docs-workflow-bootstrap -> superpowers:brainstorming -> milestone-planning -> task-spec-execution
  ```

- Added `docs-workflow-bootstrap` for minimum docs scaffold initialization.
- Added `milestone-planning` for roadmap decomposition and task selection.
- Added `task-spec-execution` for task-local spec, optional plan, readiness, implementation governance, verification, and branch closing.
- `doc-driven-spec-workflow` became the public root entry point and stage router.
- The repository split stage ownership more clearly:
  - `docs-workflow-bootstrap` initializes the minimum docs scaffold.
  - `milestone-planning` owns roadmap decomposition.
  - `task-spec-execution` owns task-local spec/plan/readiness/execution flow.
- Template ownership moved out of the root skill:
  - roadmap templates live under `skills/milestone-planning/references/`
  - execution templates live under `skills/task-spec-execution/references/`

### Breaking Changes

- The old execution-stage meaning of `doc-driven-spec-workflow` moved to `task-spec-execution`.
- Replace old root-skill execution usage of `doc-driven-spec-workflow` with `task-spec-execution`.
- Do not use `task-spec-execution` to invent or reshape roadmap structure; use `milestone-planning` first.
- If you referenced `skills/doc-driven-spec-workflow/references/` directly, update those template paths.

## v0.1.0

Initial public docs-driven spec workflow baseline.
