# Power and UPS

!!! warning "Outline — partially written"

## Calculating the load

Total IT load is the sum of each device's draw times how many of them there are:

```
P_total = SUM( P_i x Q_i )   [watts]
```

**Worked example** — one mini-PC server (50 W), one PoE switch including its PoE budget (250 W),
four access points (60 W), eight laptops (400 W), one backup drive (30 W):

```
P_total = 50 + 250 + 60 + 400 + 30 = 790 W
```

## Sizing the UPS

```
S_UPS = (P_total x t_runtime) / (PF x efficiency)   [VA]
```

| Parameter | Typical value |
|---|---|
| `t_runtime` | 0.25–1 h — enough to shut down cleanly or bridge to a generator |
| `PF` (power factor) | ≈ 0.8 for IT loads |
| `η_UPS` (efficiency) | 0.85–0.90 |

**Worked example** — 790 W, 0.5 h, PF 0.8, η 0.87:

```
S_UPS = (790 x 0.5) / (0.8 x 0.87) = 395 / 0.696 = 568 VA
```

Specify **1000–1500 VA** to leave headroom for expansion.

!!! danger "Automatic voltage regulation is not optional"

    Grid voltage swings roughly between **170 V and 260 V** against a 220–240 V nominal. A UPS
    without AVR passes that straight through to your equipment. This is the layer people skip because
    the damage is invisible until a power supply fails months later.

## Still to write

- Solar sizing for an IT-only load: daily energy, panel rating, battery capacity, days of autonomy.
- Battery technology comparison and expected life in high ambient temperature.
- Specific equipment recommendations (three `TODO` markers remain in the thesis on this).
- Protecting the *workstation*, not just the server — why laptops beat desktops at the point of care.

**Source material:** thesis Chapter 4, Phase 1 (Power Infrastructure).
