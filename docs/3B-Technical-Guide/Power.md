# Power and UPS

**Produces:** no hospital-system equipment on unprotected supply; a UPS sized on both its rating and
its stored energy; a solar system sized for the worst month, if there is no reliable generator.
**Instrument:** [D-2](../4-Instruments/D2-Infrastructure-Audit.md), rows *Power* and *Location*.

The rule, from hospital engineering guidelines: **servers and the network core never run on raw
mains or a raw generator.** Everything below serves that rule. The reasoning and every source are in
the companion thesis, §7.3.

## Step 1 — log the voltage before you choose a UPS

Log the supply voltage for **at least one full day**. A line-interactive UPS stops regulating below
roughly 184 V on a 230 V supply and goes to battery; if the log dips below that, specify a
**double-conversion** UPS. Whatever the topology, it must have **automatic voltage regulation (AVR)**.

## Step 2 — total the load, then take the critical part

```
P_total = SUM( P_i × Q_i )   [W]
```

Use **nameplate or measured** values for the equipment actually installed. The table is only for a
first estimate.

| Device | Indicative W |
|---|---|
| Mini-PC server | 35–65 |
| Managed PoE switch, chassis only | 30–50 |
| Access point via PoE | 10–15 |
| Laptop | 30–65 |
| Tablet charging | 10–15 |
| Router / gateway | 10–20 |
| Backup storage | 20–40 |

**Do not add the switch's PoE budget to the total.** The budget is what it *can* deliver, not what it
draws; count the chassis and the devices actually powered.

The UPS carries only the **critical load**: server(s), switch chassis, the access points that carry
traffic to the server, router, backup storage. **Laptops and tablets stay off the UPS** — they have
their own batteries, and putting them on would roughly triple the UPS for nothing.

**Worked example (thesis §7.3):** 50 + 40 + 69 (5 APs incl. PoE losses) + 15 + 30 = **204 W critical**.

## Step 3 — size the UPS on two numbers, separately

```
S_UPS = P_crit / PF              [VA]   PF = 0.95 (modern IT power supplies)
E_UPS = P_crit × t / η_UPS        [Wh]   t = runtime in h, η_UPS = 0.87
```

For 204 W and 30 minutes: **215 VA** and **117 Wh**.

!!! danger "Buy the energy, not the VA"

    A 600 VA unit passes the 215 VA rating several times over — and its single 12 V 7 Ah battery
    holds 84 Wh, of which about 42 Wh is usable. A third of what is needed. **A UPS chosen on its VA
    rating alone will be undersized for runtime, and you will find out during an outage.** Specify the
    battery in Wh, and multiply it by the ageing factor in Step 5.

USB or network port required, so the server can be told to shut down — see
[Server](Server.md), *Recovery after a power cut*.

## Step 4 — solar, if there is no reliable generator

Size for the IT load, not the building.

```
E_daily  = P_total × h_operation                                  [Wh/day]
P_panel  = E_daily / ( h_sun × 0.70 )                             [Wp]
C_batt   = ( E_daily × d_autonomy × k_age × k_T ) / ( V_sys × DoD ) [Ah]
```

| Term | Value | Why |
|---|---|---|
| `h_sun` | **worst month**, not the annual average. Lunsar: August, 3.8–4.3 PSH → use **4.0** | A stand-alone system must work in the monsoon |
| `0.70` | system derate | built from PVWatts losses × inverter × charge controller and battery |
| `d_autonomy` | **3 days** with a manual-start generator; 4–5 with none | One day of autonomy blacked out in every modelled year |
| `DoD` | 0.80 LiFePO4, 0.50 lead-acid | |
| `k_age` | **1.25** | battery still meets the load at 80 % of rated capacity (end of life) |
| `k_T` | 1 for rooms above 25 °C | cold reduces capacity; heat does not — heat shortens life |

!!! warning "Check the units"

    The 2024 Lunsar design divided watt-hours by volts and read the result as watt-hours, concluding
    that one 250 Ah battery gave two days' autonomy. It gives about three hours. Work the battery
    step twice, and write the units next to every number.

## Step 5 — heat, and the battery replacement date

Heat does not make the bank bigger; it makes it **die sooner**. For lead-acid (VRLA/AGM), life halves
for every 10 °C above 20 °C — one manufacturer gives 7–10 years at 20 °C, **4 years at 30 °C, 2 years
at 40 °C**. LiFePO4 charges only between 5 and 50 °C; use the manufacturer's data.

- [ ] Log the room temperature.
- [ ] Write the installation date on every battery.
- [ ] Put the replacement date — from the room temperature — in the budget and in the
      [handover pack](../4-Instruments/L1-Handover-Pack.md).

## The part that is not about electricity

Everyone protects the server. Meanwhile the registration desk runs on a desktop plugged into the
wall. **Prefer laptops over desktops at the point of care**: a power cut becomes an inconvenience,
not a data-loss event.

## What to bring

Multimeter. A voltage logger (or a meter you can read through a day). A plug-in power meter, to
measure real draw. Surge-protected power strips — more than you think. Universal plug adapters — the
2024 Lunsar bill of materials listed eighty.

!!! tip "In depth"

    Thesis §7.3 (derivations and sources) and Figure 6 (reference design: power and equipment).
    AUCOOP's [Community Network Handbook — Power and UPS](https://aucoop.github.io/Community-Network-Handbook/3-Guide/Power-and-UPS/)
    covers the site-wide power question.
