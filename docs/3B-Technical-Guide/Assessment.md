# Assessing the site

**Produces:** a completed [D-2 infrastructure audit](../4-Instruments/D2-Infrastructure-Audit.md), a
yes/no on carrier-grade NAT, and a coverage map you walked yourself.
**When:** first three to five days on site.

## Why you cannot do this from Barcelona

The 2024 network design for Lunsar was done remotely. It estimated 22 access points at 10–15 m
spacing on a floor plan; the deployed mesh has around 28. It could not know that Emergency's cable
would never be verified, or that grid voltage swings between 170 V and 260 V. Its author said so:
*"once on-site, we will be able to take exact measurements."* Three to five days of measurement on
site is worth more than a month of design at home.

## Steps

**Day 1 — walk the whole site.**

1. Get the [campus map](../5-Real-Deployments/5.2-Lunsar.md) or draw one. Every building, every
   unit, distances between them, what crosses open ground or a road.
2. Photograph every room where a workstation might go: sockets, cable routes, wall material, where a
   desk could sit.
3. Note wall materials — concrete block and reinforced concrete kill signal; wood and drywall do not.

**Day 1–2 — power.**

4. Put a multimeter on the grid supply and log readings across 24 hours: minimum, maximum, typical.
   The spread matters more than the average.
5. Observe grid hours per day — do not accept the answer you are given.
6. Generator: fuel type, capacity, runtime, and — the real question — how reliably fuel is available.
7. Any solar: panel count, orientation, rating, battery capacity and age.

**Day 2 — internet and CGNAT.**

8. Measure real bandwidth, down and up, at two times of day. Note the ISP and technology.
9. **Check for carrier-grade NAT, now, because it changes the architecture:** compare the WAN address
   on the router's status page with what a public "what is my IP" service reports. Different means
   CGNAT, and no inbound connection will ever work. See [Remote support](Remote-Support.md).
10. Note the monthly cost. The hospital inherits it.

**Day 2–3 — existing IT.**

11. Count functional computers and tablets, with OS and age. Printers. Any existing network gear —
    model, location, does it work.
12. **Ask about existing software.** Finance packages, form-collection tools, anything a previous team
    installed. Find the server if there is one. At Lunsar this question would have found Quickbooks
    Enterprise 2016 and a 2023 KoboToolbox deployment.

**Day 3 — coverage, physically.**

13. If there is an existing network, walk every target unit with a device and test the actual
    application, not a ping. Record signal and latency room by room.
14. If there is none, note candidate AP positions on the map — centrally in each area, ceiling-mounted
    if possible — and expect to revise on install day.

**Day 3–5 — environment and space.**

15. Candidate server room: ventilation, security, who has a key, dust, flooding risk.
16. Temperature and humidity range. Insects and rodents — cable insulation is food.
17. Lightning frequency and existing protection. Ask; then look at the lightning rod.

## Outputs

- [D-2](../4-Instruments/D2-Infrastructure-Audit.md), completed with readings not estimates
- A map with verified coverage per unit, and candidate AP positions
- The CGNAT answer, written down
- The list of existing systems and who runs them

!!! danger "Stop"

    If a unit scheduled for the first phase has no verified power and no verified network link, it
    cannot be in the first phase. Getting the link in *is* the project for this trip.
