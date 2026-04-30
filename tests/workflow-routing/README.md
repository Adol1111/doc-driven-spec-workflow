# Workflow Routing Tests

Prompt-based pressure tests for the docs-driven workflow skills. They check skill routing, stop points, review-pause behavior, hard-gate behavior, and ownership boundaries.

## Layout

Cases live under `tests/workflow-routing/cases/<group>/` as paired files:

- `<case-name>.prompt.md`
- `<case-name>.expected.md`

Current groups:

- `bootstrap`
- `planning-inbox`
- `milestone-planning`
- `task-execution`
- `checkpoints-closing`

Use a group directory as the default run boundary. Do not choose arbitrary numeric batches such as "five cases at a time"; if a group becomes too large, split that group into smaller semantic subdirectories first.

## Single Case Prompt

```text
Use doc-driven-spec-workflow.

Run the workflow-routing test case prompt in tests/workflow-routing/cases/<group>/<case-name>.prompt.md.
Treat it as an isolated simulated conversation.
Do not edit repository files unless the test case explicitly expects file changes.

IMPORTANT — preserve context isolation:
1. Clear previous output first:
   Delete and recreate tests/workflow-routing/expected/<group>/.
   Do NOT only clear tests/workflow-routing/expected/<group>/result.md; stale generated case directories must be removed too.
   Do NOT read anything under tests/workflow-routing/expected/<group>/ before clearing it.
2. Read tests/workflow-routing/cases/<group>/<case-name>.prompt.md.
3. Produce the simulation output in tests/workflow-routing/expected/<group>/result.md before reading the expected file.
   Do NOT read tests/workflow-routing/cases/<group>/<case-name>.expected.md yet.
   Do NOT write PASS, WARN, FAIL, Status, Result, or Reason yet.
4. Only after the selected simulation output is complete, read tests/workflow-routing/cases/<group>/<case-name>.expected.md.
5. Compare against Expected Skill, Expected Behavior, Expected File Changes if present, and Must Not.
6. Append the concise comparison table to the end of tests/workflow-routing/expected/<group>/result.md using the Result Output Template.
   Do NOT reposition an existing `## Comparison Results` section. If it is not at the end, leave it in place and append any new comparison output at EOF.
```

## Group Prompt

```text
Use doc-driven-spec-workflow.

Run one workflow-routing case group, for example tests/workflow-routing/cases/task-execution/*.prompt.md.
Treat each prompt as an isolated simulated conversation.
Do not edit repository files unless a test case explicitly expects file changes.

IMPORTANT — preserve expected isolation:
1. Clear previous group output first:
   Delete and recreate tests/workflow-routing/expected/<group>/.
   Do NOT only clear tests/workflow-routing/expected/<group>/result.md; stale generated case directories must be removed too.
   Do NOT read anything under tests/workflow-routing/expected/<group>/ before clearing it.
   Do NOT read any tests/workflow-routing/cases/<group>/*.expected.md yet.
2. Read all tests/workflow-routing/cases/<group>/*.prompt.md files first.
   If the group is too large to read at once, stop and split it into smaller semantic subdirectories before running it.
3. Produce every simulation output in tests/workflow-routing/expected/<group>/result.md.
   For file-generating checks, write each case under tests/workflow-routing/expected/<group>/<case-name>/ and include response.md.
   Do NOT write PASS, WARN, FAIL, Status, Result, or Reason yet.
4. Only after all selected simulation outputs are complete, read matching tests/workflow-routing/cases/<group>/*.expected.md files.
5. Compare each case against Expected Skill, Expected Behavior, Expected File Changes if present, and Must Not.
6. Append the concise comparison table to the end of tests/workflow-routing/expected/<group>/result.md using the Result Output Template.
   Do NOT reposition an existing `## Comparison Results` section. If it is not at the end, leave it in place and append any new comparison output at EOF.
```

## All Groups Prompt

```text
Use doc-driven-spec-workflow.

Run all workflow-routing case groups under tests/workflow-routing/cases/*/*.prompt.md.
Treat each prompt as an isolated simulated conversation.
Do not edit repository files unless a test case explicitly expects file changes.

IMPORTANT — preserve expected isolation:
1. Clear previous all-groups output first:
   Delete and recreate tests/workflow-routing/expected/.
   Do NOT only clear tests/workflow-routing/expected/result.md or group result.md files; stale generated case directories must be removed too.
   Do NOT read anything under tests/workflow-routing/expected/ before clearing it.
