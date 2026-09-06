---
stage: "While you are there"
---

# D-4 · Phase exit gates

**When:** at the end of each phase.
**Produces:** a defensible answer to "is this done?"

A phase is not finished because the feature works.

| Phase | Contains | Exit gate |
|---|---|---|
| **1** | Registration and basic EMR | The folder ID is the primary searchable identifier · a runbook exists · one unit has retired its paper register |
| **2** | Laboratory and pharmacy | A lab order completes end to end · dispensing decrements stock · the pharmacist can work unaided |
| **3** | Billing and administration | Reconciles with the incumbent finance system · the finance director signs off |
| **4** | Reporting and epidemiology | A member of hospital staff produces the statutory monthly return from the system, unaided, and submits it |

## Every gate, every phase

Two conditions apply regardless of which phase you are closing:

- The feature works **offline-tolerantly** — it degrades sensibly when power or network fails
- A **hospital-usable runbook** exists, written for zero prior IT experience, on the assumption that
  a volunteer visits once or twice a year

!!! danger "Open — not yet settled"

    These gates are engineering conditions. They need the measurable outcomes below attached to each
    one, so that a later team can test whether a gate was genuinely passed rather than declared.

    | Outcome | The question | How you would measure it here |
    |---|---|---|
    | Acceptability | Do staff find it agreeable? | Short structured question at handover |
    | Adoption | Did they take it up? | Eligible staff using it weekly |
    | Appropriateness | Does it fit this setting? | Workflow steps matched vs. worked around |
    | Feasibility | Can it be done here? | Phases completed vs. planned |
    | Fidelity | Used as intended? | Entered at point of care vs. batched from paper |
    | Implementation cost | What did it take? | Hardware, travel, staff time, recurrent cost |
    | Penetration | How far did it spread? | Units live vs. units in scope |
    | Sustainability | Still running? | Checked remotely at 6 and 12 months |
