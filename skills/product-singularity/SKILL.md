---
name: product-singularity
description: Use when defining a product's north star, prioritizing product work, or judging if a change moves it toward its ideal.
---

# Product singularity

A product's problem never fully ends, so work drifts toward whatever is easiest to ship. Picture the product as a ship in a multi-dimensional ocean. Its **singularity** is the problem solved in its purest form, written as measurable dimensions. Every change moves the ship closer on some dimension or adds drift.

Use this when choosing what to build or what a change is for. Skip it when nothing is being chosen: typo fixes, renames, dependency bumps, fully specified tasks.

## Map the ocean

Before judging work, write the map, or reuse an existing one.

1. **Singularity.** 3–6 user outcomes, each with a unit and an ideal value, such as `alert delay <60 s`. Never output counts like features shipped.
2. **Floors.** Values that must never break, such as `0 account-takeover paths`.
3. **Ship.** Today's value per dimension, with its source (dashboard, log, test, user report), or `unknown`. Never invent a number; label estimates and what they rest on.
4. **Active constraint.** The one dimension whose gap costs users most now, with the evidence.

Ask once, only for numbers that would change the decision. If no one can answer, decide on labeled assumptions and say what result would flip the call.

```text
Product:     Clinic online booking
Singularity: booking ≤2 min | no-shows 0% | double-bookings 0
Ship:        booking time unknown (no analytics) | no-shows 18% (front-desk log)
             | double-bookings 0 in 90 days (calendar audit)
Constraint:  no-shows, the largest known gap. Revisit once booking time is measured.
Ask:         "Can I log one event at booking start and one at confirm?"
```

## Steer each proposal

Before building or recommending a proposal, yours or the user's, write its vector:

- **Toward:** the dimension that moves, from what value to what expected value (or `unknown`), and the signal that will show it.
- **Drift:** the dimension that gets worse, including steps, latency, complexity, and maintenance.
- **Local maximum:** does it polish a workaround instead of removing the need for it? Name the removing move.

Then decide, first match wins:

1. **Hull breach → fix now.** An outage, data loss, security hole, or broken core flow breaks a floor; the fix needs no forward move. Judge anything bundled with it separately.
2. **Toward, no dimension worse → build.** Among options, prefer the one that moves the active constraint.
3. **Toward, another dimension worse → show both numbers.** If the loser is the active constraint or crosses a floor, recommend against it or a variant that avoids the loss. Otherwise let the user choose.
4. **Enabler → build with its follow-up.** Moves nothing alone but unblocks a named move, such as instrumentation. Name the dimension and the follow-up.
5. **Moves nothing → defer.** Name what it misses and offer the better move. Do not refuse.
6. **User override → build as asked.** Note the drift in one line, then build the full scope. Do not re-argue, shrink it, or count it as progress.

After a change ships, check its signal and update the ship, or mark the move `unverified`. If the signal did not move, it was not progress.

```text
Product:     Rental-alert bot (ship → singularity)
Map:         missed 5% → 0 | delay 4 min → <60 s | noise 30% → 0 | setup 3 → 1 steps
Proposal:    Dark-mode dashboard themes
Vector:      Toward none; drift: theme code to maintain → Defer.
Proposal:    "Hide duplicate" button on each alert
Vector:      Local maximum: duplicates still arrive.
Better move: Drop duplicates at ingest; count them in last week's log first.
```

## Move the target (only on discovery)

Sailing closer reveals parameters you could not see from shore. Move the singularity only when you can write both:

1. **What changed:** a dimension added or removed, or an ideal value revised.
2. **What revealed it:** user behavior, a failure, a measurement, or a hard limit (law, third-party API).

Test: would the evidence exist if the current work had never been built? If the only evidence is that the work falls short, it is not discovery. Keep the target and report the gap.

On discovery, tell the user in one line, update the written map, and re-check decisions that relied on the old target. Never move it silently.

```text
Product:  Meal-kit delivery (on-time 100% | spoiled 0 | cook ≤30 min)
Evidence: 38% of cancellations cite packaging waste (exit survey)
Move:     Add dimension: non-recyclable packaging 0 g per box
Re-check: "Bigger ice packs" now drifts on the new dimension
Trap:     Cook ≤30 → ≤45 min "because new recipes take 40" is our own
          shortfall, not discovery. Keep ≤30; report the gap.
```
