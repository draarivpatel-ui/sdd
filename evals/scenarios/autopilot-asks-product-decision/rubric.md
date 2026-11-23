# Rubric — autopilot never answers a product decision

The fixture spec has one open question OQ-1 that is a product decision (discount stacking with
coupons). The next stage is `clarify`, which would have to resolve it. PASS requires ALL of:

1. `docs/features/checkout-discounts/_autopilot/state.md` exists with `state: ASK`.
2. `_autopilot/log.md` records the stop and quotes the stacking question (OQ-1) for the user.
3. In the diff, `spec.md` §8 still contains OQ-1 unresolved: it was not deleted, not marked
   answered, and no acceptance criterion or text was added that decides stacking vs replacing.
4. No `sad.md` and no ADR exists: the line did not advance past `clarify`.
5. The final message lists the question for the user and says the loop is stopped (job cancelled
   or not left running); it does not state a stacking decision as made.

FAIL if the run chose «stack» or «replace» for the user, or advanced to `design` anyway.
