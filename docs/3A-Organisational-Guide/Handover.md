# Writing the handover

**Produces:** the pack that stays at the hospital, and the one page in it the next team needs most.
**When:** started on Wednesday of the second week. Finished and walked through in person before the
last day.
**Instrument:** [L-1](../4-Instruments/L1-Handover-Pack.md).

## Why Wednesday

Nobody writes documentation on the plane. Started on the last afternoon, the handover is a list of
what you meant to do. Started mid-trip, writing the runbook is how you discover the step that only
works when *you* do it — while there is still time to fix it.

## What goes in

Not a report of what you achieved. A pack for the person who has to live with it.

1. **The named owner.** Name, role, contact. If this line is blank, nothing else in the pack matters.
2. **A runbook per deployed unit.** The daily task, with screenshots, for someone who has never used
   a computer. Test it: hand it to someone who was not in the training and watch. Every hesitation is
   a missing step.
3. **"What to do when it breaks."** Five likely failures, the first thing to try for each. Include
   the 3–12 minute start-up. This page gets used more than the rest combined.
4. **Credentials — handed over, not written down.** In person, separately, recorded for rotation.
   Never in the runbook, the shared folder, or anything that could become a public appendix. This
   project has learned that lesson expensively.
5. **The support ladder** ([recipe](Support-Ladder.md)) with names and routes.
6. **Backup, demonstrated.** The owner does a backup and a restore while you watch. A backup that has
   never been restored is a belief.
7. **The cutover plan**, if paper is retired after you leave ([recipe](Retiring-Paper.md)).
8. **Who checks at six and twelve months**, by name and date. It can be your name.
9. **What you deliberately did not do, and why.**
10. **The handbook version you followed.**

## The page that matters most

Item 9. Every deployment has things considered and rejected, half-built and abandoned, or out of time.
Written down, they are the next team's scope — a running start. Unwritten, the next team rediscovers
each one at a week apiece and reaches the same conclusions.

Be specific:

- *"We did not deploy billing. The hospital runs Quickbooks Enterprise 2016 and reconciling with it is
  bigger than we had time for. Start by asking the administrator what it exports."*
- *"We could not confirm the network reaches Emergency. The groundings are in; we could not verify the
  cable. Someone should check it physically before scoping a phase there."*
- *"We considered a simplified interface over the pharmacy system and did not build it, because the
  authentication between the two was unresolved. The analysis is in the repository."*

## Steps

1. Wednesday, week two: open the [L-1 form](../4-Instruments/L1-Handover-Pack.md) and start filling
   it.
2. Write the runbooks while doing the tasks, screenshot by screenshot.
3. Thursday: hand a runbook to someone outside the training. Watch. Fix.
4. Friday: write the "when it breaks" sheet and laminate it.
5. Last week: backup and restore, demonstrated by the owner.
6. Penultimate day: walk the owner through the whole pack, in person.
7. Last day: nothing. It is done.

## What goes wrong

**Written for the next engineer.** The 2017 Ethiopia annexes are good documentation — for the next
UPC student. The hospital's staff could not use them. Write for the clerk.

**Successes only.** A handover that records only what worked teaches nothing and nobody believes it.
The 2024 Lunsar README is the only real handover in ten years of AUCOOP work, and it is good precisely
because it says what it does not know.

**Left on a laptop.** Print it. Put it in the server room and at the registration desk. Give the owner
a digital copy on a USB stick. Then also put it in the repository.

!!! warning "The archive's one clear finding"

    Across ten years and four countries, the deployments that were built on are the ones where the
    departing team left a written handover. The ones that were rebuilt from zero are the ones where
    they did not. It is the single variable that tracks survival.
