---
stage: "While you are there"
---

# D-1 · Field data capture

**When:** throughout the visit, before leaving each building.
**Produces:** the record nobody can reconstruct from home.

!!! danger "Assume you will never be able to ask again"

    Eight years of this project's archive contain no photograph of a paper form. The fourteen that
    now exist were collected retroactively, months after anyone was last on site, by asking. The
    hospital's bed capacity is still recorded three different ways in three different documents.


## Download the form

<div class="grid cards hb-dl" markdown>

-   :material-file-pdf-box: **Print and fill in by hand**

    ---
    A4, hand-fillable, works with no power at the desk.

    [Download PDF](../forms/D1_Data_Capture_Sheet.pdf){ .md-button }

-   :material-file-word-box: **Fill in on a computer**

    ---
    Same layout, editable. Save it with the unit and date in the file name.

    [Download DOCX](../forms/D1_Data_Capture_Sheet.docx){ .md-button }

-   :material-cellphone: **On a phone, offline, with photos** *(recommended)*

    ---
    An XLSForm for KoBoToolbox. Upload it to a KoBo project, install KoboCollect, and every
    photograph lands already labelled with unit, form and date. Syncs when there is signal.

    [Download XLSForm](../forms/D1_Data_Capture_KoBo.xlsx){ .md-button .md-button--primary }

</div>

## Paper records

One clean photograph of every **blank** form, and one **completed** example, per unit.

| Group | Forms in use at Lunsar (July 2026 returns) |
|---|---|
| Statutory returns | Morbidity · IPD Morbidity · Bed State · Monthly Returns Mortality · Monthly Returns Surgical · Monthly Returns X-Ray |
| Clinical units | Emergency Department · Theatre · Dressing Cases · Laboratory (2 sheets) |
| Maternal and child | ANC · Safe Motherhood · Immunization Returns |

Separately captured: two pages of the patient booklet and the folder-ID card it carries.

For each form record: the unit, who fills it in, who receives it and by when, and how many are
completed per day or per month.

## Per unit

- [ ] Daily volume, **counted not estimated** — OPD visits, inpatient census, lab tests, deliveries
- [ ] Who fills the form, who signs it, where it goes next
- [ ] How the patient is identified at this point
- [ ] Power: measured voltage over 24 h, grid hours per day, generator runtime and fuel availability
- [ ] Network: is there a working link **in this room**, and measured latency with the real application
- [ ] A photograph of the room — outlets, cable routes, where a workstation could physically go

## Deployment record

Written on site, not from memory afterwards:

- [ ] Every access point: location, model, how it is powered
- [ ] Switches, routers, models, where they sit
- [ ] Cable routes and distances; anything crossing open ground
- [ ] Solar: panel count, orientation, rating; battery capacity and age
- [ ] UPS model and **measured** runtime under real load
- [ ] Server specification and physical location
- [ ] Every credential created — recorded for rotation, **never** in a shared document
