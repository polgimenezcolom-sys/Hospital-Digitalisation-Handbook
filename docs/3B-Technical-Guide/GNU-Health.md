# GNU Health deployment

**Produces:** a phase-1 GNU Health configuration for the model hospital.

!!! warning "Status: v0.2 — Phase 1 only"

    Phases 2–4 are not built. This page describes what exists and what the next phases would contain;
    it does not pretend they are done.

## What runs

GNU Health 5.0.6 on Tryton 7.0, one PostgreSQL database, the SAO web client on port 8000. Deployed
natively (Ubuntu 24.04 in WSL2 at Lunsar's model configuration), 46 modules activated. Runs on far
less hardware than Bahmni.

## Phase 1 — Registration and basic EMR

- Master patient index, wards, users, registration; malaria, maternity and nutrition encounters
  tested.
- **Eighteen custom clinical forms** in a custom Tryton module, with conditional visibility by PYSON:
  OPD, Emergency, Emergency bed, General ward, Maternity, Paediatrics, Under-5, ANC, Delivery,
  Neonatal, Dressing, Echo, Vaccination, Theatre, Bed-state totals, X-ray, Abortion, Death note.
- A lightweight mobile-friendly Flask app connecting directly to the database for tablet form entry.

Tagged `v1.0-phase1-registration` in the companion repository.

## Phases 2–4 — to build

Laboratory (GNU LIMS), pharmacy stock, billing, reporting. The single-database architecture makes
these additive rather than integrative — the main argument for GNU Health at a small site with a
part-time maintainer.

!!! danger "Where it runs"

    The model-configuration instance lives on an **external disk** — a single point of failure. Mount
    to run; back it up; document rebuild-from-repository before relying on it.

!!! tip "In depth"

    Companion deployment repository (`aucoop-gnuhealth-deployment`). Companion thesis, Chapter 5,
    §5.2.
