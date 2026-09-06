# Network and connectivity

**Produces:** a LAN dimensioned for the real device count, segmented, with coverage **verified in every
target unit with the real application**.
**Instrument:** [D-2](../4-Instruments/D2-Infrastructure-Audit.md).

Three priorities, in order: **reliability** (fewest points of failure), **simplicity** (maintainable by
local staff), **efficiency** (power everything over PoE from one switch).

## Step 1 — dimension

1. **Inventory every device.** Wired: server, desktops, printers, PoE access points. Wireless:
   laptops, tablets, phones.
2. **Bandwidth.** A hospital-system workstation needs roughly 2–5 Mbps sustained. For *n* users:
   `BW = n × BW_per_user × CF`, with concurrency factor CF ≈ 0.3–0.5.
3. **Switch ports.** `Ports = ceil( (N_wired + N_AP + N_uplinks) × 1.2 )` — 20% spare.
4. **PoE budget.** Sum every PoE device's maximum draw and add 25%.

## Step 2 — topology

A **star** on a managed PoE switch:

- Internet gateway / router (NAT, DHCP, DNS, basic firewall)
- Core PoE switch — managed, 24 or 48 ports, PoE+ (802.3at), PoE budget ≥ 200 W
- Access points, each on one Cat6 run to the switch, powered by it
- Server on a Gigabit port

**Cabling:** Cat6 UTP in PVC conduit — rodents, moisture, accidents. Never more than 100 m on one run.
Between buildings beyond that: fibre or a point-to-point wireless bridge.

!!! danger "The ≤ 3 rule"

    If access points are cascaded — AP feeding AP feeding AP — one failure takes out everything
    downstream. Rule from the 2024 Lunsar design: **no more than three APs on one switch chain**;
    extend by adding a switch, in a star. (Rodríguez Trabal 2024, p. 32.)

## Two ways to link buildings — and Lunsar tried both

**Cabled star with point-to-point radios** (the 2024 design): cheap consumer APs in AP mode, Cat6
inside buildings, Ubiquiti directional links between them. Argued for on cost, per-AP
replaceability, and device flexibility. Never deployed.

**802.11s mesh on OpenWrt** (what was built in 2025): around 28 inexpensive routers reflashed with
OpenWrt, meshing wirelessly, with a fibre road crossing. Cheaper to run cable-free across a spread-out
campus; harder to reason about latency.

Both are legitimate. The handbook's position: **measure latency at the far end of whatever you build,
with the real application.** A mesh that is fine for form uploads can be unusable for a browser-based
hospital system at the fourth hop. The Lunsar mesh was measured against KoboCollect and has never been
re-measured with Bahmni running.

## Step 3 — lightning

The area has frequent storms and the hospital's rod may not catch every strike. Two rules from the
2024 design that the 2025 deployment kept:

- **A PoE surge arrester, grounded, on every Ethernet run**, doubled at the first device after any
  outdoor radio.
- **Fibre for any link between buildings**, especially across the road — glass carries no conductor
  and cannot carry a strike from one building into the next. At Lunsar the road crossing between
  AP21 and AP4 is fibre for exactly this reason.

## Step 4 — coverage

| Obstacle | Attenuation | Radius per AP |
|---|---|---|
| Open space | — | 25–35 m |
| Drywall / wood | −3 to −5 dB | |
| One concrete block wall | −10 to −15 dB | 10–15 m |
| Two concrete walls | | 5–8 m — usually needs another AP |
| Reinforced concrete | −15 to −25 dB | |
| Metal door | −20 to −30 dB | |

One AP per ward or clinical area, centrally, ceiling-mounted. One per floor per zone in multi-storey
buildings. Non-overlapping channels: 1/6/11 on 2.4 GHz; any non-overlapping on 5 GHz. Reuse a 5 GHz
channel only across separate buildings. Check the national spectrum plan for what is permitted.

**Then walk it.** Desk estimates at 10–15 m spacing are a starting point; the count changes on site.
Every target unit gets a signal and latency reading, in the room, with the application.

## Step 5 — segment

| VLAN | Who | Rule |
|---|---|---|
| 10 Clinical | Workstations and tablets on the hospital system | No internet — reduces malware risk |
| 20 Administration | Finance, management | Internet for email and reporting |
| 30 Server | Hospital system server, NAS | Reachable from 10 and 20 only |
| 40 Guest (optional) | Personal devices | Isolated from everything clinical |

Inter-VLAN routing on the gateway, with rules permitting only what is needed. A flat network with one
password is simpler and it is how the 2024 design started; segment as soon as there is a server.

## Example equipment, small hospital, three buildings

| Item | Example | Qty | ≈ EUR |
|---|---|---|---|
| Gateway / router | MikroTik hEX | 1 | 60 |
| Core PoE switch, 24-port | TP-Link TL-SG2428P | 1 | 280 |
| Extension switch, 8-port PoE | TP-Link TL-SG108PE | 1 | 65 |
| Access points | Ubiquiti U6 Lite | 5 | 500 |
| Cat6, 305 m box | | 2 | 140 |
| RJ45 + crimper | | 1 | 30 |
| PVC conduit, 50 m | | 4 | 60 |
| Patch panel | | 1 | 35 |
| Wall cabinet, 6U | | 1 | 80 |
| **Network total** | | | **≈ 1,250** |

For comparison: the 2024 Lunsar design costed a 22-AP cabled network with point-to-point radios,
tablets and solar at **5,866 €**; the 2025 mesh used routers at about 25 € each. Yassa–Douala did it
for around **2,000 €** of network equipment plus 2,000–2,500 € of tablets, with no VLANs and aerial
cabling by the hospital's own technician — and Douala is the site that adopted.

!!! tip "In depth"

    [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/) — Network Planning, Wireless Mesh, IP Addressing, Flash
    OpenWrt, Antennas. The 2025 Lunsar mesh follows their pattern.
