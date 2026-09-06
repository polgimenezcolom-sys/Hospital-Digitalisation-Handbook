# Case study template

A [Real Deployments](../5-Real-Deployments/index.md) entry is a write-up of a deployment that
actually happened. The goal is to give a future team enough to understand your decisions, learn from
what worked and what did not, and reuse the parts that fit their context.

*Adapted from AUCOOP's
[Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/contributing/case-study/),
so that the two handbooks stay consistent.*

## How to start

1. Copy an existing case study as your template.
2. Create a folder under `docs/5-Real-Deployments/` — for example `5.3-YourSite/`.
3. Put your `index.md` and an `images/` subfolder inside.
4. Add an entry under **Real Deployments** in `mkdocs.yml`.
5. Open a pull request.

## What to cover

**Context.** Where is the hospital, and how big? Service volumes — outpatient visits per day,
inpatient census, deliveries per month. Staffing. What existed before: paper only, a partial system,
a previous attempt? Who asked for this?

**Design.** What level did you deploy at, and what did [B-1](../4-Instruments/B1-Readiness.md) score?
Which platform, and why? Where did you depart from this handbook's defaults, and what motivated the
change?

**Deployment.** What was the on-the-ground experience? What worked smoothly? What broke, and how did
you recover? Which phase did you start with, and did you retire any paper process? What would you do
differently?

**Current state.** Is it still running? Who operates it now? What do the outcome measures in
[D-4](../4-Instruments/D4-Exit-Gates.md) say at six and twelve months? If it is not running, say so
plainly and say what you think happened.

## Health-specific things to include

- **The forms.** Photographs of the paper records the hospital uses. These are the single most
  reusable artefact a case study can carry.
- **The identifier.** How patients are identified, and whether that survived digitalisation.
- **What was retired.** Which paper process, if any, actually stopped. And if none did, say so.

## Images

- An `images/` subfolder beside your `index.md`.
- `.webp` where possible.
- Before/after diagrams of the site or the data flow are especially valuable.
- **Faces and patient data must not appear.** Photograph blank forms, or completed forms with
  identifying details covered.

## Honesty over polish

!!! warning

    A case study that only records successes is close to useless, and everyone can tell.

    The next team to work in conditions like yours will hit the same problems. Your write-up is the
    only thing that lets them avoid the week you lost — and the most-read section of any case study
    here will be the one headed *what we would do differently*.
