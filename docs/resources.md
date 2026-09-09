# Resources and downloads

Everything you can take away from this handbook, in one place.

## The instrument forms

Ten instruments. Nine are completed on the trip; [S-1](4-Instruments/S1-Follow-Up.md) is completed
six and twelve months later, by the person named in L-1.

Print and fill by hand, or fill on a computer. Each carries the handbook version in its footer.

| | Instrument | PDF | DOCX | Phone |
|---|---|---|---|---|
| **B-1** | Readiness assessment | [PDF](forms/B1_Readiness_Assessment.pdf) | [DOCX](forms/B1_Readiness_Assessment.docx) | |
| **B-2** | Level decision | [PDF](forms/B2_Level_Decision.pdf) | [DOCX](forms/B2_Level_Decision.docx) | |
| **B-3** | Mandate and ownership | [PDF](forms/B3_Mandate_and_Ownership.pdf) | [DOCX](forms/B3_Mandate_and_Ownership.docx) | |
| **D-1** | Field data capture | [PDF](forms/D1_Data_Capture_Sheet.pdf) | [DOCX](forms/D1_Data_Capture_Sheet.docx) | **[KoBo XLSForm](forms/D1_Data_Capture_KoBo.xlsx)** |
| **D-2** | Infrastructure audit | [PDF](forms/D2_Infrastructure_Audit.pdf) | [DOCX](forms/D2_Infrastructure_Audit.docx) | |
| **D-3** | Workflow mapping | [PDF](forms/D3_Workflow_Mapping.pdf) | [DOCX](forms/D3_Workflow_Mapping.docx) | |
| **D-4** | Phase exit gate | [PDF](forms/D4_Phase_Exit_Gate.pdf) | [DOCX](forms/D4_Phase_Exit_Gate.docx) | |
| **L-1** | Handover pack | [PDF](forms/L1_Handover_Pack.pdf) | [DOCX](forms/L1_Handover_Pack.docx) | |
| **A-1** | Debrief and feedback | [PDF](forms/A1_Debrief_and_Feedback.pdf) | [DOCX](forms/A1_Debrief_and_Feedback.docx) | |
| **S-1** | Six- and twelve-month check | [PDF](forms/S1_Six_and_Twelve_Month_Check.pdf) | [DOCX](forms/S1_Six_and_Twelve_Month_Check.docx) | |

**Using the KoBo form.** Create a free project at [kobotoolbox.org](https://www.kobotoolbox.org/),
choose *Upload an XLSForm*, deploy, then install **KoboCollect** on the team's phones and download
the form while you still have internet. It works fully offline and attaches photographs to each
entry. This is the same tool AUCOOP used at Lunsar in 2023 — deliberately.

The forms are generated from `scripts/build_forms.py` in the repository, so they stay in step with
the handbook version. Change the script, not the files.

## Companion repositories

- **Bahmni deployment** — per-phase configuration, user guides, in-product Help Center
  *(private; ask the maintainer)*
- **GNU Health deployment** — Phase 1, tagged `v1.0-phase1-registration` *(private)*

## Related AUCOOP handbooks

- [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/) — mesh, OpenWrt,
  addressing, Proxmox, Zabbix, VPN, power. The network layer this handbook defers to.

## Prior work from the same association

- **Bonet Armengol, A. (2017).** *Suport TIC en centres de salut en zones rurals i aïllades.* TFG,
  ETSETB-UPC. [hdl.handle.net/2117/106696](https://hdl.handle.net/2117/106696) — Bahmni at Meki,
  Ethiopia; the first attempt at this methodology.
- **Rodríguez Trabal, E. (2024).** *Digital Transformation to Improve Hospital Efficiency at Saint
  John of God Hospital in Sierra Leone.* TFG, ETSETB-UPC — the pre-deployment network design for
  Lunsar, the campus map, and the lightning analysis.
- **Giménez Colom, P. (2026).** *Methodological Guide for the Implementation of Open-Source Hospital
  Information Systems in Resource-Limited Settings.* TFM, ETSETB-UPC — the companion thesis to this
  handbook.

## Institutional guidance this handbook builds on

- WHO, *Digital transformation handbook for primary health care* (2024) — the closest existing
  process guide; this handbook differs on scope (hospital, not PHC), named software, costing, and the
  non-state sector.
- WHO, *Digital Implementation Investment Guide* (2020) — programme-scale costing.
- WHO/ITU, *National eHealth Strategy Toolkit* (2012).
- WHO, *Monitoring and Evaluating Digital Health Interventions* (2016) — the five questions Bonet
  used in 2017 and this handbook still uses.
- Heeks, R. (2006), *Health information systems: failure, success and improvisation* — the
  design–reality gap behind [B-1](4-Instruments/B1-Readiness.md).
- Proctor, E. et al. (2011), *Outcomes for implementation research* — the eight outcomes behind
  [D-4](4-Instruments/D4-Exit-Gates.md).

## Software

- [Bahmni](https://www.bahmni.org/) · [GNU Health](https://www.gnuhealth.org/) ·
  [OpenMRS](https://openmrs.org/) · [KoBoToolbox](https://www.kobotoolbox.org/) ·
  [DHIS2](https://dhis2.org/) · [WireGuard](https://www.wireguard.com/) ·
  [Proxmox VE](https://www.proxmox.com/) · [Network UPS Tools](https://networkupstools.org/)
