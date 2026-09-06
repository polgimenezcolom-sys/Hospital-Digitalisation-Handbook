# The Technical Guide

Recipes for the infrastructure and the software. Self-contained — open the one you need.

The [organisational guide](../3A-Organisational-Guide/index.md) comes first for a reason: nothing
here survives without it. But nothing there works without this either. A hospital information system
on a server that corrupts its database at every power cut is not a system.

| | Recipe | Produces |
|---|---|---|
| 1 | **[Assessing the site](Assessment.md)** | A completed [D-2](../4-Instruments/D2-Infrastructure-Audit.md), a CGNAT answer, and a verified coverage map |
| 2 | **[Power and UPS](Power.md)** | A sized UPS with voltage regulation, and — if needed — a solar system |
| 3 | **[Network and connectivity](Network.md)** | A dimensioned, segmented LAN with verified coverage in every target unit |
| 4 | **[Server and backup](Server.md)** | A server that survives a power cut, and a backup that has been restored |
| 5 | **[Remote support](Remote-Support.md)** | A tunnel through carrier-grade NAT, monitoring, and safely handled credentials |
| 6 | **[Choosing the platform](Choosing-Platform.md)** | Bahmni or GNU Health, with the reason written down |
| 7 | **[Bahmni deployment](Bahmni.md)** | Phase by phase |
| 8 | **[GNU Health deployment](GNU-Health.md)** | Phase by phase |
| 9 | **[Packing list](Packing-List.md)** | What to bring, from two deployments' worth of things nobody brought |

!!! tip "Networking in depth lives next door"

    AUCOOP's [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/) has full recipes for OpenWrt, mesh, addressing,
    Proxmox, Zabbix, VPN and power. Where the two overlap, this guide gives the hospital-specific
    rule and links to theirs for the procedure.

!!! note "Where the rationale is"

    Every recipe here says *what to do*. The *why* — the dimensioning theory, the comparison of
    alternatives, the evidence — is in the companion thesis, Chapter 4 (infrastructure) and Chapter 5
    (software). These pages point at it rather than repeat it.
