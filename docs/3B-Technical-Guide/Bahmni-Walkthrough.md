# Using Bahmni: a walkthrough

**Produces:** a picture of what each member of staff sees, screen by screen, before you train anyone.
**Use it for:** training sessions, the handover pack ([L-1](../4-Instruments/L1-Handover-Pack.md)),
and checking a new installation against what was configured.

!!! note "What these screenshots are"

    One **test patient** followed through the **Phase 2** configuration (registration, clinical
    record, laboratory, pharmacy) on the test instance, October 2026. No hospital data appears.
    Phase 2 contains Phase 1; a Phase 1-only version will be added. Reasoning and status: thesis
    §8.3 and Appendix I.

!!! tip "Try it: the click-through"

    An interactive version of this page: choose your role (registration desk, doctor or nurse,
    laboratory, pharmacy) and Phase 1 or 2, then click through pictures of the real screens. Every
    numbered marker explains one button; the green one is what to press next. It works offline.

    [Open the click-through in a new tab](../assets/bahmni/walkthrough.html){ .md-button .md-button--primary target="_blank" }

<iframe src="../../assets/bahmni/walkthrough.html" title="Bahmni click-through" style="width:100%;height:900px;border:1px solid #d5e1e0;border-radius:8px"></iframe>

## 1 · Signing in

User name and password, then the **login location** — the user's unit. The location decides which
patients the worklists show. The home screen offers only what the user's **role** permits.

![Login](../assets/bahmni/p2_01_login.png){ width="48%" } ![Login location](../assets/bahmni/p2_02_login_location.png){ width="48%" }

| Emergency | Laboratory (adds OpenELIS) | Pharmacy (adds Odoo) |
|---|---|---|
| ![](../assets/bahmni/p2_03_home_emergency.png) | ![](../assets/bahmni/p2_04_home_laboratory.png) | ![](../assets/bahmni/p2_24_home_pharmacy.png) |

## 2 · Registration

Name, sex, age or date of birth, address — then **open a visit for the unit** that will see the
patient. The eight visit types are the eight units, so choosing the visit is choosing the unit.

![New patient](../assets/bahmni/p2_05_registration_new_patient.png){ width="64%" } ![Start visit by unit](../assets/bahmni/p2_06_start_visit_by_unit.png){ width="32%" }

## 3 · The clinical record

Each unit has a tab listing its patients with an open visit. The patient's dashboard summarises
allergies, vital signs, visits, treatments and laboratory results.

![Unit worklist](../assets/bahmni/p2_07_unit_worklist.png)
![Patient dashboard](../assets/bahmni/p2_08_patient_dashboard.png)

The consultation has four tabs: **Observations, Consultation, Orders, Medications**. Values outside
the normal range are flagged. Tests are ordered from panels grouped by sample type.

![Vitals with an abnormal flag](../assets/bahmni/p2_09_vitals_abnormal_flag.png){ width="48%" } ![Lab order](../assets/bahmni/p2_10_lab_order.png){ width="48%" }

Type part of a medicine's name; fill dose, frequency, route and duration; the total quantity is
calculated. **On Save**, the lab order goes to OpenELIS and the prescription to Odoo.

![Drug search](../assets/bahmni/p2_11_drug_search.png){ width="48%" } ![Prescription](../assets/bahmni/p2_12_prescription.png){ width="48%" }

## 4 · The laboratory (OpenELIS)

The technician's menu is reduced to what a technician uses. The day's status, result entry against
the order from Bahmni, validation — and the result appears in the patient's record.

![Today's status](../assets/bahmni/p2_13_openelis_today.png)
![Result entry](../assets/bahmni/p2_14_openelis_result_entry.png){ width="48%" } ![Validation](../assets/bahmni/p2_15_openelis_validation.png){ width="48%" }
![Results in the record](../assets/bahmni/p2_16_lab_results_in_record.png)

## 5 · The pharmacy (Odoo)

A page of three actions — **receive orders, dispense, check stock** — opens the matching Odoo
screen. The prescription arrives as an order marked *not yet dispensed*; **Dispense** confirms the
delivery and reduces the stock.

![Pharmacy page](../assets/bahmni/p2_17_pharmacy_launcher.png){ width="48%" } ![Medicine stock](../assets/bahmni/p2_20_odoo_medicine_stock.png){ width="48%" }
![Not yet dispensed](../assets/bahmni/p2_18_odoo_order_to_dispense.png){ width="48%" } ![Dispensed](../assets/bahmni/p2_19_odoo_dispensed.png){ width="48%" }

!!! warning "Not validated"

    The pharmacy page sits over Odoo, which could not be reduced far enough: Odoo's other functions
    remain one click away, and a pharmacist who strays into them reaches screens the training does
    not cover. Odoo also asks for its own sign-in. Test with the pharmacists, supervised, before
    relying on it (thesis §8.3.4, §10.1).

## 6 · Reports and help

Two Phase 2 reports (laboratory orders and results; prescriptions), each for a date range. A help
centre in English and French, served from the hospital's own network.

![Reports](../assets/bahmni/p2_21_reports.png)
![Help centre](../assets/bahmni/p2_22_help_centre.png){ width="70%" }
