# Server and backup

!!! warning "Outline — not yet written"

**What this page will contain**

1. Hardware selection and sizing for a small hospital — and why a mini-PC is usually the right answer
   rather than a rack server.
2. Operating system and virtualisation.
3. Redundancy: what is worth duplicating and what is not, at this scale.
4. **Backup and restore.** The section that matters. A backup that has never been restored is a
   belief, not a backup — the procedure must be demonstrated by the hospital's own owner before the
   team leaves.
5. Physical siting: ventilation, security, dust, who has a key.

!!! tip "Expect a slow start"

    Bahmni's OpenMRS container takes **3–12 minutes** to become healthy after a restart, and a
    rebuild with a large search index has been observed to take around 26 minutes. Do not diagnose a
    failed boot before then — and make sure this is written in the handover pack, because someone
    will restart it at 8 a.m. and panic at 8:04.

**Source material:** thesis Chapter 4, Phase 3 (Server Infrastructure).
