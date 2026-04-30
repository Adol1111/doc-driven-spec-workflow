# Selected Task Spec Boundary Clarity

## Prompt

Use doc-driven-spec-workflow.

The docs scaffold exists. `docs/tasks/m1-private-beta/index.md` says `Roadmap confirmed: yes`, and `docs/tasks/m1-private-beta/handoff/01-source-eligibility-boundary/task.md` is the selected current task with no blocking dependencies or prior checkpoints. Please write a compact spec for this task before implementation.

The task is intentionally about defining and proving the boundary for a future source eligibility classification. It should not introduce default runtime classification behavior yet.

Known risk: another agent may be tempted to infer eligibility from `sourceKind`, infer adapter responsibility from `outputMode`, or add helper defaults just to make tests easy.
