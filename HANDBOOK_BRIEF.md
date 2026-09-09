# The Handbook — what it is, why it exists, and how it is meant to work

*Briefing document, v1.1 · 2026-09-09 · Pol Giménez Colom, AUCOOP / UPC*

*v1.1 adds §0 (the hypothesis, settled 2026-09-07), corrects how the evidence base is described,
narrows the GNU Health claim, gives exact figures for the technical-guide sync, and adds §10 on
running the next working session.*

**Purpose of this file.** It is the orientation document for anyone — a person or an AI session —
picking up work on the *Hospital Digitalisation Handbook*. Attach it, the published handbook and the
thesis to a new conversation and this document should be enough to start from, without having to
reconstruct nine years of context first. Sections 5 and 6 are the ones to read if you only read two.

**Current state:** v0.3, 56 pages, deployed at
`polgimenezcolom-sys.github.io/Hospital-Digitalisation-Handbook`, built with MkDocs Material from
`10_Handbook/`. Nine instruments generated as DOCX and PDF by `scripts/build_forms.py`.

---

## 0. The hypothesis the handbook exists to serve

*Settled 2026-09-07. Everything else in this document follows from it. Full derivation in
`THESIS_BRIEF.md` §2b.*

> **Hypothesis.** The failure of volunteer-led hospital information system deployments in
> resource-limited settings — in AUCOOP's record, and plausibly in comparable organisations — is
> caused not by the technical inadequacy of the systems deployed, but by **discontinuity between
> implementing cohorts**: without a structured method to follow and a recorded account to inherit,
> each cohort begins from zero.
>
> **Proposition.** Such projects therefore require a **baseline guide** — founded on the literature,
> on international-organisation guidance, and on the association's own project record — setting out
> how a deployment is approached and what must be recorded at each step. And because a guide written
> once and deposited is precisely what has already failed here, that guide must itself carry a
> **mechanism for revision**: a version, a named owner, and a return path from each cohort's
> experience into the next edition.
>
> **Deliverable.** The handbook is that guide.

**Why this changes how the handbook should be worked on.** The mechanism is not an implementation
detail bolted onto a document — **it is part of the claim being made.** Bonet 2017 was already a
well-founded baseline guide and it was lost for nine years. If the next versions of this handbook
improve the prose and leave §6 unresolved, the handbook will have failed on its own terms while
looking finished.

So the priority order for the next versions is:

1. **The mechanism** (§6, and open questions E1–E5) — who owns it, where returns go, what cadence.
2. **The instruments chapter** (§5) — the argument for why fillable documents, which the handbook
   currently never makes.
3. Everything else.

That ordering is deliberate and should survive contact with the temptation to polish pages instead.

---

## 1. What it is, in one paragraph

The handbook is the **operational guide an AUCOOP volunteer team follows** when it goes to digitise a
hospital in a resource-limited setting. It is not a summary of the thesis and it is not documentation
for a piece of software. It is the distilled, practical form of an investigation — checklists,
decision rules, worksheets, procedures and worked examples — written so that a team of engineering
students with four weeks on site can do the work without repeating what four previous cohorts already
learned and lost.

**Three artefacts, three jobs. Keeping them distinct is the whole design.**

| | What it is | Where it lives | Lifespan |
|---|---|---|---|
| **The thesis** | The argued, evidenced, examined investigation. *Why* the guide is shaped as it is. | LaTeX → PDF → UPCommons | Frozen at submission |
| **The handbook** | The operational guide AUCOOP follows. Checklists, worksheets, calculators, procedures. | Git repo → versioned website + printable PDF | **Living.** Edited by every future cohort |
| **The handover pack** | What a team physically leaves at the hospital on its last day. | An *instrument inside the handbook* (L-1) | Produced fresh each trip |

The thesis **specifies, justifies and releases v1.0 of the handbook**. That is the contribution: the
artefact, plus the knowledge about it. The handbook then outlives the thesis, which is the point.

---

## 2. Why it exists — and why "another guide" is not the answer to nothing

The motivating problem is not that hospitals lack computers. It is that **a person's medical history
is unreachable at the moment it is needed** — a clinician facing a queue starts a returning patient
over from scratch because finding the paper folder costs twenty minutes they do not have.

