# Workflow Routing Tests

These are lightweight behavior tests for the docs-driven workflow skills.

They are not unit tests. They are prompt-based scenarios for checking whether an agent routes to the right stage skill, stops at the right checkpoint, and avoids crossing ownership boundaries.

## How To Run Manually

Run each case in a fresh agent conversation when possible.

Use this prompt for routing-only checks:

```text
Use doc-driven-spec-workflow.

Run the workflow-routing test case prompt in tests/workflow-routing/cases/<case-name>.prompt.md.
Treat it as an isolated simulated conversation.
Do not edit repository files unless the test case explicitly expects file changes.

IMPORTANT — preserve context isolation:
1. First, clear any previous output by writing an empty result file:
   Write an empty string to tests/workflow-routing/expected/result.md.
   Do NOT read tests/workflow-routing/expected/result.md before writing — you must not see previous run output.
2. Read the prompt file at tests/workflow-routing/cases/<case-name>.prompt.md.
3. Produce the simulated agent response and write it to tests/workflow-routing/expected/result.md.
   Do NOT read tests/workflow-routing/cases/<case-name>.expected.md yet.
4. Only after step 3 is complete, read tests/workflow-routing/cases/<case-name>.expected.md.
5. Compare the output in result.md against Expected Skill, Expected Behavior, and Must Not.
   Output PASS, WARN, or FAIL with evidence.
```

Use this prompt when you want to inspect generated files:

```text
Use doc-driven-spec-workflow.

Run the workflow-routing test case prompt in tests/workflow-routing/cases/<case-name>.prompt.md.
Treat it as an isolated simulated conversation.

IMPORTANT — preserve context isolation:
1. First, clean the output directory:
   Delete tests/workflow-routing/expected/<case-name>/ if it exists, then recreate it empty.
   Do NOT read any files under tests/workflow-routing/expected/<case-name>/ before writing — you must not see previous run output.
2. Read the prompt file at tests/workflow-routing/cases/<case-name>.prompt.md.
3. Produce the simulated agent response. When the test case expects file changes, write them under
   tests/workflow-routing/expected/<case-name>/ as the simulated repository root instead of editing the real repository root.
   Also write the agent's text response to tests/workflow-routing/expected/<case-name>/response.md.
   Do NOT read tests/workflow-routing/cases/<case-name>.expected.md yet.
4. Only after step 3 is complete, read tests/workflow-routing/cases/<case-name>.expected.md.
5. Compare the output against Expected Skill, Expected Behavior, Must Not, and Expected File Changes.
   Output PASS, WARN, or FAIL with evidence.
```

## Test Protocol

For each case, the agent must follow this sequence strictly to prevent context pollution:

### Routing-only cases

1. **Clear output:** Write an empty string to `tests/workflow-routing/expected/result.md`. Do NOT read the file first — stale output from a previous run must not enter context.
2. **Read prompt:** Read `tests/workflow-routing/cases/<case-name>.prompt.md` as the simulated user request.
3. **Write response:** Produce the simulated agent response using only the prompt file and the loaded workflow skill instructions. Write it to `tests/workflow-routing/expected/result.md`. Do NOT read `tests/workflow-routing/cases/<case-name>.expected.md` yet.
4. **Read expected:** Only after step 3 is complete, read `tests/workflow-routing/cases/<case-name>.expected.md`.
5. **Compare and grade:** Compare the response against `Expected Skill`, `Expected Behavior`, and `Must Not` from the expected file. Mark as `PASS`, `WARN`, or `FAIL`.

### File-generating cases

1. **Clean output directory:** Delete `tests/workflow-routing/expected/<case-name>/` if it exists, then recreate it empty. Do NOT read any files in it first.
2. **Read prompt:** Read `tests/workflow-routing/cases/<case-name>.prompt.md`.
3. **Write files + response:** Write generated files under `tests/workflow-routing/expected/<case-name>/` as the simulated repository root. Write the agent's text response to `tests/workflow-routing/expected/<case-name>/response.md`. Do NOT read `tests/workflow-routing/cases/<case-name>.expected.md` yet.
4. **Read expected:** Only after step 3 is complete, read `tests/workflow-routing/cases/<case-name>.expected.md`.
5. **Compare and grade:** Compare the response and generated files against `Expected Skill`, `Expected Behavior`, `Must Not`, and `Expected File Changes`. Mark as `PASS`, `WARN`, or `FAIL`.

### Grading rules

- `PASS`: correct skill, correct stop point, no forbidden behavior
- `WARN`: mostly correct, but wording or handoff could confuse users
- `FAIL`: wrong skill, skipped an approval gate, or performed forbidden behavior

