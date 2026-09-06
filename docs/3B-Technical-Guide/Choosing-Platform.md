# Choosing the platform

**Produces:** Bahmni or GNU Health — or something smaller — with the reason written down.

## First: which level?

Before any platform, decide the **level** with [B-2](../4-Instruments/B2-Level-Decision.md). Need
always points at level 4; the question is what the hospital can sustain. If the answer is level 1 or
2, this page does not apply — KoBoToolbox or DHIS2 is the platform.

## The two full systems

| | Bahmni | GNU Health |
|---|---|---|
| **What it is** | OpenMRS for clinical records + Odoo (or OpenBoxes) for pharmacy/stock + OpenELIS for lab + reporting, behind one proxy | One application on the Tryton framework with one PostgreSQL database for everything |
| **Architecture** | Several systems, several databases, integrated — or deliberately decoupled | Single database, single application |
| **Footprint** | Heavy: Docker stack, ~12 GB RAM comfortable | Light: runs on modest hardware, even ARM |
| **Customisation** | Config files and a form builder; simplification is deleting things from JSON | Tryton modules and PYSON; low-code within its model |
| **Community and support** | Large; commercial support firms in the region; a documented multi-country, multi-decade record | Smaller; enthusiastic; thin published longitudinal evidence |
| **Offline** | Once had Bahmni Connect; effectively unmaintained on current Docker releases | No native offline client |
| **What it is good at** | A hospital that will use lab, pharmacy and clinical together, and can afford the hardware and the support | A small facility, tight hardware, a team comfortable in Python |

## What the choice actually turns on

Not features. Both do registration, encounters, lab, pharmacy, reporting.

1. **Who will maintain it.** A part-time technician can keep GNU Health alive on one box. Bahmni's
   five containers reward someone who understands Docker.
2. **Whether commercial support can be bought.** For Bahmni, yes — several firms in West and East
   Africa. For GNU Health, less clearly.
3. **Hardware.** GNU Health runs where Bahmni will not.
4. **Track record.** OpenMRS/Bahmni has AMPATH, Lesotho, PIH, CURE — documented, multi-year. GNU
   Health's case for a mission hospital has to be made on architecture and footprint, because the
   published record is thin. That is a legitimate case; make it deliberately.

## The honest history

AUCOOP has chosen Bahmni **three times** — Meki 2017 (from a comparison of thirteen systems and a
hands-on test of three), and Lunsar 2026 (from a comparison of six). The 2017 reasoning is still
sound: Bahmni was "designed precisely for health centres in low-resource areas", and it had lab,
pharmacy and offline where OpenMRS alone did not. The 2024 Lunsar design chose **KoboToolbox over
any full system**, on the grounds that staff were not computer literate, and deferred a full HIS
until they were. Both decisions were reasonable. The 2026 deployment went to a full system anyway.

Whichever you choose: write the reason in the [level decision form](../4-Instruments/B2-Level-Decision.md),
and write what would have made you choose the other.

!!! tip "In depth"

    Companion thesis, Chapter 2 (the comparison matrix and its criteria) and Chapter 5, §5.1 (why two
    platforms were deployed). Bonet (2017), §7.1, for the earlier comparison.
