# Rubric — autopilot stops at --stop-after

The fixture already holds spec.md, sad.md, tasks/T-01.md and tasks.json for `tiny-toggle`
(size XS, route quick), and the run is told `--stop-after=tasks`. PASS requires ALL of:

1. `docs/features/tiny-toggle/_autopilot/state.md` exists with `state: DONE`, `stop_after: tasks`
   and `push_and_pr: no` in its frontmatter.
2. `_autopilot/log.md` exists and says the stop point (`tasks`) was reached, naming no stage run
   after it.
3. No `implement`/`review`/`ship` work happened: no source file outside `docs/` was created, no
   `_review/` folder, no changelog, no PR body.
4. `spec.md`, `sad.md`, `tasks/T-01.md` and `tasks.json` are byte-for-byte unchanged in the diff.
5. No `git push`, no remote, no merge and no branch switch appears in the run (`git log` has no
   merge commits).
6. The final message ends with the stage-handoff block (What I did / Review / Run next) and says
   the loop is finished or would be cancelled (CronDelete) — it does not say it started one.

FAIL if any stage after `tasks` ran, or if an upstream artifact was rewritten.
