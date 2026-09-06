# Hospital Digitalisation Handbook

A practical guide to putting a hospital information system into a hospital that runs on paper — and
to it still being there when you come back.

---

This handbook is for volunteer engineering teams: students and professionals who arrive at a hospital
for two or three weeks, install something, and fly home. It was written inside
[AUCOOP](https://aucoop.upc.edu), a UPC student cooperation association, out of eight years of
deployments at St. John of God Hospital in Lunsar, Sierra Leone, and one at St. Jean de Dieu in
Yassa–Douala, Cameroon.

Some of those deployments worked. Several did not, and the ones that failed did not fail for
technical reasons.

<div class="grid cards" markdown>

-   __Start with the story__

    ---

    Twelve problems, in the order a deployment meets them. Each one explains what goes wrong and
    why it goes wrong. This is the part to read before you travel.

    [The Story of a Hospital That Runs on Paper](2-Story/index.md)

-   __Jump to a recipe__

    ---

    Step-by-step instructions for one task — sizing a UPS, configuring a phase, training a ward.
    Self-contained. Open the one you need.

    [The Guide](3-Guide/index.md)

-   __Fill in an instrument__

    ---

    The assessments, checklists and templates you actually complete: before you go, on site, and
    on the day you leave.

    [The Instruments](4-Instruments/index.md)

-   __Read what happened__

    ---

    Real deployments, written up honestly — including what went wrong and what we would do
    differently.

    [Real Deployments](5-Real-Deployments/index.md)

</div>

## The principles behind this handbook

**A hospital is not a network.** If a router is misconfigured, a page loads slowly. If a patient
record is attached to the wrong identifier, someone can be given the wrong drug. Everything in here
is more cautious than it would be for any other kind of infrastructure, and that is deliberate.

**Adoption is the hard part, not installation.** You can install Bahmni in a day. Getting a ward to
stop using its paper register is the work of a year, and it is where these projects actually fail. So
this handbook spends as much time on directors, nurses and handover as it does on servers.

**Doing less, properly, beats doing more, partially.** A form-collection tool that staff use every
day is worth more than a full hospital information system that is abandoned three months after you
fly home. There is a whole chapter on how to decide to do less — and on when not to deploy at all.

**Write it down while you are standing there.** Everything you do not record on site becomes a
question you cannot answer from Barcelona. Eight years of this project's archive contain no
photograph of a paper form; the fourteen we now have were collected retroactively, months later, by
asking. The bed capacity of the hospital is still recorded three different ways in three different
documents.

**This is a living book.** It is version 0.2 and it is wrong in places nobody has found yet. When
your project finds one of those places, [say so](contributing/index.md) — that is how the next team
starts from somewhere better than you did.

!!! note "The companion thesis"

    The reasoning, the evidence and the academic argument behind all of this live in
    *Methodological Guide for the Implementation of Open-Source Hospital Information Systems in
    Resource-Limited Settings* (UPC ETSETB, 2026). You do not need to read it to use this handbook.
    If you want to know *why* something is recommended rather than just what to do, that is where
    the answer is.

!!! tip "Networking is covered next door"

    AUCOOP's [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/)
    covers mesh, addressing, OpenWrt, monitoring, VPN and power in far more depth than we do. Where
    the two overlap, use theirs. This handbook covers what is different about a *hospital*.
