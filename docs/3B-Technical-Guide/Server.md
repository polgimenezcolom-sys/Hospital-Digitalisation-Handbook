# Server, backup and recovery

**Produces:** a server that meets the platform's published requirements, in a locked cabinet in a room
kept within its temperature range, with a backup that has been **restored** in front of the owner, and
a hospital that knows what to do when the power goes.
**Instrument:** [D-2](../4-Instruments/D2-Infrastructure-Audit.md), rows *Location*, *Server*,
*Backup* and *Recovery*. Reasoning and sources: thesis §7.2, §7.5–7.7.

## Size it from the platform, not from a table

| Platform | Processor | Memory | Disk |
|---|---|---|---|
| **Bahmni** | 4 cores (8 with PACS) | **8 GB** (16 GB with PACS) | 500 GB listed; 150 GB usually enough; SSD preferred |
| OpenMRS, 1–10 users | 4 cores | 8 GB | 100 GB or more |
| OpenMRS, over 10 users | 8 cores or more | 16 GB | 100 GB or more, in RAID |

- **Decide the platform before the hardware.** A Raspberry Pi-class machine can run OpenMRS kits for
  small clinics; it **cannot run Bahmni**.
- Bahmni implementers advise more than the published minimum: one recommends **16 GB for about 10–15
  concurrent users, 32 GB for 25–50**, and PACS on its own server. Size for what you will run.
- Bahmni has **three databases** (OpenMRS in MySQL, OpenELIS and Odoo in PostgreSQL). Every backup step
  below covers all three.

## Where it lives

- A **large, sturdy, lockable metal cabinet** for the servers, their fans and the UPS batteries; metal
  door with a lock and bars on the windows of the room (OpenMRS Field Guide).
- **Central**, so the cable runs to the units stay under 90 m.
- **Within the equipment's temperature range.** ASHRAE recommends 18–27 °C for IT equipment; the
  OptiPlex 7020 servers at Lunsar are rated for 5–35 °C and 20–80 % humidity. An unventilated room in
  the tropics can exceed that — and the same heat halves battery life every 10 °C. Ventilate or cool,
  and **log the temperature**.
- Surge protection and voltage stabilisation on the supply ([Power](Power.md)).
- One named keyholder. Dust is the enemy — cleaning is on the maintenance schedule.

## Two servers if you can

**Server 1** runs Proxmox VE with two virtual machines: **VM 1** the hospital system (at least the
platform's requirements above), **VM 2** the VPN endpoint and monitoring (1–2 vCPU, 2 GB, 50 GB).
**Server 2** runs Proxmox Backup Server. One failure cannot take both the system and its backups.

## Backup: three copies, two media, one off site

| Copy | Where | How |
|---|---|---|
| 1 | Server 1 | the live data |
| 2 | Server 2 (Proxmox Backup Server) | nightly at 02:00: backup of both VMs **encrypted on the client** (AES-256-GCM), plus a dump of each of the three databases; keep 14 daily, 8 weekly, 6 monthly, dumps 30 days |
| 3 | **Off site:** the VPN hub server | nightly copy of the dumps, already encrypted, through the VPN |

**A building on the same campus is not off site** — a fire, flood or theft reaches both. If the
connection cannot carry the copy: encrypted USB drives, rotated, **kept away from the hospital site**.

**The encryption key** is printed as a QR code and held by the **hospital's owner**, not by a
volunteer. Lose the key and the backups are unreadable.

**Test a restore every month** (Proxmox Backup Server documentation). A backup nobody has restored is a
hope, not a backup.

Scripts: thesis Appendix F (database dump) — templates, no credentials in them.

## Recovery after a power cut — the machines

Three settings, each from the supplier's documentation. Set and **test all three by cutting the supply
under supervision**.

1. **Shut down before the battery is exhausted.** Connect the UPS by USB or network and run **NUT**
   (Network UPS Tools): it shuts the host down when the UPS is on battery and low.
2. **Power on when the supply returns.** Set the BIOS *AC Recovery* option to **Power On**. On the Dell
   OptiPlex 7020 it is **Power Off by default** — if you do not change it, the server stays off after
   every cut.
3. **Start the services in order.** In Proxmox, *Start at boot* plus a start order and delay, so the
   databases are up before the applications.

**Targets** (design targets of the thesis, not standards): lose at most **24 h** of data (RPO = the
backup interval); have the system back within **4 h** (RTO). A 150 GB restore over a 1 Gb/s link
takes about 20 minutes — the rest is diagnosis.

**If a server is lost:** install Proxmox VE on Server 2 or a replacement, restore the VMs from the
backup server, check against the last paper entries, re-enter what the paper forms hold.

## Recovery after a power cut — the people

The machines come back on their own. The hospital's work has to be organised. Write this procedure
**with the hospital**, before you leave, and leave it in the [handover pack](../4-Instruments/L1-Handover-Pack.md).
After the US contingency-planning guide (ONC SAFER, 2024) and the WHO handbook.

**During the outage**

- [ ] The IT technician — or the unit focal person — **declares downtime** and tells the units. The
      technician is in charge until it ends.
- [ ] Each unit records on its **emergency paper forms** — the same fields as its form in the system.
      **Stock in every unit: enough for at least 8 hours.**
- [ ] A patient registered during the outage gets a **temporary paper number**, written on every form.

**When the power returns**

- [ ] **Nobody enters data until the technician confirms** the system and its databases are running.
- [ ] Each unit enters its paper records. In Bahmni, clinical records go in **retrospective mode** so
      they carry the right date — it exists **only in the Clinical app**; test how registrations made on
      paper are back-dated before you rely on it.
- [ ] Temporary numbers replaced by the system's identifiers; sheets marked entered, signed, filed.

**Once a year:** a downtime drill with every unit.

## Bring a clone

From the 2017 Ethiopia deployment's contingency kit: **bring a tested, bootable clone of the whole
server** — in the Docker era, the images plus a recent database dump on a USB drive. A dead disk on
day three is then an afternoon, not a trip.

## Before you leave

- [ ] The owner has done a backup **and a restore** while you watched
- [ ] The restore is written in the runbook, with screenshots
- [ ] NUT shutdown, BIOS power-on and start order tested **by cutting the supply**
- [ ] The downtime procedure is written, the forms are stocked, and the units have rehearsed it
- [ ] The encryption key is with the hospital's owner
- [ ] The maintenance schedule is printed and on the wall

## Maintenance schedule

| When | What | Who | Check |
|---|---|---|---|
| Daily | Backup completed | Super-user | Green in PBS |
| Weekly | Disk usage on all VMs | Super-user | < 80 % |
| Weekly | UPS battery status | Super-user | Charged, no errors |
| Monthly | OS security updates | Remote engineer | |
| Monthly | Test a VM restore | Remote engineer | To a test VM, data checked |
| Quarterly | Review user accounts | Super-user + admin | Disable inactive |
| Quarterly | Clean the hardware | Super-user | Dust |
| Annually | Downtime drill with the units; full restore to the backup server | Remote + local | Procedure followed; restore within target |

!!! note "Expect a slow start"

    Bahmni's OpenMRS container takes **3–12 minutes** to become healthy after a restart; one rebuild
    with a large search index was observed at ~26 minutes. Put this in the runbook, or someone will
    restart it at 8:00 and declare it broken at 8:04.

!!! tip "In depth"

    Thesis §7.5–7.7 (requirements and sources), §8.2.1–8.2.2 (the procedure and configuration
    proposed), Figure 7 (reference design: backup and recovery).
