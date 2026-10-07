# Network and connectivity

**Produces:** a LAN that reaches every unit using the system, with an **interactive response verified
in every target unit with the real application**.
**Instrument:** [D-2](../4-Instruments/D2-Infrastructure-Audit.md), rows *Network*.

Two requirements, in this order: **reach** — every unit that uses the system reaches the server — and
**response** — a browser-based record asks the server at every step, so latency matters as much as
bandwidth. Reasoning and sources: thesis §7.4.

Three priorities, in order: **reliability** (fewest points of failure), **simplicity** (maintainable by
local staff), **efficiency** (power everything over PoE from one switch).

## Step 1 — dimension

1. **Inventory every device.** Wired: server, desktops, printers, PoE access points. Wireless:
   laptops, tablets, phones.
2. **Bandwidth.** `BW = n × BW_per_user × CF`, with **0.5 Mbit/s per user** and **CF = 0.4**. Both
   are declared assumptions: neither Bahmni nor OpenMRS publishes a bandwidth figure (DHIS2 gives
   80 kbit/s per client). At a hospital of this size the uplink is very unlikely to be the constraint;
   latency is.
3. **Switch ports.** `Ports = ceil( (N_wired + N_AP + N_uplinks) × 1.2 )` — 20 % spare.
4. **PoE budget.** Sum the **per-port supply figure of each device's PoE Type** — 15.4 W (Type 1),
   30 W (Type 2), 60 W (Type 3), 90 W (Type 4). Do **not** add 25 % on top: the standard already
   allows for cable loss in that figure.

## Step 2 — topology

A **star** on a managed PoE switch:

- Internet gateway / router (NAT, DHCP, DNS, basic firewall)
- Core PoE switch — managed, 24 or 48 ports, PoE+ (802.3at), PoE budget ≥ 200 W
- Access points, each on one Cat6 run to the switch, powered by it
- Server on a Gigabit port

**Cabling** (Victorian hospital engineering guideline): horizontal runs **under 90 m**, whole channel
under 100 m; **at least 150 mm from power cables**; **20 % spare** capacity. Cat6 in PVC conduit
against rodents and moisture. Between buildings beyond that, or wherever a cable would cross between
buildings exposed to lightning: fibre or a point-to-point wireless link.

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

- **One access point for every 200 m² or less, no more than 15 m apart** (Victorian guideline).
- Concrete and block walls attenuate more than the partitions those figures assume — so the desk
  plan is only a starting point.
- 2.4 GHz has only three non-overlapping channels (1/6/11); give neighbouring APs different ones.
  Check the national spectrum plan for what is permitted.

**Then walk it.** With the access points in place, measure signal strength **and response time with
the real application** at every workstation position. The units furthest from the core in hops are
the ones to check first.

## Step 5 — segment

Separating clinical devices, the management interfaces of the servers and network equipment, and any
guest access, with filtering between them, is a **requirement** (thesis §7.4.5). The segment plan
and the rules depend on the network actually installed, and the thesis leaves their design to future
work. The table below is a **starting point to adapt, not a tested design** — no AUCOOP site has run
it yet. Record what you build in [D-2](../4-Instruments/D2-Infrastructure-Audit.md).

| VLAN | Who | Rule |
|---|---|---|
| 10 Clinical | Workstations and tablets on the hospital system | No internet — reduces malware risk |
| 20 Administration | Finance, management | Internet for email and reporting |
| 30 Server and management | Hospital system server, backup server, switch and router management | Reachable from 10 and 20 only on the ports the system uses |
| 40 Guest (optional) | Personal devices | Isolated from everything clinical |

## Example equipment, small hospital, three buildings

Indicative 2026 prices for planning, not quotations. Check current prices before you budget.

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

    Thesis §7.4 (sources) and Figure 8 (reference design: how data flows).
    [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/) — Network Planning, Wireless Mesh, IP Addressing, Flash
    OpenWrt, Antennas. The 2025 Lunsar mesh follows their pattern.
