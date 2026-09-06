# Server and backup

**Produces:** a server sized for the hospital, on a UPS it can talk to, with a backup that has been
**restored** in front of the owner.

## Size it

| | Small (< 500 patients/month) | Medium (500–2000) | Large (> 2000) |
|---|---|---|---|
| CPU | 4-core ARM/x86 | 4-core x86 | 8-core x86 |
| RAM | 4–8 GB | 8–16 GB | 16–32 GB |
| Storage | 128 GB SSD | 256–512 GB SSD | 512 GB–1 TB SSD |
| Hardware | Raspberry Pi 5 | Intel NUC / mini-PC | Tower |
| Power | 10–15 W | 35–65 W | 100–250 W |
| ≈ EUR | 100–200 | 300–600 | 600–1500 |

A clinical database grows roughly 1–5 GB a year at medium volume. A 256 GB SSD is decades of text.

**Bahmni needs more than this table.** Its Docker stack — OpenMRS, Odoo, OpenELIS, reporting, a
reverse proxy — wants 12 GB of RAM and eight cores to be comfortable. Size for what you are actually
running.

## Where it lives

A room with ventilation, a lock, and one named keyholder. Off the floor. Away from the window. Dust
is the enemy — quarterly cleaning is on the maintenance schedule below.

## Operating system and virtualisation

- **Small hospital:** bare-metal install of the platform on its recommended OS. Simplest to maintain.
- **Medium or larger:** **Proxmox VE** as hypervisor. Web GUI from any workstation on the LAN, so no
  terminal for routine tasks; snapshot before every update and restore in minutes if it goes wrong;
  native backup integration.

Recommended layout on Proxmox: **VM 1 — the hospital system** (2–4 vCPU, 4–8 GB, 200 GB thin);
**VM 2 — services** (WireGuard endpoint, monitoring; 1–2 vCPU, 2 GB, 50 GB).

## Two servers if you can

Hardware failure here is not exceptional; it is scheduled. Heat, dust, humidity and voltage make sure
of it. **Server 1** runs Proxmox with the VMs. **Server 2** runs Proxmox Backup Server. One failure
cannot take both the system and its backups.

Targets: **RPO ≤ 24 h** with daily backups (≤ 6 h with 6-hourly incrementals); **RTO ≤ 4 h** including
diagnosis — a 50–100 GB VM restores in 15–45 minutes.

If only one server: automated database dumps to an external USB drive, rotated to another building,
plus offsite over the VPN when bandwidth allows.

## The 3-2-1 rule, adapted

- **3 copies:** production, local backup, offsite
- **2 media:** the server's SSD, and a separate server or external drive
- **1 offsite:** encrypted to the VPS over the VPN, or encrypted USB drives rotated to a different
  building

**Schedule.** Daily 02:00 incremental to PBS; weekly Sunday 03:00 full; keep 14 daily, 8 weekly,
6 monthly; nightly database dump synced offsite if the tunnel is up.

**Application-level dump as well** — VM backups plus a database dump give you granular recovery:

```bash
#!/bin/bash
# daily, 02:00, via cron
BACKUP_DIR=/backup/his
DATE=$(date +%Y-%m-%d)
pg_dump -U his -Fc his_db > $BACKUP_DIR/his_$DATE.dump
find $BACKUP_DIR -name "*.dump" -mtime +30 -delete
rsync -avz $BACKUP_DIR/ vps:/offsite-backup/his/   # only if the VPN is up
```

## Tell the server about the UPS

Connect the UPS by USB and run **NUT** (Network UPS Tools). It watches battery, input voltage and load,
and shuts the VMs down cleanly at a threshold — say 20% — so an extended outage never corrupts the
database. It also logs every power event, which is evidence for the next team.

## Bring a clone

From the 2017 Ethiopia deployment's contingency kit: **bring a tested, bootable clone of the whole
server** — in the Docker era, the images plus a recent database dump on a USB drive. A dead disk on
day three is then an afternoon, not a trip.

## Before you leave

- [ ] The owner has done a backup **and a restore** while you watched
- [ ] The restore is written in the runbook, with screenshots
- [ ] NUT is shutting the VMs down on battery — tested by pulling the plug
- [ ] The maintenance schedule is printed and on the wall

## Maintenance schedule

| When | What | Who | Check |
|---|---|---|---|
| Daily | Backup completed | Super-user | Green in PBS |
| Weekly | Disk usage on all VMs | Super-user | < 80% |
| Weekly | UPS battery status | Super-user | > 90%, no errors |
| Monthly | OS security updates | Remote engineer | |
| Monthly | Test a VM restore | Remote engineer | To a test VM |
| Quarterly | Review user accounts | Super-user + admin | Disable inactive |
| Quarterly | Clean the hardware | Super-user | Dust |
| Annually | Full disaster-recovery drill | Remote + local | Restore to the backup server |

!!! note "Expect a slow start"

    Bahmni's OpenMRS container takes **3–12 minutes** to become healthy after a restart; one rebuild
    with a large search index was observed at ~26 minutes. Put this in the runbook, or someone will
    restart it at 8:00 and declare it broken at 8:04.
