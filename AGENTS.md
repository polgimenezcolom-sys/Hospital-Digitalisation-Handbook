# AGENTS.md — Hospital Digitalisation Handbook

> Durable project memory for AI assistants working in this repository.
> Read this first, every session. When something here goes stale, update it.
> **Companion:** `HANDBOOK_BRIEF.md` in this folder is the long-form orientation. This file is the
> operating rules; that one is the reasoning.

## 1. What this repo is

The **Hospital Digitalisation Handbook** — the operational guide an AUCOOP volunteer team follows
when it goes to digitise a hospital in a resource-limited setting. It is the practical deliverable of
Pol Giménez Colom's master's thesis (UPC ETSETB, MSc Telecommunications Engineering).

MkDocs Material site, published to GitHub Pages at
`polgimenezcolom-sys.github.io/Hospital-Digitalisation-Handbook`.

**Three artefacts, three jobs — do not blur them:**

| | What it is | Lifespan |
|---|---|---|
| **The thesis** | The argued, evidenced investigation. *Why* the guide is shaped as it is. | Frozen at submission |
| **The handbook** (this repo) | The operational guide. Checklists, worksheets, procedures. | **Living** — edited by every future cohort |
| **The handover pack** | What a team leaves at the hospital. An *instrument inside* the handbook (L-1) | Produced fresh each trip |

**If you find yourself explaining *why* at length here, it belongs in the thesis. If you find
yourself writing a checklist in the thesis, it belongs here.**

## 2. The hypothesis this serves

> Volunteer-led HIS deployments in resource-limited settings fail not because the systems are
> technically inadequate but because of **discontinuity between implementing cohorts**: with no
> structured method to follow and no recorded account to inherit, each cohort begins from zero.
> Such projects therefore need a baseline guide — founded on the literature, on
> international-organisation guidance and on the association's own project record — that **carries a
> mechanism for its own revision**: a version, a named owner, and a return path from each cohort's
> experience into the next edition.

**The mechanism is part of the claim, not an implementation detail.** Bonet 2017 was already a
well-founded baseline guide and it sat unread in the university repository for nine years. A version
of this handbook that improves the prose and leaves the feedback loop unresolved has failed on its
own terms while looking finished.

**Priority order for any work here:** (1) the mechanism and open questions E1–E5, (2) the instruments
chapter, (3) everything else.

## 3. Current status (keep this current)

- **v0.3**, 56 pages, deployed. Nine instruments generated as DOCX + PDF.
- **Open and blocking v1.0:** E1 (B-1 score thresholds), **E2 (who merges A-1 returns, and how
  often — the most important)**, E3 (can A-1 attach to the CCD closure report?), E4 (internal or
  public?), E5 (long-term home). Tracked in `../TFM_Open_Questions.md`.
- **Known stale:** the technical guide still carries pre-audit figures. See `HANDBOOK_BRIEF.md`
  §7(4) for the eight exact corrections to propagate.

## 4. Status honesty — non-negotiable

Every document in this project has overstated progress at some point and every one has had to be
corrected. Do not add to the list.

- Bahmni: **Phase 1 designed.** Not deployed, not adopted. Phase 2 in design; the Odoo
  simplification is unresolved.
- GNU Health: **no phase achieved. On standby.** The interface simplification was *not achieved in
  the time available* — which is **not** the same as "impossible", and must not be written as such.
  A future team with a Python developer may succeed.
- **Design ≠ deployment ≠ adoption.** Three distinct claims. Say which one you are making, every
  time.

## 5. What the author actually did

- **Fieldwork:** Lunsar, Sierra Leone, **February–March 2026. One deployment, one site.**
- **Yassa–Douala, Cameroon (2026):** not visited. A questionnaire and the counterpart's written
  evaluation — a source, not a site.
- **Ghana 2016, Ethiopia 2017, Ghana 2019–20, Sierra Leone 2018–2025:** run by AUCOOP cohorts
  **before the author joined in 2025**. Read from the archive, as any researcher would.
- The author has never been to Ethiopia or Ghana.

**Standing wording:** *"the association's documentary record of deployments in Ghana, Ethiopia,
Sierra Leone and Cameroon between 2016 and 2026, and the author's own deployment at Lunsar in
February–March 2026."* Never "our deployments". Never "we found, over ten years". The design is
**archival analysis plus one case study** — defensible and unusual, but it collapses the moment
someone asks what Ada Foah was like.

## 6. Evidence rules

- **Two fabrications have already been caught in this project** — a journal reference in the thesis
  carrying the introduction's headline statistics, and several claims in a slide deck. Assume the
  next one is yours unless you check.
- **If a figure is not traceable** to a document in `../6_Past_Projects/`, `../8_Resources/`, or a
  cited source, say so in the text rather than asserting it.
- **Sourcing protocol**, the one that caught both fabrications: state what was *actually opened*.
  Mark `[FULL]` (body read), `[PAGE]` (landing page only), `[SNIPPET]` (search listing only). Return
  **"no citable source found"** rather than a plausible guess — a negative result is a useful answer
  and several are load-bearing in this project.
- Verified engineering sources and their explicit non-verified lists:
  `../2_Research/Analysis/Power_Sizing_Sources_Verification.md` and
  `Network_Sizing_Sources_Verification.md`.

## 7. Voice — three registers, kept distinct

The commonest failure mode is the whole handbook drifting into thesis prose. Do not let it.

| Part | Register |
|---|---|
| **2 · The Story** | Narrative, second person, specific. Real events. Never condescending. Each chapter ends at the instrument that would have prevented it |
| **3A/3B · The Guides** | Imperative and terse. Procedures, not reasoning |
| **4 · The Instruments** | Checkboxes and fields. Nothing else |
| **5 · Real Deployments** | Honest case studies, **including what failed**. A guide with no failures in it is not believed |

British English. No em-dash-heavy academic hedging in the Story or the Guides.

## 8. Build and layout

```
docs/1-Introduction/     docs/2-Story/       docs/3A-Organisational-Guide/
docs/3B-Technical-Guide/ docs/4-Instruments/ docs/5-Real-Deployments/
docs/forms/              generated — do not hand-edit
scripts/build_forms.py   generates the 9 DOCX + 9 PDF + the KoBo XLSForm
overrides/main.html      version banner, act/chapter eyebrow from front matter
docs/stylesheets/extra.css   AUCOOP navy #0b3583, stage badges, download cards
```

- Build: `mkdocs build --strict` (also runs in `.github/workflows/deploy.yml`).
- Forms: `python scripts/build_forms.py` — **bump `VERSION` in that file when you change them**.
- `mkdocs.yml` uses `navigation.sections` deliberately: it keeps the whole book visible in the
  sidebar on every page. An earlier drill-down config made the menu vanish inside chapters. Do not
  revert it.
- Story chapters carry `act:` / `chapter:` front matter used by the overrides template.

## 9. Housekeeping

- `aucoop_field_handbook.html` in the repo root is the **superseded** single-file first version.
  Archive or delete it — two artefacts claiming to be the handbook is precisely the drift problem
  this handbook is about.
- **Pushes happen from Pol's machine.** A sandboxed session can commit but cannot reach GitHub.
  Say so rather than reporting a push that did not happen.
- Anything that changes the published site is a correctness issue, not a cosmetic one: the live URL
  is what a volunteer reads.
