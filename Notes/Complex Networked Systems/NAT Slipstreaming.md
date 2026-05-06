---
title: NAT Slipstreaming
aliases:
  - NAT Slipstreaming Attack
  - NAT Slipstreaming 2.0
tags:
  - cybersecurity
  - network-security
  - attacks
description: "Attack that bypasses NAT to remotely access TCP/UDP services on an internal victim machine via malicious JavaScript."
---

> "NAT Slipstreaming allows an attacker to remotely access any TCP/UDP service bound to a victim machine, bypassing the victim's NAT just by the victim visiting a website containing malicious JavaScript."
> Samy Kamkar

## Requirement

Presence of an **ALG (Application Layer Gateway)** proxy firewall. ALGs typically include extra features that allow many protocols by default, silently expanding the attack surface.

## Attack Steps (v1)

1. Victim visits a malicious website
2. Victim's private IP is extracted (via WebRTC or similar)
3. Malicious JavaScript forces the victim to submit a large POST request to the attacker's server, opening a connection in the [[Network Address Translation|NAT]] table. The packet is deliberately oversized, leading to packet fragmentation
4. The packet is crafted so that fragmentation produces two specific packets:
   - An ordinary HTTP packet
   - A packet opening a secondary connection to a vulnerable service (e.g. SIP on port 5060)
5. Some routers/NATs naively process both fragments as individual requests, even though they are segments of the same initial packet

The attacker tricks the NAT into opening a connection with a special protocol by exploiting ALG rules, as if the victim device initiated the service. The attacker can then send packets to and receive responses from any port or service on the victim's machine.

```
Victim ----[oversized POST]----> Attacker
              |
              fragments into:
              [HTTP packet]   ---> handled normally
              [SIP open conn] ---> ALG opens port 5060 mapping
              |
Attacker now reaches the victim on port 5060 directly
```

## NAT Slipstreaming 2.0

A later variant extends the attack:

- Steps 1-3 of v1 stay the same
- Exploits **H.323**, a VoIP protocol that allows **call forwarding**
- The attacker can trick the NAT into creating traversal mappings to any device on the same network as the victim
- Malicious H.323 packets sent "from" the victim can reference secondary IPs in the network (discovered by guessing or scanning), causing the NAT to add entries for any internal IP
- The attacker can directly address any discovered device, not just the original victim

## Mitigations

- Automatic removal or disabling of vulnerable ALGs
- Default blocking of ports used by vulnerable protocols (SIP, H.323, etc.)

## Related Concepts

- [[Network Address Translation]]: the mechanism being abused
- [[Firewall]]: ALG firewalls are the precondition for the attack
- [[Digital Perimeter Security]]: shows that NAT alone is not security
