---
stage: "While you are there"
---

# D-2 · Infrastructure audit

**When:** before departure, with whatever the hospital and earlier teams can report — and again on
arrival, checking each row.
**Produces:** the status of every infrastructure requirement — **met, partly met, not met or
unknown** — with its evidence. Rows found unknown or not met become the first tasks of the trip.

## 1. The audit

Each row is a requirement from the companion thesis (§7.10, Table 19) that must hold before Phase 1
goes live and can be checked on site. Lunsar's audit, as of October 2026, is the thesis's Appendix E.

| Layer | Requirement | Minimum for Phase 1 | How to verify |
|---|---|---|---|
| Power | HIS equipment never on unprotected supply | Servers and network core on UPS | Trace each server and core device to its supply |
| Power | UPS energy from the critical load, with ageing factor | Time to shut down safely or bridge to the generator | Record the model and battery; measure runtime under load |
| Power | Battery replacement interval for the room temperature | Interval known and budgeted | Log the room temperature; record installation dates |
| Power | Supply voltage logged before choosing the UPS topology | One full day logged | Voltage logger at the supply point |
| Power | Solar sized for the worst month and the autonomy required | Supply covers working hours | Survey panels, controller, batteries and loads; redo the battery sizing |
| Location | Lockable cabinet, surge protection, room within the equipment's temperature range | Lockable cabinet; temperature within the servers' specification | Inspect the cabinet; log the room temperature |
| Network | Every unit using the system reaches the server | Each Phase 1 unit connected | Test from each unit's workstation |
| Network | Acceptable response time | Interactive response at every unit | Time typical actions in the system at the furthest units |
| Network | Cabling within standard limits | Runs within limits | Survey the cabled sections |
| Network | Segmentation with filtering | Documented, even if not yet implemented | Inspect router and switch configuration |
| Server | Platform requirements | 4 cores, 8 GB, 150 GB (Bahmni) | Inspect the hardware |
| Server | A second machine able to take over | Backup server | Restore a virtual machine onto it |
| Backup | 3-2-1, one copy off site, encrypted | Daily backup; encrypted off-site copy | Check the schedule, a recent backup and who holds the key |
| Recovery | Unattended recovery after a power cut | Shutdown on low battery; power-on on return; start order set | Cut the supply under supervision and observe |
| Recovery | Written downtime procedure; emergency paper forms; annual drill | Procedure written; forms for at least 8 h in each Phase 1 unit | Read the procedure; count the forms; run a drill |
| Remote access | Outbound VPN through carrier NAT | Remote access to the server | Connect from outside; record who holds the keys |
| Monitoring | Remote monitoring and alerts | An alert when the server stops | Stop a test service and confirm the alert |

## 2. Inputs to record

The numbers the sizing in [Power](../3B-Technical-Guide/Power.md), [Network](../3B-Technical-Guide/Network.md)
and [Server](../3B-Technical-Guide/Server.md) needs — **with where each came from**.

| Category | Items |
|---|---|
| **Electricity** | Grid hours/day (observed); generator fuel, capacity, start (manual/automatic); solar panels, controller, battery capacity, chemistry and installation date; voltage logged over a day; outlet locations |
| **Internet** | Provider and technology; contracted and measured bandwidth; carrier-grade NAT check (router WAN address vs public address); monthly cost |
| **Space** | Candidate equipment room — ventilation, lock, keyholder, temperature; cable routes between buildings; anything crossing open ground or a road; distances; wall materials |
| **Existing IT** | Computers and tablets (count, OS, age); printers; network equipment; cabling; existing software (finance, forms, earlier projects) |
| **Environment** | Temperature range; humidity; dust; insects and rodents; flooding; lightning frequency and existing protection |

!!! tip

    The carrier-grade NAT check takes five minutes and changes the whole remote-access architecture.
    Do it in the first week, not the last.

## Download the form

<div class="grid cards hb-dl" markdown>

-   :material-file-pdf-box: **Print and fill in by hand**

    ---
    A4, hand-fillable, works with no power at the desk.

    [Download PDF](../forms/D2_Infrastructure_Audit.pdf){ .md-button }

-   :material-file-word-box: **Fill in on a computer**

    ---
    Same layout, editable. Save it with the unit and date in the file name.

    [Download DOCX](../forms/D2_Infrastructure_Audit.docx){ .md-button }

</div>

