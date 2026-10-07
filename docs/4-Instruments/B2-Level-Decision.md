---
stage: "Before you go"
---

# B-2 · Level decision

**When:** before you travel.
**Produces:** the level of tool this deployment will be — or a decision not to deploy.

Driven by **what the hospital can sustain**, not by need. Need always points at level 4.

| Level | Scope | Tools | When |
|---|---|---|---|
| **1** | Data collection and surveys | KoBoToolbox, ODK | None of the four conditions below holds |
| **2** | Aggregate reporting and case tracking | DHIS2, CommCare | None holds; a reporting officer and alignment with the national system |
| **3** | Clinical record | OpenMRS | Conditions 1 and 2 hold |
| **4** | Full HIS — clinical, lab, pharmacy, billing | Bahmni, GNU Health | All four hold — and then phase by phase |

The four conditions are those of the implementation matrix in the companion thesis (§6.3.1).


## Download the form

<div class="grid cards hb-dl" markdown>

-   :material-file-pdf-box: **Print and fill in by hand**

    ---
    A4, hand-fillable, works with no power at the desk.

    [Download PDF](../forms/B2_Level_Decision.pdf){ .md-button }

-   :material-file-word-box: **Fill in on a computer**

    ---
    Same layout, editable. Save it with the unit and date in the file name.

    [Download DOCX](../forms/B2_Level_Decision.docx){ .md-button }

</div>

## The four conditions

Tick each one that **holds**:

- [ ] **1.** A person employed by the hospital is responsible for the system and can be reached after
      you leave
- [ ] **2.** Protected power and a working network at the point of use, verified in each unit before it
      goes live
- [ ] **3.** A management mandate: a named owner, and agreement to close the paper registers when the
      exit criteria are met
- [ ] **4.** A paper process that can actually be retired, including the statutory returns that depend
      on it

**The stop rule:** if a condition needed for the level you planned does not hold, drop a level or do
not deploy. Separately, agree **who pays the running costs** — connectivity, spares, batteries,
support — before anything is bought.

Dropping a level is not a defeat. See
[*"Should we be deploying this at all?"*](../2-Story/2.03-Should-We-Deploy.md).
