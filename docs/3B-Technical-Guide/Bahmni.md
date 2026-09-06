# Bahmni deployment

**Produces:** a phased Bahmni configuration, version-controlled per phase, with the folder ID as the
primary identifier and every screen stripped to what this hospital uses.

!!! warning "Status: v0.2 — procedure outline"

    The step-by-step configuration lives in the companion deployment repository and its per-phase
    `configuration/` folders. This page says what each phase contains and the rules that were learned;
    the repository holds the files. Link, do not paste.

## What runs

OpenMRS (clinical, MySQL) · Odoo 16 (pharmacy and stock, PostgreSQL) · OpenELIS (lab, PostgreSQL) ·
Reports / Metabase · an Apache reverse proxy — all in Docker Compose. Profiles select which start.

**Resources:** 12 GB RAM and 8 CPUs allocated to Docker was the working configuration at Lunsar.
OpenMRS takes **3–12 minutes** to become healthy after a restart — watch the log for
`Done refreshing Context` before deciding anything is wrong.

## Phase switching

Point `CONFIG_VOLUME` in the Docker `.env` at the phase's `configuration/` folder, `docker compose up
-d`, then **hard-refresh the browser** (`Ctrl+F5`) — it caches the JSON aggressively. Config-only edits
need only the refresh; the folders are bind-mounted.

## Phase 1 — Registration and basic EMR

- **The folder ID is the primary searchable identifier.** Not a secondary attribute. Registration is a
  single event at Reception; every other unit consumes the identity.
- Custom clinical forms per unit through the Implementer Interface; consultation limited to
  observations, diagnosis, disposition and summary; patient dashboard with vitals, observations,
  allergies, visits.
- Reports gated by privilege. **Check the gating by logging in as each role** — at Lunsar the Phase-1
  tile was gated on the board privilege and doctors could not open reports at all until Phase 2 fixed
  it.
- Bonet's 2017 registration recipe still applies conceptually: minimal person attributes, address
  hierarchy with village autocomplete, fee field disabled, CSV patient import.

## Phase 2 — Laboratory and pharmacy

- Lab and Pharmacy home tiles, privilege-gated; medications and orders tabs; treatments widget;
  pharmacy queue.
- **Pharmacy: two approaches, both documented.** Odoo tightly integrated (prescriptions sync as draft
  quotations; pharmacist confirms; stock decrements) — built-in, heavier, more moving parts. Or
  decoupled: the pharmacist reads a "pending prescriptions" report and records the movement by hand,
  ~30 s per transaction — resilient to a bad network and a missing DBA. Lunsar's live backend is
  Odoo, cut to a **two-screen dispensing flow**; invoicing off until Phase 3.
- **Odoo boots with `-u all` by default and reverts every version-controlled SQL customisation on each
  restart.** Pin the service to `["odoo","-d","odoo"]`; after an image upgrade boot once with `-u all`,
  then re-apply the simplification SQL.
- Reports trimmed to this hospital's: ~44 stock demo reports removed because they query concepts the
  dictionary does not have and return errors — which teaches staff the system is broken.

## Phase 3 — Billing and administration

**Not greenfield.** Expect an incumbent finance system — Quickbooks Enterprise 2016 at Lunsar, asked
for in 2018. Inventory it before scoping billing; the exit gate is reconciliation with it, signed off
by the finance director. Not yet deployed.

## Phase 4 — Reporting and epidemiology

The statutory monthly return, produced by hospital staff, unaided. Aggregate by the administrative
unit the returns report by (district). Standard diagnosis coding. Keep the export simple enough that
whoever integrates with the national system in two years can. Not yet deployed.

## Simplification — the rule

Every field on a screen earns its place by being used, today, by this person. Optional fields are left
blank; pointless mandatory ones get rubbish. Delete before you train.

!!! tip "In depth"

    Companion deployment repository (`aucoop-bahmni-deployment`) — `AGENTS.md`, per-phase
    `configuration/`, `docs/user-guides/`, and the in-product Help Center under
    `openmrs/apps/help/`. Companion thesis, Chapter 5, §5.3.
