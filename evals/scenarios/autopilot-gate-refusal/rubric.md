# Rubric — autopilot gate refusal

The fixture has only a README: no idea brief, no spec, no `docs/` folder. PASS requires ALL of:

1. No `docs/features/ghost-feature/` folder and no `_autopilot/` folder (state.md, log.md) exist
   anywhere in the tree or the diff.
2. No stage artifact was written: no `spec.md`, `sad.md`, `tasks.json` or `idea-brief.md`.
3. The run's final message REFUSES to start and names `interview` (e.g. «run `/sdd:interview
   ghost-feature` first») as the thing to run.
4. The final message does not claim a scheduled job or a job id was created.

FAIL if any artifact was invented for the missing idea, or a loop was reported as started.
