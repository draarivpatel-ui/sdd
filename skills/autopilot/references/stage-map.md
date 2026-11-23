# autopilot: stage map and state files

> Reference for [`../SKILL.md`](../SKILL.md). One level deep, no nested references.

## Which stage is next

Walk the list in order; the first stage whose output is missing or older than its input is next.
`route` (from `.route`) decides which optional stages are skipped, per the Routes table in
[`../../_shared/size-matrix.md`](../../_shared/size-matrix.md): `quick` auto-skips when the N/A
condition holds, `standard` skips when it holds, `full` skips nothing.

| # | Stage | Done when this exists | Optional? |
|---|-------|-----------------------|-----------|
| 0 | `interview` | `docs/idea-brief.md` | yes, only when starting from a raw idea |
| 0 | `survey` | `docs/architecture-map.md` | once per repo |
| 0 | `roadmap` | `docs/roadmap.md` | yes |
| 1 | `specify` | `docs/features/<slug>/spec.md` | no |
| 2 | `clarify` | spec has zero open §8 questions | skippable |
| 3 | `ux-flows` | `ux-flows.md` | UI features only |
| 4 | `design` | `sad.md` | no |
| 5 | `sequences` | `sad.md §6` filled | skippable |
| 6 | `data-model` | `data-model.md` | skippable |
| 7 | `api` | `contracts/` | skippable |
| 8 | `screens` | `screens.md` | UI features only |
| 9 | `tasks` | `tasks/` and `tasks.json` | no |
| 10 | `plan-tests` | `test-plan.md` (M and up) or inline test plan | skippable on XS/S |
| 11 | `implement` | every task in `tasks.json` done, gate green | no |
| 12 | `review` | a `PASS` record in `_review/` | no |
| 13 | `ship` | changelog and PR body written | no |

Stale means: an input file has a newer commit than the stage's output. Re-run that stage and all
after it.

## `_autopilot/state.md`

```md
---
slug: checkout-discounts
job: <cron job id>
interval: 10m
stop_after: ship          # tasks | implement | ship
push_and_pr: no           # standing instruction, never widened
depth: easy               # easy | medium | hard
state: RUN                # RUN | WAIT | STUCK | ASK | DONE
running: ""               # "<stage> since <iso time>" while a subagent works
laps_review: 0            # review -> implement bounces, max 3
---
```

## `_autopilot/log.md`

One line per finished stage, newest last:

```md
- 2026-11-23T10:12 specify: wrote spec.md (size M, route standard); commit a1b2c3d;
  decided: auth method = existing session cookie (recommended, overrule in review)
```

A stop appends its reason and the exact question for the user:

```md
- 2026-11-23T11:40 ASK at design: should discounts stack with coupons? (product decision)
```

Both files are committed with the stage that changed them, never in a separate "autopilot" commit
per tick.
