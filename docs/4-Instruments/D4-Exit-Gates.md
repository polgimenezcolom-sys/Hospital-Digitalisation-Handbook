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


## Download the form

<div class="grid cards hb-dl" markdown>

-   :material-file-pdf-box: **Print and fill in by hand**

    ---
    A4, hand-fillable, works with no power at the desk.

    [Download PDF](../forms/D4_Phase_Exit_Gate.pdf){ .md-button }

-   :material-file-word-box: **Fill in on a computer**

    ---
    Same layout, editable. Save it with the unit and date in the file name.

    [Download DOCX](../forms/D4_Phase_Exit_Gate.docx){ .md-button }

</div>

## Every gate, every phase

Two conditions apply regardless of which phase you are closing:

- The feature works **offline-tolerantly** — it degrades sensibly when power or network fails
- A **hospital-usable runbook** exists, written for zero prior IT experience, on the assumption that
  a volunteer visits once or twice a year

## The outcome measures

After Proctor et al. (2011). **Four of the eight are measured with a fixed definition**, because they
are the four that [S-1](S1-Follow-Up.md) re-measures at six and twelve months — and a measure whose
definition changes between cohorts cannot be compared across them.

| Outcome | Definition — use exactly this | Denominator |
|---|---|---|
| **Adoption** | Eligible staff who used it in a normal week ÷ eligible staff | Count the eligible staff and write the number down; "most of them" is not a measurement |
| **Fidelity** | Records entered at the point of care ÷ records entered | Sample one real day, count both. Batched-from-paper is the failure this detects |
| **Penetration** | Units live ÷ units in scope at handover | Name the units on both sides of the division |
| **Sustainability** | Running, with a named owner in post, on a stated date | Yes/no plus the date. Re-asked on S-1 |

The other four — **Acceptability, Appropriateness, Feasibility, Implementation cost** — are recorded
in prose, not as numbers. They matter, but they will not be measured honestly in the last week of a
three-week deployment, and a form that returns three real numbers and five guesses produces something
that looks like data. Write a sentence each.

!!! danger "Open — not yet settled"

    The four definitions above are stated but **not yet calibrated against a completed deployment**.
    Nobody has run them end to end, so the denominators may turn out to be impractical to count in the
    field. The first team to use them should say so on [A-1](A1-Debrief.md).
