# Power and UPS

**Produces:** a UPS sized for the real load, with automatic voltage regulation; a solar system if
there is no reliable generator.
**Instrument:** [D-2](../4-Instruments/D2-Infrastructure-Audit.md), Electricity.

## Three layers, in this order

1. **Voltage regulation.** Grid voltage in these settings swings roughly between **170 V and 260 V**
   against a 220–240 V nominal. Equipment does not switch off — it runs badly and then a power supply
   fails months later, and nobody connects the two. A UPS with **automatic voltage regulation (AVR)**
   corrects the sag instead of passing it through. This is the layer people skip because the damage
   is invisible.
2. **Battery backup for a clean shutdown**, or to bridge to the generator. You are not trying to keep
   working through a four-hour outage. You are making sure the server is never surprised.
3. **Independent generation** — usually solar, sized for the IT load only — where there is no reliable
   generator.

## Step 1 — total the load

```
P_total = SUM( P_i × Q_i )   [W]
```

| Device | Typical W | Notes |
|---|---|---|
| Mini-PC / NUC server | 35–65 | |
| Raspberry Pi 4/5 as server | 5–15 | |
| Managed PoE switch, 24-port | 30–50 + PoE budget | the PoE budget is the big number |
| Access point via PoE | 10–15 | |
| Desktop workstation | 80–150 | prefer laptops — see below |
| Laptop | 30–65 | |
| Tablet charging | 10–15 | |
| Monitor 22" | 25–40 | |
| Router / gateway | 10–20 | |
| NAS / backup drive | 20–40 | |

**Worked example.** One mini-PC (50 W), one PoE switch with a 200 W PoE budget (250 W), four APs
(60 W), eight laptops (400 W), one NAS (30 W):

```
P_total = 50 + 250 + 60 + 400 + 30 = 790 W
```

## Step 2 — size the UPS

```
S_UPS = ( P_total × t_runtime ) / ( PF × η_UPS )   [VA]
```

| Parameter | Value |
|---|---|
| `t_runtime` | 0.25–1 h — enough to shut down cleanly or bridge to the generator |
| `PF` | ≈ 0.8 for IT loads |
| `η_UPS` | 0.85–0.90 |

```
S_UPS = ( 790 × 0.5 ) / ( 0.8 × 0.87 ) = 395 / 0.696 = 568 VA
```

Specify **1000–1500 VA** for headroom. Requirements: AVR, pure sine-wave output, and a USB port so
the server can be told to shut down when the battery runs low (see [Server](Server.md), NUT).

For scale: the 2017 Ethiopia deployment used two 650 VA units at about 71 € each for a single donated
server. Cheap, and it was the primary mitigation.

## Step 3 — solar, if needed

Only where there is no reliable generator. Size for the IT load, not the building.

```
E_daily  = P_total × h_operation                     [Wh/day]   h_operation ≈ 10–14 h
P_panel  = E_daily / ( h_sun × 0.70 )                [Wp]       h_sun ≈ 4–5.5 h; 0.70 = system losses
C_batt   = ( E_daily × d_autonomy ) / ( V_sys × DoD ) [Ah]      d ≈ 1–2 days; V_sys 24 or 48 V
```

DoD ≈ 0.50 for lead-acid, 0.80 for LiFePO4. LiFePO4 costs more up front and less over ten years
(3000+ cycles vs ~500).

**For Port Loko district**, worst-month irradiation is **August, 2.109 peak sun hours**; yearly
average 3.1. Design for August.

!!! warning "Check the units"

    The 2024 Lunsar design divided watt-hours by volts and read the result as watt-hours, concluding
    that one 250 Ah battery gave two days' autonomy. It gives about three hours. Work the battery
    step twice, and write the units next to every number.

## The part that is not about electricity

Everyone protects the server. Meanwhile the registration desk runs on a desktop plugged into the
wall, and that is the machine a clerk is typing into when the power goes.

**Prefer laptops over desktops at the point of care.** A laptop has a battery, so a power cut is an
inconvenience rather than a data-loss event. It is the cheapest reliability decision available.

## What to bring

Multimeter. A plug-in power meter (to measure real draw rather than nameplate). Surge-protected power
strips — more than you think. Universal plug adapters — the 2024 Lunsar BOM listed eighty.

!!! tip "In depth"

    AUCOOP's [Community Network Handbook — Power and UPS](https://aucoop.github.io/Community-Network-Handbook/3-Guide/Power-and-UPS/)
    covers the site-wide power question. Companion thesis, Chapter 4, Phase 1, for the derivations.