But the handbook is not aimed at that problem directly. It is aimed at the *second* problem, which
the archive establishes far more damningly: **volunteer digitisation projects do not fail
technically. They fail at the seam between one cohort and the next.**

The evidence, all of it from AUCOOP's own record:

- **2016, Ada Foah, Ghana** — OpenMRS installed.
- **2017, Meki, Ethiopia** — Bonet's TFG deployed Bahmni and set out, in its own abstract, "to set a
  methodology in order to implement a medical record system" in rural health centres. Its
  requirements list included minimal-typing interfaces, offline operation, resilience to power cuts,
  staff able to maintain the system, and a phased rollout from registration to lab and pharmacy.
  **That is this handbook, nine years early.** The 2026 team did not know it existed until September
  2026, when it was found on the university's own repository.
- **2018, Lunsar, Sierra Leone** — the administrator asked for three things: stock control, finance
  compatible with their existing accounting software, and clinical history "because now it is
  impossible for them to get the information of every patient that has come before." The same report
  tabulated Odoo, GNU Health and OpenMRS with advantages, disadvantages and demo links.
- **2022–23** — KoboToolbox on tablets. A review in January 2024 found **2 of 11 forms carried any
  data**, all of it from two months.
- **2023–24** — more tablets, a Linux server, maintenance training **certified by a third party**.
  Adoption still did not follow. *Training is necessary and demonstrably insufficient — the handbook
  concedes this openly, and the argument is stronger for it.*
- **2024** — a 22-AP network designed remotely. Never deployed as designed. This cohort wrote **the
  only handover index in ten years**.
- **2025** — a ~28-node mesh built, Starlink uplink, fibre road crossing for lightning isolation.
- **2026** — Bahmni Phase 1 designed. Four months later, **every statutory monthly return the
  hospital submits was still being filled in by hand.**

Eight years later a different UPC team ran the same platform comparison and reached essentially the
same shortlist — the third time the association had chosen Bahmni.

**The pattern that matters:** two deployments died where no handover pack existed (RosarioSIS 2018;
KoboCollect 2023). Three were inherited and extended where one did (2024 → 2025 → 2026). Handover is
sporadic, not absent, and **it correlates exactly with survival.** That is the finding the handbook
is built on.

A small, concrete illustration of the same defect, found on 7 September 2026: the hospital's bed
count circulated in project documents in three inconsistent forms (25, 85, 100) across four cohorts
for eight years, while the correct figure — 85 — sat in a spreadsheet the hospital had been
maintaining the entire time. That number sets server sizing, switch port counts and UPS capacity.
Nobody had recorded where their figure came from, so nobody could check it. **That is D-1's entire
justification, stated from the project's own history.**

---

## 3. How it was built

**Sources, in order of weight:**

1. **The association's documentary record, 2016–2026** — closure reports, CCD funding forms,
   handover READMEs, TODO logs, network surveys, campus maps, 14 photographed statutory returns.
   Read end to end and analysed systematically. This is the evidence base nobody else has.

   ⚠️ **Say what this is, precisely, and never more.** These are projects run by AUCOOP cohorts
   **before the author joined in 2025**. The author's own fieldwork is **one deployment: Lunsar,
   February–March 2026**. Yassa–Douala was not visited — it is a questionnaire and the counterpart's
   written evaluation, a source rather than a site. The design is **archival analysis plus one case
   study**, which is defensible and unusual; a decade of participant observation is not what
   happened, and any sentence that lets a reader infer it collapses the moment someone asks what
   Ada Foah was like. Standing wording is in `THESIS_BRIEF.md` §7.2(2). This applies to the
   handbook's Part 5 case studies as much as to the thesis.
2. **Prior UPC and Spanish theses** — Bonet 2017, Rodríguez Trabal 2024, Badosa 2015, Berdún 2015,
   Luís Rodríguez 2018 and the wider repository sweep (`2_Research/Analysis/`).
