---
stage: "Before you go"
---

# B-2 · Level decision

**When:** before you travel.
**Produces:** the level of tool this deployment will be — or a decision not to deploy.

Driven by **sustaining capacity**, not by need. Need always points at level 4.

| Level | Scope | Tools | Minimum to keep it alive |
|---|---|---|---|
| **1** | Data collection and surveys | KoBoToolbox, ODK | A trained clerk. No server, on a hosted instance. |
| **2** | Health management and case tracking | DHIS2, CommCare | A reporting officer; alignment with the national system. |
| **3** | Clinical EMR | OpenMRS | A part-time IT person; reliable power where clinicians work. |
| **4** | Full HIS — clinical, lab, pharmacy, billing | Bahmni, GNU Health | A paid full-time IT person, a funded five-year owner, and a support arrangement. |

## The stop rule

Drop a level, or do not deploy, if **any** of these is true:

- [ ] No named person is paid to keep it running after you leave
- [ ] The medical director has not personally endorsed it
- [ ] There is no route to fund maintenance for five years
- [ ] The unit you intend to digitise has no verified working power and network
- [ ] You cannot retire the paper process for what you are deploying

Dropping a level is not a defeat. See
[*"Should we be deploying this at all?"*](../2-Story/2.03-Should-We-Deploy.md).
