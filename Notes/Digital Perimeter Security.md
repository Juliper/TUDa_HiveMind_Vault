---
title: Digital Perimeter Security
aliases:
  - DPS
  - Network Perimeter Security
tags:
  - cybersecurity
  - network-security
description: "Set of software and hardware checkpoints used to protect networks and resources from unauthorized access."
---

**Digital Perimeter Security (DPS)** is the set of software and hardware checkpoints used to protect resources and networks from unauthorized access.

A typical perimeter combines several mechanisms working together:

- [[Firewall]]: filters traffic between two networks based on rules
- [[Intrusion Detection System]] (IDS/IPS): monitors or blocks malicious traffic
- [[Demilitarized Zone]] (DMZ): isolates client-facing services from the internal network
- [[Honeypot]]: decoys that lure attackers and detect intrusions

## Typical Architecture

```
Internal Network
  |
  Switch
  |
  Firewall (internal) -- DMZ (Webserver, DNS, Email)
  |
  Router
  |
  NAT
  |
  Firewall (external) -- Honeypot
  |
  Internet
```

The internal firewall protects the trusted network. The DMZ holds public-facing services. The external firewall faces the Internet. Honeypots can be placed alongside the perimeter to catch attackers that bypass other defenses.

## Related Concepts

- [[Defense in Depth]]: DPS implements layered defense at the network level
- [[Zero Trust Architecture]]: complementary model that does not rely on perimeter trust
- [[Network Address Translation]]: often part of the perimeter via NAT devices