3. **Primary interviews** — Luis Falcón (GNU Health), IntelliSOFT, IPLit Solutions. Nine transcripts.
4. **The implementation-science and health-informatics literature** — Heeks's design–reality gap
   (ITPOSMO), Proctor et al. 2011, NASSS, Normalisation Process Theory, HISP/DHIS2 scaling, WHO's
   2024 PHC digital transformation handbook.
5. **Deliberately not copied:** AUCOOP's own *Community Network Handbook*. Same organisation, same
   audience, adjacent domain — but the handbook was written to be substantially more complete and
   more explanatory than a checklist, because a guide nobody reads solves nothing.

**Method.** Action design research within an ongoing cooperation programme: the guide was drafted
from the archive, tested against two live deployments (Lunsar and Yassa–Douala), and is designed to
be revised by each subsequent cohort. It is explicitly **version 1 of an artefact plus a method for
improving it**, which is what makes the deferred phases a next cycle rather than a shortfall.

---

## 4. Architecture — five parts, and why each exists

| Part | Contains | Why it is separate |
|---|---|---|
| **1 · Introduction** | Motivation, audience, how to use it | Someone must be able to tell in ninety seconds whether this is for them |
| **2 · The Story** | 12 narrative chapters, each a real failure | **The part people actually read.** Every chapter is a thing that genuinely happened, told as narrative, ending in the instrument or procedure that would have prevented it |
| **3A · Organisational Guide** | Mandate, stakeholders, super-users, retiring paper, support ladder, funding the owner, training, handover | The 80 % that decides success. WHO's own framing. Kept **first**, before the technical guide, deliberately |
| **3B · Technical Guide** | Assessment, power, network, server, remote support, platform choice, Bahmni, GNU Health, packing list | The 20 %. Procedures only — the *reasoning* lives in the thesis |
| **4 · The Instruments** | Nine fillable documents | See §5 — this is the load-bearing part |
| **5 · Real Deployments** | Ada Foah, Meki, Lunsar, Yassa–Douala | Case studies written honestly, including what failed. A guide with no failures in it is not believable |

**The single most important structural decision** is that the organisational guide comes *before* the
technical guide, and that the Story comes before both. The thesis's core argument is that these
systems fail for organisational and economic reasons, not technical ones. A handbook that opened with
UPS sizing would contradict its own thesis on page one.

---

## 5. The instruments — why fill-in documents at all

*This is the chapter the handbook most needs and currently states only partially. What follows is
both a description of what exists and a specification of what the next version should say.*

### 5.1 Why documents, and not a wiki, a database or "good notes"

Because everything else has been tried in this project and none of it survived.

- **Free-form notes** were kept by most cohorts. They exist. They are unsearchable, they contradict
  each other, and the bed-count episode shows what happens: three numbers, no provenance, eight
  years.
- **A wiki or shared drive** requires an account, a network and a habit. Volunteers have a four-week
  window, intermittent connectivity, and no institutional login that outlives the trip.
- **A database** requires someone to maintain it between projects. There is nobody. That is the
  premise of the whole thesis.

A **numbered, printable, hand-fillable form** survives all three failure modes. It works with no
power at the desk. It can be photographed on a phone. It has a code short enough to say out loud —
*"has anyone finished D-1 for the pharmacy?"* is a question a team can ask each other in a corridor,
and that is a real design criterion, not a flourish.

### 5.2 The nine, and what each is for

**Before you go** — these decide whether to deploy at all, and at what level.

| Code | Instrument | Produces | The failure it prevents |
|---|---|---|---|
| **B-1** | Readiness assessment | A score for the gap between what the system assumes and what the hospital is | Deploying a level-4 system into a level-1 hospital. Operationalises Heeks's design–reality gap |
| **B-2** | Level decision | Which of four levels this deployment is — **or a decision not to deploy** | The commonest and most expensive error in the archive |
| **B-3** | Mandate and ownership | Named stakeholders and a written agreement | "Nobody told the nurses." A system with no institutional owner |

**While you are there** — these capture what cannot be reconstructed from Barcelona.

