# Bahmni deployment

!!! warning "Outline — not yet written"

**What this page will contain**

- Architecture and what actually runs: OpenMRS for clinical records, a separate system for pharmacy
  and stock, another for laboratory, behind one reverse proxy.
- Installation with Docker Compose, and realistic resource requirements.
- **Phase 1 — Registration and basic EMR.** Making the folder ID the primary searchable identifier.
  Custom clinical forms. Stripping the consultation screen down.
- **Phase 2 — Laboratory and pharmacy.** Order to result. Dispensing that decrements stock. The
  decoupled versus integrated question.
- **Phase 3 — Billing and administration.** Not greenfield: expect an incumbent finance system.
- **Phase 4 — Reporting.** Role-gated reports; producing the statutory monthly return.
- Configuration is version-controlled per phase; switching phases means pointing the config volume
  at a different folder and restarting.

**Source material:** thesis Chapter 5, §5.3, plus the companion deployment repository, which holds
the actual configuration files and is the thing to link to rather than paste.
