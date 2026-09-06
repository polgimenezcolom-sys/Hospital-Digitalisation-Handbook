---
stage: "While you are there"
---

# D-2 · Infrastructure audit

**When:** during the assessment visit.
**Produces:** the inputs for power, network and server dimensioning.

| Category | Items to assess |
|---|---|
| **Electricity** | Grid availability (hours/day); generator fuel type, capacity, runtime; solar installation if any; voltage stability measured with a multimeter over 24 h; outlet locations per building |
| **Internet** | ISP name and technology (fibre, 4G, VSAT); contracted bandwidth; actual measured bandwidth; carrier-grade NAT check — compare the router's WAN address against the public address; monthly cost |
| **Physical space** | Candidate server room — ventilation, security, access control; cable routing between buildings; distance between the farthest buildings; wall materials |
| **Existing IT** | Functional computers and tablets; operating systems; printers; existing network equipment; cabling |
| **Environment** | Temperature range; humidity; dust; insect and rodent risk; flooding risk |

!!! tip

    The carrier-grade NAT check takes five minutes and changes the whole remote-access architecture.
    Do it in the first week, not the last.