| Code | Instrument | Produces | The failure it prevents |
|---|---|---|---|
| **D-1** | Field data capture | The record you cannot rebuild from home — **with its source, not just its value** | The bed count. Eight years, three numbers, no provenance |
| **D-2** | Infrastructure audit | Power, network, space, existing IT, environment | Scoping a phase for a unit whose network cable was never actually run |
| **D-3** | Workflow mapping | The patient journey as it actually is, not as described | Digitising a process nobody follows |
| **D-4** | Phase exit gates | A defensible answer to "is this phase done?" | "Designed" being reported as "adopted" |

**Before you leave**

| Code | Instrument | Produces | The failure it prevents |
|---|---|---|---|
| **L-1** | Handover pack | What physically stays at the hospital | The two deployments that died. This is the instrument the evidence most directly supports |

**Once you are back**

| Code | Instrument | Produces | The failure it prevents |
|---|---|---|---|
| **A-1** | Debrief and feedback | What goes back into this handbook | The handbook silently going stale — the failure mode of every guide ever written, including Bonet 2017 |

### 5.3 The design constraints, which are constraints and not preferences

Every instrument was designed against the same five rules, each derived from an observed failure:

1. **Attach to something mandatory.** A new voluntary task will not be completed; an extension of an
   obligatory one will. A-1 is designed to ride on the CCD closure report the team already has to
   write. *(Whether CCD's format can be extended is still open — see §8.)*
2. **Complete it in the field, before you fly.** People land and stop. This is not cynicism; it is
   the observed behaviour of every cohort in the archive.
3. **Under two hours in total, all nine.** A half-filled form is worse than none, because it looks
   like data.
4. **Hand-fillable on paper.** No power, no login, no connectivity assumed at the moment of use.
5. **One named person merges the returns**, on a fixed cadence. Without this the handbook forks. It
   has already happened once, to the project's own control document.

A sixth rule is implicit and worth stating explicitly in the next version: **a skipped instrument is
a finding about the handbook, not a failure of the team.** A-1 asks which instruments were skipped
and why, and treats the answer as evidence that the instrument was too long, unclear, or wrong.

### 5.4 What the instruments deliberately do *not* do

They do not attempt to capture clinical data, and they are not a project-management system. They
capture exactly the information that (a) can only be obtained on site, and (b) the next cohort will
otherwise have to rediscover. Everything else is out of scope on purpose, because scope is what kills
forms.

---

## 6. The feedback loop — where the completed documents go

*This is the part the handbook currently under-specifies, and it is the part on which the whole
obsolescence argument depends. What follows is a proposal to be settled before v1.0.*

### 6.1 The mechanism

```
    ┌─ Before departure ────────────────────────────────────────────┐
    │  Team reads the previous project's completed D-1/D-2/D-3      │
    │  from the archive repo, plus the current handbook version     │
    └───────────────────────────────┬───────────────────────────────┘
                                    ▼
    ┌─ On site ─────────────────────────────────────────────────────┐
    │  B-1, B-2, B-3 completed and signed before deployment starts  │
    │  D-1 … D-4 completed as the work proceeds                     │
    │  L-1 assembled and physically left at the hospital            │
    └───────────────────────────────┬───────────────────────────────┘
                                    ▼
    ┌─ Before flying home ──────────────────────────────────────────┐
    │  A-1 drafted in the field. Scans/photos of every completed    │
    │  instrument taken before departure.                           │
    └───────────────────────────────┬───────────────────────────────┘
                                    ▼
    ┌─ Within two weeks ────────────────────────────────────────────┐
    │  Completed instruments deposited in the project archive       │
    │  A-1 filed as an issue against the handbook repository        │
    └───────────────────────────────┬───────────────────────────────┘
                                    ▼
    ┌─ Once per project cycle ──────────────────────────────────────┐
    │  The named maintainer merges A-1 returns, bumps the version,  │
    │  and publishes. Case study added to Part 5.                   │
    └───────────────────────────────────────────────────────────────┘
```

### 6.2 Where things are deposited — the proposal

**Two destinations, because the two kinds of output have different audiences.**

**Completed instruments** go to the project archive, in a per-project folder under a fixed naming
convention, alongside the existing structure in `6_Past_Projects/`:

```
<YEAR>_<COUNTRY>/Instruments/
    B1_Readiness_<site>_<YYYY-MM-DD>.pdf
    B2_Level_Decision_<site>_<YYYY-MM-DD>.pdf
    ...
    L1_Handover_Pack_<site>_<YYYY-MM-DD>.pdf
```

They are **evidence**, not guidance. They are never edited after deposit. The next team reads them;
it does not change them.

**A-1 debriefs** go to the handbook repository as **GitHub issues**, one per project, using a fixed
template. This is deliberate: an issue is public within the association, has a thread, cannot be
silently lost in a drive, and creates a visible queue of unmerged feedback that shames the
maintainer into acting. A document in a folder does none of those things.

### 6.3 Versioning, and the citation rule

The handbook carries a semantic version, displayed on every page. **A-1's first question is "which
handbook version did you follow?"** — and that single question is what makes the loop auditable. A
finding against v0.3 can be checked against v0.3's text; a finding against "the handbook" cannot.

Each case study in Part 5 records the version the team followed. Over time this produces something no
previous cohort had: **a traceable line from a failure on site to the paragraph that failed to
prevent it.**

### 6.4 How this actually changes the next project

The mechanism is worth stating plainly, because it is the answer to "why does this solve anything":

1. **The next team starts from evidence, not from zero.** They read the previous D-1/D-2/D-3 before
   they buy a plane ticket. The bed count is settled once, with its source recorded, and never
   rediscovered.
2. **The stop rule is applied before money is spent.** B-1 and B-2 are completed *before departure*.
   By the handbook's own level criteria, Lunsar in 2026 qualified for level 1 or 2 — no paid IT post,
   no funded owner, no support contract — and a level-4 system was deployed. The engineering was
   careful. There was simply no instrument at the time that made the mismatch visible before the
   decision.
3. **"Done" becomes a claim that can be checked.** D-4's exit gates force design, deployment and
   adoption to be three distinct claims. The archive's central ambiguity — installed versus
   implemented versus used — becomes impossible to fudge.
4. **The handbook improves rather than ages.** Every project returns an A-1. The guide gets more
   accurate with each cohort instead of decaying into a document that describes a hospital that no
   longer exists.

### 6.5 Why this specifically answers the obsolescence problem

Bonet 2017 is the proof of the negative case. It was a good methodology, it identified the right
preconditions, and it was **lost for nine years** — sitting in the university's own repository,
invisible because it was a static document with no mechanism for anyone to find it, follow it, or
correct it. It aged into irrelevance without ever being wrong.

The handbook is built to fail differently, in four ways:

- **It has a version, so it can be cited and superseded** rather than silently replaced.
- **It has a named owner and a cadence**, so staleness is somebody's responsibility rather than
  nobody's.
- **It has a return path**, so contact with reality flows back into the text instead of evaporating
  when the cohort graduates.
- **It lives where the work lives** — a git repository the deployment teams already use — rather than
  in a repository nobody searches. *(And note R28: UPCommons cannot find the string "Bahmni" at all.
  Its index covers metadata, not full text. The thesis's own failure mode, reproduced by the
  institution meant to preserve it.)*

A guide that is followed, corrected and re-published each year is not the same kind of object as a
guide that is written once and deposited. **That difference is the contribution** — not the
checklists themselves, which any competent team could write.

---

## 7. What I would change in the next version

Working through the above surfaced five things:

1. **Part 4 needs the chapter this document's §5 and §6 sketch.** At present the instruments index
   lists what each produces but never argues *why fillable documents*, never states the design
   constraints as a set, and never specifies the deposit mechanism. That is the handbook's biggest
   structural gap.
2. **A-1 is the keystone and is presented as the last item.** Consider promoting the feedback loop to
   its own short part, or into the introduction — a reader who stops before Part 4 currently never
   learns that the handbook is meant to be edited by them.
3. **B-1's thresholds are still unset** (open question E1). They should be derived by scoring Lunsar
   and Yassa–Douala retrospectively, where the outcomes are known, rather than chosen a priori.
4. **The technical guide still carries pre-audit figures.** Every calculation in the thesis was
   audited and sourced on 7 September; `docs/3B-Technical-Guide/Power.md`, `Network.md` and
   `Server.md` have not been synced. The exact changes to propagate:

   | Was | Now | Why |
   |---|---|---|
   | Autonomy 1–2 days | **3 days** | AS/NZS 4509.2: 4–5 with no generator, 2–3 manual start. One day blacked out in 28 of 28 modelled years |
   | Peak sun hours 4–5.5 (annual avg) | **4.0** (August worst month) | Stand-alone systems are sized on the critical design month. Lunsar's is August, at 3.8–4.3 |
   | Power factor 0.8 | **0.95** | No source supports 0.8 for modern IT loads; ENERGY STAR requires ≥0.95 for servers |
   | UPS sized on total load | **Critical load only** (204 W, not 652 W) | Laptops hold their own charge |
   | UPS specified by VA | **VA *and* Wh, separately** | Rating and runtime are independent constraints. A 600 VA unit passes the rating and stores a third of the energy needed |
   | PoE budget = Σ PD input × 1.25 | **Σ PSE per-port figures** | The standard already allows 18–26 % for cable loss; ×1.25 counts it twice |
   | 2–5 Mbps per workstation | **0.5 Mbps** | Unsourced and an order of magnitude high. DHIS2 gives 80 kbit/s per client |
   | (not stated) | **A Pi-class server cannot run Bahmni** | Below its published 8 GB / 500 GB minimum on both counts. Fine for GNU Health |

   Sources and what could *not* be verified: `2_Research/Analysis/Power_Sizing_Sources_Verification.md`
   and `Network_Sizing_Sources_Verification.md`.

6. **Narrow the GNU Health claim in `docs/3B-Technical-Guide/GNU-Health.md`.** It currently reads
   that the interface "could not be simplified". That is stronger than the evidence supports and
   stronger than the thesis now claims. It was **not achieved within the time available**, which is
   a different statement. The defensible form is about the kind of work each platform demands:

   > In Bahmni, interface simplification is a **configuration** activity. In GNU Health it is a
   > **development** activity — GNU Health's own documentation routes view customisation through
   > writing a `z_health_<name>` Python module.

   Four independent sources support that framing (GNU Health's documentation, Purkayastha 2019,
   Badosa 2015, Mpassy 2020); none supports "impossible". Volunteers reading this page need the
   distinction, because a future team with a Python developer may well succeed where this one did
   not — and the handbook should tell them that rather than closing the door.

7. **Part 5's case studies should each name the handbook version** they are written against, per
   §6.3. Retrofitting this now costs nothing and is impossible to add later.

8. **`aucoop_field_handbook.html` (45 KB, repo root) is the superseded single-file first version.**
   Archive or delete it. Two artefacts claiming to be the handbook is exactly the drift problem the
   handbook is about.

---

## 8. Open questions that block v1.0

| | Question | Why it blocks |
|---|---|---|
| **E1** | B-1's score thresholds — what total maps to which level? | The level model is the stop rule, and the stop rule is the handbook's first substantive claim |
| **E2** | **Who merges the A-1 returns, and how often?** | Without a named owner and a cadence there will be three handbooks within two years and none canonical. This has already happened once to the control document |
| **E3** | Can the A-1 return genuinely be attached to the CCD closure report? Is that format fixed by CCD, or can AUCOOP extend it? | Design constraint 1 in §5.3 depends on it. If it cannot be extended, the feedback loop needs a different mandatory host |
| **E4** | Is the handbook AUCOOP-internal or public from the start? | Changes the tone, and changes what can go in it — credentials, hospital-identifying detail, the counterpart's letter |
| **E5** | Where does it live long-term — its own repo, or inside a deployment repo? | It needs a home that survives its author |

**E2 is the one that matters most.** Everything in §6 is mechanism; without a named human on a
calendar, the mechanism is decoration.

---

## 9. If you are an AI session picking this up

- **Read first:** this file, then `docs/1-Introduction/1.1-Motivation.md`, then
  `docs/4-Instruments/index.md`, then one Story chapter to get the register.
- **The register matters.** The Story chapters are narrative, second person, specific, and never
  condescending. The guides are imperative and terse. The instruments are checkboxes. Do not
  homogenise them.
- **Facts come from the archive, not from plausibility.** Two fabrications have already been caught
  in this project — a journal reference in the thesis, and several claims in a slide deck. If a
  figure is not traceable to a document in `6_Past_Projects/`, `8_Resources/` or a cited source, say
  so in the text rather than asserting it.
- **Status honesty is non-negotiable.** Bahmni Phase 1 is *designed*, not adopted. GNU Health has
  achieved *no* phase and is on standby. Every document in this project overstated progress at some
  point and every one of them had to be corrected.
- **Build:** `mkdocs build --strict` via the GitHub Actions workflow in `.github/workflows/`. Forms
  regenerate with `python scripts/build_forms.py` — bump `VERSION` when you change them.
- **The thesis is the source of reasoning; the handbook is the source of procedure.** If you find
  yourself explaining *why* at length in the handbook, it probably belongs in the thesis, and vice
  versa.

---

## 10. Running the next working session

### What to attach

**Essential — attach all four:**

| File | Why |
|---|---|
| `10_Handbook/HANDBOOK_BRIEF.md` | This file. The orientation |
| `THESIS_BRIEF.md` | The hypothesis (§2b), the standing wording on participation (§7.2(2)), and the structure the handbook must stay consistent with |
| The handbook itself | The whole `10_Handbook/` folder if the session has folder access; otherwise the published site URL |
| `TFM_Open_Questions.md` | E1–E5 are the blockers. Everything in §6 above is mechanism until E2 has a name in it |

**Attach if the session will touch the technical guide:**
`2_Research/Analysis/Power_Sizing_Sources_Verification.md` and `Network_Sizing_Sources_Verification.md`
— they carry the corrected figures in §7(4) *and* the explicit list of what could not be verified.

**Do not attach the whole `6_Past_Projects/` folder.** It is large, and the analysis has already been
done: `2_Research/Analysis/Archive_Analysis_2023-2026.md` and `Past_Projects_Analysis.md` are the
distillations. Pull individual PDFs only when a specific claim needs checking.

### Agents

There is no handbook agent yet. The existing definitions live in
`4_Deployment/aucoop-gnuhealth-deployment/claude/agents/` and only two are relevant:

- **`researcher`** — for sourcing claims. Give it the honesty protocol that produced the two
  verification memos: state what was actually opened, mark `[FULL]` / `[PAGE]` / `[SNIPPET]`, and
  return "no citable source found" rather than a plausible guess. That instruction is why two
  fabrications were caught rather than published.
- **`reviewer`** — for checking a draft page against the archive before it is committed.

**`thesis-writer` is the wrong voice for the handbook.** Its register is academic; the handbook's
Story chapters are narrative and second person, the guides are imperative and terse, and the
instruments are checkboxes. **Worth creating a `handbook-writer` agent** with those three registers
written into it — it is ten minutes and it prevents the most likely failure mode, which is the whole
handbook drifting into thesis prose.

### Two housekeeping items for the new session

- **`10_Handbook/` has no `AGENTS.md`**, though the project convention is that every repo has one.
  Worth writing early: build commands, the three registers, the status-honesty rule, and the
  instruction never to assert a figure that is not traceable to the archive or a cited source.
- **Two handbook files are still uncommitted** in the working tree (`GNU-Health.md`,
  `5.2-Lunsar.md`). Commit and push before starting, or the session will be working against a
  version that differs from the live site.

### A suggested opening

> I'm working on the Hospital Digitalisation Handbook — the practical guide that comes out of my
> TFM. `HANDBOOK_BRIEF.md` is the orientation; read it and `THESIS_BRIEF.md` §2b first.
>
> The handbook is at v0.3 and deployed. I want to get it to v1.0. Per §0 of the brief the priority
> order is: (1) the feedback mechanism, (2) the instruments chapter, (3) everything else — because
> the mechanism is part of the thesis's claim, not a detail. A guide without it is exactly what
> already failed here once.
>
> Start by asking me the questions in §8 that you need answered — particularly E2, who merges the
> feedback returns and how often — and then propose a plan for v0.4. Don't write pages yet.

The last line matters. The strong temptation in a handbook session is to start producing polished
pages, which is satisfying and leaves the actual blockers untouched.