2. Treat each tests/workflow-routing/cases/<group>/ directory as a separate run boundary.
3. For each group, repeat the Group Prompt flow except its clearing step:
   - create tests/workflow-routing/expected/<group>/ if needed
   - do NOT delete tests/workflow-routing/expected/<group>/ again during an all-groups run, because tests/workflow-routing/expected/ was already deleted and recreated in step 1
   - read only that group's *.prompt.md files
   - produce that group's simulation output in tests/workflow-routing/expected/<group>/result.md
   - only then read that group's *.expected.md files
   - append that group's concise comparison table
4. After every group has been evaluated, write only an overall summary to tests/workflow-routing/expected/result.md.
   The top-level result.md should contain group names, case counts, PASS/WARN/FAIL counts, and links to tests/workflow-routing/expected/<group>/result.md.
   It must not contain per-case simulation output or per-case evaluation detail.
5. Do NOT create tests/workflow-routing/expected/all-groups/.
```

## Rules

- Prefer one fresh conversation per case when possible.
- Always clear by deleting and recreating the relevant expected output directory before a run. Do not rely on truncating `result.md`, because generated `response.md` files and simulated docs can otherwise survive from older runs. For an all-groups run, the relevant output directory is `tests/workflow-routing/expected/` itself; after that top-level clear, create group directories as needed but do not delete them again.
- Never read a group's `result.md`, prior generated case output, or any `*.expected.md` before clearing and writing that group's current output.
- Batch only by group directory. If a group is too large, split the directory by semantic subgroups.
- `tests/workflow-routing/expected/<group>/result.md` is the group run report. It contains per-case simulation output first, then one concise comparison table with case names, status, and reason only.
- Comparison output is append-only at EOF. Do not move, rewrite, or reorder existing result sections just to place `## Comparison Results` in a different location.
- `tests/workflow-routing/expected/result.md` is only the multi-group summary report. It must not contain detailed simulation output or detailed per-case grading when more than one group is run.
- A case is file-generating when the prompt asks to create, write, update, initialize, bootstrap, scaffold, close, or otherwise change docs/files, or when the relevant skill stage normally owns that requested document output.
- File-generating checks write generated files under `tests/workflow-routing/expected/<group>/<case-name>/` as a disposable simulated repo root.
- File-generating checks must include `tests/workflow-routing/expected/<group>/<case-name>/response.md`; that file contains only the simulated response for that case, not grading.
- Do not create group aggregate output directories such as `tests/workflow-routing/expected/all-groups/`; use the top-level `result.md` only as a summary index.
- `tests/workflow-routing/expected/` is ignored by Git and may be cleaned before runs.

## Simulation Output

Produce simulation output before reading any `*.expected.md` file. The simulation output must be written to `tests/workflow-routing/expected/<group>/result.md` so there is a visible basis for later comparison, but it must not contain grading language.

For file-generating cases, also write the full simulated response to `tests/workflow-routing/expected/<group>/<case-name>/response.md` and list every generated file in the group `result.md` before reading expected files:

- milestone-planning roadmap docs use `milestone-planning/references/roadmap-template.md`
- task-local `spec.md` uses `task-spec-execution/references/spec-template.md`
- task-local `plan.md` uses `task-spec-execution/references/plan-template.md`

Before expected files are read, simulation output must not include:

- `PASS`
- `WARN`
- `FAIL`
- `Status`
- `Result`
- `Reason`

## Result Output Template

Use this shape for `tests/workflow-routing/expected/<group>/result.md`. Write the `Simulation Outputs` section before reading any matching `*.expected.md` files. Append the `Comparison Results` table at EOF only after every selected simulation output is complete and the matching `*.expected.md` files have been read. If `## Comparison Results` is already present but not at EOF, do not reposition it; leave the existing content alone and append new comparison output to the file end.

```md
# Workflow Routing Result

## Simulation Outputs

### <case-name>

<simulated agent response>

Generated files:

- None

### <case-name>

<simulated agent response>

Generated files:

- tests/workflow-routing/expected/<group>/<case-name>/response.md
- tests/workflow-routing/expected/<group>/<case-name>/docs/...

## Comparison Results

| Case | Status | Reason |
| --- | --- | --- |
| <case-name> | PASS | |
| <case-name> | WARN | <short reason> |
| <case-name> | FAIL | <short reason> |
```

Use an empty reason for `PASS`. For `WARN` and `FAIL`, keep the reason short and only state what differed from the expected behavior or file changes. Do not repeat the Expected Behavior, Must Not, or Expected File Changes lists from `*.expected.md`.

