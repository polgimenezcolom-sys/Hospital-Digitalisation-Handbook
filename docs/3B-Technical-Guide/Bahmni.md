# Bahmni deployment

**Produces:** a phased Bahmni configuration, version-controlled per phase, with the folder ID as the
primary identifier and every screen stripped to what this hospital uses.

!!! warning "Status: v0.5 — procedure outline"

    The step-by-step configuration lives in the companion deployment repository and its per-phase
    `configuration/` folders. This page says what each phase contains and the rules that were learned;
    the repository holds the files. Link, do not paste.

## What runs

OpenMRS (clinical, MySQL) · Odoo 16 (pharmacy and stock, PostgreSQL) · OpenELIS (lab, PostgreSQL) ·
Reports / Metabase · an Apache reverse proxy — all in Docker Compose. Profiles select which start.

**Resources:** 12 GB RAM and 8 CPUs allocated to Docker was the working configuration of the test
instance. Published minimum: 8 GB; implementers advise 16 GB for 10–15 concurrent users.
OpenMRS takes **3–12 minutes** to become healthy after a restart — watch the log for
`Done refreshing Context` before deciding anything is wrong.

## Phase switching

Point `CONFIG_VOLUME` in the Docker `.env` at the phase's `configuration/` folder, `docker compose up
-d`, then **hard-refresh the browser** (`Ctrl+F5`) — it caches the JSON aggressively. Config-only edits
need only the refresh; the folders are bind-mounted.

## Phase 1 — Registration and the clinical record

Status: **configured on a test instance, not yet used by the hospital's staff.**

- **One mental model per person:** their unit is their login location, the visit type they open and
  the worklist they see. The hospital's eight units are the only visit types; types the hospital does
  not use are **retired, not deleted**, so a later phase can restore them.
- **One worklist per unit**, with the all-patients search kept, so a patient registered to the wrong
  unit can still be found. Moving a patient between units means closing one visit and opening another.
- **Error messages rewritten in plain language** through the translation files; generic errors left as
  they are, because specific wording would mislead.
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
Status: **open.** The laboratory is simplified; the pharmacy is not.

- **Laboratory (OpenELIS):** the technician's menu reduced to Home, Sample, Results, Validation and
  Reports; Administration hidden from everyone but the administrator — by a database migration and a
  style overlay kept in the repository.
- **Pharmacy: not yet simplified.** No way was found of reducing Odoo to the functions the pharmacy
  uses. Considered: a thin interface over Odoo, replacing Odoo with OpenBoxes, and the unsimplified
  interface — none judged ready for deployment. Odoo, when used, receives prescriptions as draft orders
  that the pharmacist confirms, which decrements stock; invoicing stays off until Phase 3.
- **Two defects open:** saving some observations fails because the forms refer to concepts that exist
  only in the test database, not in the version-controlled metadata; ordering from some orderable sets
  fails because their concept classes are not mapped to an order type. Both diagnosed, neither fixed.
- **Odoo boots with `-u all` by default and reverts every version-controlled SQL customisation on each
  restart.** Pin the service to `["odoo","-d","odoo"]`; after an image upgrade boot once with `-u all`,
  then re-apply the simplification SQL.
- Reports trimmed to this hospital's: stock demo reports that query concepts the dictionary does not
  have return errors — which teaches staff the system is broken. Remove them before training.

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
    `openmrs/apps/help/`. Companion thesis §8.3 (Bahmni phase by phase) and Appendix F.
