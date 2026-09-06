---
hide:
  - toc
---

<div class="hb-hero" markdown>
<p class="hb-hero__eyebrow">AUCOOP · Field handbook · Version 0.3</p>
<h1 class="hb-hero__title">Putting a hospital information system into a hospital that runs on paper — and having it still be there when you come back.</h1>
<p class="hb-hero__lede">A practical guide for volunteer engineering teams who arrive for two or three weeks, install something, and fly home. Written from ten years of deployments in Ghana, Ethiopia, Sierra Leone and Cameroon — including the ones that did not work, and why.</p>
<p class="hb-hero__actions">
<a class="md-button md-button--primary" href="2-Story/">Read the story</a>
<a class="md-button" href="1-Introduction/1.2-Who-This-Is-For/">Who this is for</a>
<a class="md-button" href="4-Instruments/">Go to the instruments</a>
</p>
</div>

<div class="hb-stat" markdown>
<div><div class="hb-stat__n">10</div><div class="hb-stat__l">years of AUCOOP hospital deployments, four countries, five sites, 2016–2026</div></div>
<div><div class="hb-stat__n">1</div><div class="hb-stat__l">written handover in all that time. It was the one edition that got built on.</div></div>
<div><div class="hb-stat__n">14</div><div class="hb-stat__l">statutory returns, still handwritten four months after a full system was installed</div></div>
<div><div class="hb-stat__n">2 / 11</div><div class="hb-stat__l">digital forms carrying any data a year after a form-collection rollout</div></div>
</div>

## Five parts, five different questions

<div class="grid cards" markdown>

-   **The Story**

    ---

    *Why does this go wrong, and what actually causes it?*

    Twelve problems in the order a deployment meets them, each one titled the way you'd say it out
    loud. About an hour to read. This is the part to read before you travel.

    [:octicons-arrow-right-24: Start with chapter 1](2-Story/2.01-Last-Time-She-Came.md)

-   **The Organisational Guide**

    ---

    *How do I do the 80% that is not technical?*

    Eight recipes: the mandate, the six conversations, super-users, retiring paper, the support
    ladder, funding the owner, training, the handover.

    [:octicons-arrow-right-24: Start with the mandate](3A-Organisational-Guide/index.md)

-   **The Technical Guide**

    ---

    *How do I build the infrastructure and configure the software?*

    Assessment, power, network, server, remote access, platform choice, Bahmni, GNU Health, and what
    to pack.

    [:octicons-arrow-right-24: Browse the recipes](3B-Technical-Guide/index.md)

-   **The Instruments**

    ---

    *What do I have to produce?*

    Nine things you actually fill in, ordered by when — before you go, while you're there, the day
    you leave, once you're back.

    [:octicons-arrow-right-24: See the instruments](4-Instruments/index.md)

-   **Real Deployments**

    ---

    *What happened when someone tried?*

    Meki, Ada Foah, Lunsar and Yassa–Douala, written up honestly — including what nobody knows.
    And a template for adding yours.

    [:octicons-arrow-right-24: Read the case studies](5-Real-Deployments/index.md)

-   **Resources**

    ---

    *Where do I download the forms?*

    Every instrument as PDF and DOCX, the KoBo form for field capture, the companion repositories,
    and the prior work this builds on.

    [:octicons-arrow-right-24: Downloads](resources.md)

</div>

## What this handbook believes

**A hospital is not a network.** A misconfigured router means a slow page. A patient record attached
to the wrong identifier means someone can be given the wrong drug. Everything here is more cautious
than it would be for any other kind of infrastructure, on purpose.

**Adoption is the hard part, not installation.** Bahmni installs in a day. Getting a ward to stop
using its paper register is the work of a year, and it is where these projects actually fail. So this
handbook spends as much time on directors, nurses and handover as on servers.

**Doing less, properly, beats doing more, partially.** A form-collection tool a ward uses every day
is worth more than a full hospital information system abandoned three months after you fly home.
There is a whole chapter on how to decide to do less — and on when not to deploy at all.

**Write it down while you are standing there.** Ten years of this project's archive contain no
photograph of a paper form; the fourteen we now have were collected months later, by asking. The
hospital's bed capacity is still recorded three different ways in three different documents.

**This is a living book.** It is version 0.3 and it is wrong in places nobody has found yet. When
your project finds one, [say so](contributing/index.md). That is how the next team starts from
somewhere better than you did.

!!! note "The companion thesis"

    The reasoning, evidence and academic argument behind all of this live in *Methodological Guide
    for the Implementation of Open-Source Hospital Information Systems in Resource-Limited Settings*
    (UPC ETSETB, 2026). You do not need it to use this handbook. If you want to know *why* something
    is recommended rather than just what to do, that is where the answer is.

!!! tip "Networking is covered next door"

    AUCOOP's [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/)
    covers mesh, addressing, OpenWrt, monitoring, VPN and power in far more depth than we do. Where
    the two overlap, use theirs. This handbook covers what is different about a *hospital*.
