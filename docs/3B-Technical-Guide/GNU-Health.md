# GNU Health deployment

**Produces:** a phase-1 GNU Health configuration for the model hospital.

!!! danger "Status: no phase achieved — the platform is on standby"

    GNU Health was installed, configured against the model hospital profile, and tagged — but the
    **interface simplification that Phase 1 requires was not achieved in the time available**, and
    the platform is on standby.

    Read that precisely. It was **not** shown to be impossible, and this page does not claim it is.
    What the deployment found is a difference in the *kind of work* each platform demands:

    > In Bahmni, interface simplification is a **configuration** activity. In GNU Health it is a
    > **development** activity.

    GNU Health's own documentation routes view customisation through writing a local
    `z_health_<name>` Python module, so that changes survive an update. Independent work points the
    same way without going further: Badosa (2015, FIB-UPC) recorded Tryton's limited customisation as
    a formal obstacle while *adding* a module; Purkayastha et al. (2019) scored GNU Health lowest of
    five open-source EHRs against 32 functional criteria.

    **What this means for you.** If your team includes a Python developer with time, this is a
    solvable problem and nobody has yet published the solution — doing it and writing it up would be
    a real contribution. If it does not, expect simplification to cost development effort that a
    Bahmni deployment would spend in configuration. That difference decides maintainability for an
    association whose next team is unknown. See [Choosing the platform](Choosing-Platform.md).

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