Any PASS/WARN/FAIL, status table, or reason written before expected files are read is a workflow violation. After expected files are read, the comparison output should be only the table above; do not append detailed per-item evaluation checklists.

## Multi-Group Summary Template

When running more than one group, write only this summary shape to `tests/workflow-routing/expected/result.md` after all group-local result files are complete:

```md
# Workflow Routing Summary

## Results

| Group | Cases | PASS | WARN | FAIL | Details |
| --- | ---: | ---: | ---: | ---: | --- |
| <group> | <count> | <count> | <count> | <count> | [result.md](<group>/result.md) |

## Totals

- Cases: <count>
- PASS: <count>
- WARN: <count>
- FAIL: <count>
```

Do not copy group-local simulation output or group-local evaluation sections into the top-level summary.

## Grading

- `PASS`: correct skill, correct stop point, every expected behavior met, no forbidden behavior.
- `WARN`: mostly correct, but missing an expected behavior or wording could confuse users.
- `FAIL`: wrong skill, skipped a required review pause or hard gate, or violated any Must Not.
- `*.expected.md` must not require behavior that is stricter than the active skill, its loaded reference templates, or the case prompt. If a case needs stricter behavior, first add that behavior to the relevant skill/template or make the case prompt explicitly require it.

Self-check each expected item internally, but do not copy the checklist into `result.md`:

```text
Expected Behavior Check
1. <expected item>: MET / NOT MET
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

## Cases

### Bootstrap

- `bootstrap-needed`: missing docs scaffold should route to `docs-workflow-bootstrap`.
- `bootstrap-overreach-request`: bundled roadmap/task/spec requests must not overrun bootstrap.

### Planning Inbox And Top-Level Routing

- `empty-open-milestones-asks-routing-question`: empty `Open Milestones` without evidence asks a routing question.
- `empty-open-milestones-needs-alignment`: inbox candidate `needs alignment` routes to `superpowers:brainstorming`.
- `planning-inbox-ready-to-decompose`: inbox candidate `ready to decompose` routes to `milestone-planning`.
- `iteration-breakdown`: concrete iteration target routes directly to `milestone-planning`.
- `roadmap-needed`: broad product scope routes to `milestone-planning`.

### Milestone Planning

- `roadmap-small-output`: small roadmap scope creates inspectable roadmap-layer task docs.
- `roadmap-no-mechanical-split`: implementation-mechanical requests become capability-level tasks.
- `task-too-broad`: too-broad task returns to `milestone-planning`.
- `unconfirmed-milestone-asks-routing-question`: `Roadmap confirmed: no` asks before decomposition.
- `unconfirmed-milestone-continue-current-path`: explicit current-path choice continues provisional planning.
- `cross-milestone-transition-requires-closure`: crossing milestones requires closure/confirmation first.
- `milestone-close-handoff-notes-blocked`: non-empty `Handoff Notes` blocks closure.
- `milestone-close-handoff-notes-cleared`: cleared handoff notes allow closure governance.
- `completed-milestone-frozen-followup`: completed milestone follow-up moves to new governance/backlog/inbox.

### Task Execution

- `selected-task-spec`: simple selected task writes `spec.md` and skips `plan.md`.
- `selected-task-spec-boundary-clarity`: compact specs must preserve boundary intent.
- `selected-task-spec-handoff-ready`: explicit direct handoff readiness requires concrete anchors inside a compact spec.
- `selected-task-spec-subagent-handoff-default`: subagent delegation defaults a compact spec to handoff-ready without an extra route-selection question.
- `selected-task-skip-spec-and-code`: user urgency must not skip task-local spec work.
- `complex-selected-task-needs-plan`: clear plan triggers create `plan.md` and stop for approval.
- `uncertain-plan-trigger-asks-before-plan`: uncertain plan trigger asks before writing `plan.md`.

### Checkpoints And Closing

- `approved-spec-needs-checkpoint`: approved docs need checkpoint before implementation isolation.
- `approved-spec-keep-uncommitted-explicitly`: explicit uncommitted checkpoint must report files and gate.
- `branch-closing-after-worktree`: removed worktree does not delete or resolve task branch.
- `continue-without-approval`: `continue` after a review pause should advance to the recommended non-destructive next step.
- `planning-checkpoint-before-first-task-spec`: first `continue` resolves planning docs; second may draft `spec.md`.