## Self-Check Discipline

- Self-checks must compare the initial response against `Expected Behavior` item by item, not by overall impression.
- A response must not be marked `PASS` unless every `Expected Behavior` item is explicitly satisfied.
- If a response is broadly on track but misses one or more required actions from `Expected Behavior`, mark it `WARN`, not `PASS`.
- If any `Must Not` item is violated, mark it `FAIL`.
- If `Expected File Changes` are required and missing or incorrect, do not mark the result `PASS`.
- The self-check should quote or summarize concrete evidence from the response for each expected item.

Use this self-check shape:

```text
Expected Behavior Check
1. <expected item>: MET / NOT MET
Evidence: <quote or short explanation>

2. <expected item>: MET / NOT MET
Evidence: <quote or short explanation>

Must Not Check
1. <must not item>: VIOLATED / NOT VIOLATED
Evidence: <quote or short explanation>

Expected File Changes Check
1. <expected file change item>: MET / NOT MET
Evidence: <quote or short explanation>

Result: PASS/WARN/FAIL
Reason:
```

## Isolation Notes

- Prefer one fresh conversation per case.
- If running several cases in one conversation, explicitly say each case is isolated.
- Do not let a previous case's simulated repository state affect the next case.
- Routing-only checks do not edit repository files.
- File-generating checks use `tests/workflow-routing/expected/<case-name>/` as each case's disposable simulated repository root.
- `tests/workflow-routing/expected/` is ignored by Git and should be cleaned once before each file-generating run.
- Keep case outputs until the next run so generated files remain inspectable.

## Cases

Each case below refers to a `<case-name>.prompt.md` + `<case-name>.expected.md` pair.

- `approved-spec-needs-checkpoint`: approved task-local docs must be checkpointed before branch/worktree isolation for implementation.
- `branch-closing-after-worktree`: merged task branches must be explicitly deleted or kept after worktree cleanup.
- `bootstrap-needed`: missing docs scaffold should route to `docs-workflow-bootstrap`.
- `bootstrap-overreach-request`: even when the user bundles roadmap, task selection, and `spec.md` requests into bootstrap, the workflow should still stop at minimum scaffold creation.
- `empty-open-milestones-needs-alignment`: an empty `Open Milestones` list plus unclear roadmap goals should route to `superpowers:brainstorming` before decomposition.
- `empty-open-milestones-asks-routing-question`: an empty `Open Milestones` list without enough context should trigger a routing question before any recommendation.
  These two cases are the same routing family with different pressure sources: one should ask a routing question, the other should route to alignment.
- `cross-milestone-transition-requires-closure`: finishing one milestone does not authorize jumping into the next milestone while closure and roadmap confirmation are still unresolved.
- `first-task-in-new-milestone-needs-explicit-selection`: after `milestone-planning` creates the first concrete task in a new milestone, one case should explain that the first `continue` resolves the task-planning checkpoint and the second `continue` begins drafting `spec.md` only.
- `milestone-close-handoff-notes-blocked`: a milestone must not close while `Handoff Notes` still contains unresolved transfer items.
- `milestone-close-handoff-notes-cleared`: a milestone may close once its own work is done and `Handoff Notes` has been cleared after transfer.
- `iteration-breakdown`: a concrete iteration target should route directly to `milestone-planning` without detouring through `superpowers:brainstorming`.
- `placeholder-milestone-asks-routing-question`: a placeholder open milestone should trigger a routing question before direct decomposition.
- `placeholder-milestone-asks-routing-question` and `unconfirmed-milestone-asks-routing-question` are the same guarded-decomposition family with different signals: placeholder naming versus explicit `Roadmap confirmed: no`.
- `roadmap-needed`: broad product scope should route to `milestone-planning`.
- `roadmap-no-mechanical-split`: implementation-mechanical task requests should be corrected into capability-level roadmap tasks.
- `roadmap-small-output`: small roadmap scope should route to `milestone-planning` and generate inspectable roadmap-layer task docs.
- `selected-task-spec`: selected concrete task should route to `task-spec-execution`.
- `selected-task-skip-spec-and-code`: a selected concrete task still must not skip task-local spec work just because the user wants to code immediately.
- `task-too-broad`: too-broad task should return to `milestone-planning`.
- `unconfirmed-milestone-asks-routing-question`: an explicit `Roadmap confirmed: no` milestone should trigger a routing question before direct decomposition.
- `unconfirmed-milestone-continue-current-path`: after the user explicitly chooses to keep the current milestone path, `milestone-planning` should continue with governance and decomposition instead of re-asking the routing question or jumping into execution.
- `continue-without-approval`: `continue` must not skip approval gates.
