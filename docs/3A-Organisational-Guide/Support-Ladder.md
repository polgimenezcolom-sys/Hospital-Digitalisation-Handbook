# Building the support ladder

**Produces:** the written answer to *"what does someone do when they get stuck?"* — three tiers, each
with a real name and a real route.
**When:** designed in week two; written into the handover pack before you leave.
**Instrument:** [L-1](../4-Instruments/L1-Handover-Pack.md), section 3.

## Why

A nurse hits a problem she cannot solve. What does she do?

If the honest answer is *"message a volunteer in Spain and hope"*, the system works only while that
volunteer is interested — which is not five years. If the honest answer is *"nothing, she goes back
to the book"*, you have read [*"They're doing both now"*](../2-Story/2.08-Doing-Both.md) and know
how that ends.

The ladder is the designed answer. It exists on paper, it has names, and it is in the handover pack.

## The tiers

**Tier 0 — self-help, in the product.**
Short, task-focused help pages, reachable from where the person is working, that work offline. Not a
PDF on a shared drive. At Lunsar this is the in-product Help Center served from the Bahmni
configuration itself — a home tile, bookmarkable, bilingual, with a page per task and an error
reference. Build tier 0 as part of configuration, not afterwards.

**Tier 1 — on site: the hospital's IT staff and the super-users.**
The hospital's own technician for first-line problems, and one or two [named people](Super-Users.md)
in the units who answer nine questions in ten. With time allowance. Reachable across shifts.

**Tier 2 — your organisation, remotely.**
Configuration problems, diagnosed through the VPN, for a defined period — then talked through with
tier 1 rather than fixed silently.

**Tier 3 — a contracted implementer.**
Where the hospital can fund it, a firm that supports Bahmni professionally, under a **service-level
agreement**, for upgrades and defects that need development. Firms consulted for this work quoted
US$25–30 an hour, and work on one-time, milestone-based payments with maintenance under an agreement
(companion thesis §8.3.2, §8.5). That costs money. Being able to name the cost is more useful to the hospital than pretending it is free,
because it is the number the board needs to decide whether to keep the system.

## Steps

1. **Write the five most likely failures** and the first thing to try for each. The server does not
   respond. The screen is blank. Nobody can log in. The report is empty. The printer does nothing.
   Add: *"the system takes 3–12 minutes to start after a restart — do not panic before then."*
2. **Put that sheet where the failure happens.** Laminated, next to the workstation. This is tier 0 in
   its most basic form and it will be used more than anything else you write.
3. **Name tier 1.** Super-users, contact route, shifts covered.
4. **Define tier 2 honestly.** What your organisation will answer, by what channel, for how long — and
   when that ends. Then find out what commercial support would cost and write the number down.
5. **Define escalation.** Tier 1 tries the sheet; if that fails, tier 1 contacts tier 2 with *these*
   three pieces of information (what was being done, what the screen said, what was tried). Simple.
   Written.
6. **Set up monitoring so tier 2 finds out before tier 1 has to tell them.** An uptime check that
   messages you. Three weeks of silent downtime is a much worse problem than an hour.
7. **Write the whole ladder into the handover pack.**

## The trap

Remote access makes it easy to keep the system alive by fixing things yourself from Barcelona at
midnight. That feels like support. It prevents ownership.

Use remote access to *diagnose*, then talk tier 1 through the fix. Every silent midnight repair is one
step further from the system being theirs.

## What goes wrong

**Tier 2 is a person, not a role.** "Message Pol" works until Pol graduates. Name a channel the
organisation owns.

**Tier 0 is a 40-page manual.** Nobody opens it. Five failures, one page, laminated.

**No end date on tier 2.** Your organisation's support quietly becomes permanent, unfunded, and
resented on both sides. Write the end date; renew it deliberately if you want to.
