# Remote support

!!! warning "Outline — not yet written"

**What this page will contain**

1. **Detecting carrier-grade NAT**, in five minutes, on site: compare the router's WAN address with
   what a public address service reports. If they differ, no inbound connection is possible and the
   architecture changes.
2. **The tunnel.** WireGuard from the hospital outward to a cheap VPS with a public address, held
   open. Full recipe in the
   [Community Network Handbook](https://aucoop.github.io/Community-Network-Handbook/3-Guide/VPN/) —
   link, do not duplicate.
3. **Monitoring**, so a failure is noticed by you rather than reported three weeks later.
4. **Credential handling.** Handed over in person, recorded for rotation, never in the runbook, the
   shared folder, or anything that could become a public appendix.
5. **The support ladder** — tier 0 in-product help, tier 1 on-site super-user, tier 2 external or
   commercial support, each with a name.

!!! danger "The trap"

    Remote access makes it easy to keep the system alive by doing the work yourself. That feels like
    support and it prevents ownership. Use it to help the hospital's own person fix something, not to
    fix it silently at midnight.

**Source material:** thesis Chapter 4, Phases 4 and 5.
