# Remote support

**Produces:** a tunnel that works through carrier-grade NAT, monitoring that tells you before the
hospital does, and credentials nobody has to write down.

## Step 1 — diagnose CGNAT, on site, in five minutes

Compare the WAN address on the router's status page with what a public "what is my IP" service shows.
**Different means carrier-grade NAT**: the ISP has given the hospital a private address in the
100.64.0.0/10 range and shares one public address among many customers.

Consequences: port forwarding does nothing; dynamic DNS is useless; a VPN *server* at the hospital
is impossible. Every plan that involves connecting *inwards* is dead. Check this in week one.

## Step 2 — hub-and-spoke WireGuard

All connections go **outwards** from the hospital to a rented server with a real public address, and
stay open. You connect to the same server. Now you and the hospital are on one network.

- **Hub:** a VPS (Hetzner, Contabo, OVH — 3–5 €/month) with a static public IPv4, running WireGuard.
- **Spoke 1:** the hospital server, holding a persistent tunnel open with `PersistentKeepalive = 20`.
- **Spokes 2…n:** engineers' laptops.

Addressing: VPN subnet `100.101.219.0/24`; hub `.1`; hospital `.2`; engineers from `.10`; hospital
LAN `192.168.1.0/24` routed through.

**Hub — `/etc/wireguard/wg0.conf`:**

```ini
[Interface]
Address    = 100.101.219.1/24
ListenPort = 443
PrivateKey = <VPS_PRIVATE_KEY>
PostUp     = iptables -A FORWARD -i wg0 -j ACCEPT
PostDown   = iptables -D FORWARD -i wg0 -j ACCEPT

[Peer]  # hospital server
PublicKey  = <HOSPITAL_PUBLIC_KEY>
AllowedIPs = 100.101.219.2/32, 192.168.1.0/24

[Peer]  # engineer
PublicKey  = <ENGINEER_PUBLIC_KEY>
AllowedIPs = 100.101.219.10/32
```

**Hospital spoke — `/etc/wireguard/wg0.conf`:**

```ini
[Interface]
Address    = 100.101.219.2/32
PrivateKey = <HOSPITAL_PRIVATE_KEY>
MTU        = 1420
DNS        = 100.101.219.1

[Peer]
PublicKey           = <VPS_PUBLIC_KEY>
AllowedIPs          = 100.101.219.0/24
Endpoint            = <VPS_PUBLIC_IP>:443
PersistentKeepalive = 20
```

Why these choices: **port 443** so restrictive ISPs do not filter it; **keepalive 20 s** so the CGNAT
gateway does not drop the mapping; **split tunnel** — only VPN traffic goes through, the hospital's
scarce bandwidth stays for clinical use; **MTU 1420** to avoid fragmentation.

Set it up **during the deployment**. Two hours on site; impossible from home.

## Step 3 — keys and revocation

Each peer generates its own key pair locally — `wg genkey | tee privatekey | wg pubkey > publickey` —
and private keys never travel. When someone leaves or loses a laptop, remove their public key from
the hub and restart (`systemctl restart wg-quick@wg0`). VPS firewall: only UDP 443 and SSH with
key-based auth.

## Step 4 — monitoring

On the VPS, every five minutes:

```bash
#!/bin/bash
HOSPITAL=100.101.219.2
if ! ping -c 3 -W 5 $HOSPITAL >/dev/null 2>&1; then
  curl -s "https://api.telegram.org/bot<TOKEN>/sendMessage" \
       -d "chat_id=<CHAT_ID>" -d "text=ALERT: hospital tunnel DOWN $(date)"
fi
```

Three weeks of silent downtime is a far worse problem than an hour. In February 2026 a remote check
found the Lunsar server inactive; there is one line about it in the archive and no record of what
happened next. Monitoring exists so that line has a follow-up.

## Step 5 — credentials

You will create many: server, database, application admin, VPN keys, router. All still in use in
three years.

!!! danger "Never in writing"

    Not in the runbook. Not in the shared project folder. Not in a document that could become a thesis
    appendix or a public repository. This project found plaintext passwords and private keys spread
    across ten years of files in a cloud-synced folder that fed document appendices.

    Hand them over in person, separately. Record in the handover pack *that* they exist and *who*
    holds them — never the values. Rotate them when a team leaves.

## The trap

Remote access makes it easy to keep the system alive yourself from Barcelona at midnight. That feels
like support. It prevents the hospital from ever owning the system, and it lasts exactly as long as
you personally stay interested.

Diagnose remotely; then talk the [super-user](../3A-Organisational-Guide/Super-Users.md) through the
fix.

!!! tip "In depth"

    [Community Network Handbook — VPN](https://aucoop.github.io/Community-Network-Handbook/3-Guide/VPN/) has the full recipe including Netmaker
    for managing keys across many devices, and [Zabbix](https://aucoop.github.io/Community-Network-Handbook/3-Guide/Zabbix/) for monitoring at
    scale.
