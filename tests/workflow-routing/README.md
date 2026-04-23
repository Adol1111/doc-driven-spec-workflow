# Workflow Routing Tests

These are lightweight behavior tests for the docs-driven workflow skills.

They are not unit tests. They are prompt-based scenarios for checking whether an agent routes to the right stage skill, stops at the right checkpoint, and avoids crossing ownership boundaries.

## How To Run Manually

Run each case in a fresh agent conversation when possible.

Use this prompt for routing-only checks:

```text
Use doc-driven-spec-workflow.

Run the workflow-routing test case in tests/workflow-routing/cases/<case-name>.md.
Treat it as an isolated simulated conversation.
Do not edit repository files unless the test case explicitly expects file changes.
Use only the Prompt section to produce the initial simulated agent response; use Expected sections only afterward for self-check.
First respond to the Prompt section as the agent would.
Then perform a self-check against Expected Skill, Expected Behavior, and Must Not.
Mark the result as PASS, WARN, or FAIL.
```

Use this prompt when you want to inspect generated files:

```text
Use doc-driven-spec-workflow.

Run the workflow-routing test case in tests/workflow-routing/cases/<case-name>.md.
Treat it as an isolated simulated conversation.
Before running the case or case set, clean tests/workflow-routing/expected/ once.
When the test case explicitly expects file changes, create them under tests/workflow-routing/expected/<case-name>/ as the simulated repository root instead of editing the real repository root.
When running several cases, keep each case output in its own tests/workflow-routing/expected/<case-name>/ directory so all generated results remain inspectable after the run.
Use only the Prompt section to produce the initial simulated agent response; use Expected sections only afterward for self-check.
First respond to the Prompt section as the agent would.
Then perform a self-check against Expected Skill, Expected Behavior, Must Not, and Expected File Changes.
Mark the result as PASS, WARN, or FAIL.
```

## Test Protocol

For each case:

1. Read the `Prompt` section as the simulated user request.
2. Produce the initial simulated agent response using only the `Prompt` section and the loaded workflow skill instructions.
3. If running a file-generating check, clear `tests/workflow-routing/expected/` once before the run.
4. If the case expects file changes, write them under `tests/workflow-routing/expected/<case-name>/` only.
5. Compare the response with `Expected Skill`, `Expected Behavior`, `Expected Output Shape`, `Expected File Changes`, and `Must Not`.
6. Mark the result:
   - `PASS`: correct skill, correct stop point, no forbidden behavior
   - `WARN`: mostly correct, but wording or handoff could confuse users
   - `FAIL`: wrong skill, skipped an approval gate, or performed forbidden behavior

## Isolation Notes

- Prefer one fresh conversation per case.
- If running several cases in one conversation, explicitly say each case is isolated.
- Do not let a previous case's simulated repository state affect the next case.
- Routing-only checks do not edit files.
- File-generating checks use `tests/workflow-routing/expected/<case-name>/` as each case's disposable simulated repository root.
- `tests/workflow-routing/expected/` is ignored by Git and should be cleaned once before each file-generating run.
- Keep case outputs until the next run so generated files remain inspectable.

## Cases

- `approved-spec-needs-checkpoint.md`: approved task-local docs must be checkpointed before branch/worktree isolation for implementation.
- `branch-closing-after-worktree.md`: merged task branches must be explicitly deleted or kept after worktree cleanup.
- `bootstrap-needed.md`: missing docs scaffold should route to `docs-workflow-bootstrap`.
- `empty-open-milestones-needs-alignment.md`: an empty `Open Milestones` list plus unclear roadmap goals should route to `brainstorming` before decomposition.
- `empty-open-milestones-asks-routing-question.md`: an empty `Open Milestones` list without enough context should trigger a routing question before any recommendation.
- `iteration-breakdown.md`: a concrete iteration target should route directly to `milestone-planning` without detouring through `brainstorming`.
- `placeholder-milestone-asks-routing-question.md`: a placeholder open milestone should trigger a routing question before direct decomposition.
- `roadmap-needed.md`: broad product scope should route to `milestone-planning`.
- `roadmap-no-mechanical-split.md`: implementation-mechanical task requests should be corrected into capability-level roadmap tasks.
- `roadmap-small-output.md`: small roadmap scope should route to `milestone-planning` and generate inspectable roadmap-layer task docs.
- `selected-task-spec.md`: selected concrete task should route to `task-spec-execution`.
- `task-too-broad.md`: too-broad task should return to `milestone-planning`.
- `unconfirmed-milestone-asks-routing-question.md`: an explicit `Roadmap confirmed: no` milestone should trigger a routing question before direct decomposition.
- `continue-without-approval.md`: `continue` must not skip approval gates.
