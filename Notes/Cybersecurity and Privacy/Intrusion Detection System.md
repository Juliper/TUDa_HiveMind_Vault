---
title: Intrusion Detection System
aliases:
tags:
description: Systems that monitor (IDS) or actively block (IPS) malicious network traffic; combined with firewalls in NGFWs.
---

## Intrusion Detection System (IDS)

An **IDS** is a passive observer that monitors network traffic for patterns of malicious activity.

- Observes all incoming and outgoing network traffic
- **Not in-line** with the traffic flow, no latency added
- Computationally heavy
- Logs information and alerts admins on malicious activity

## Intrusion Prevention System (IPS)

An **IPS** actively analyzes network traffic in real-time and takes preventative measures to stop attacks.

- **In-line** with the traffic flow
- Actively blocks or drops malicious connections
- Alerts admins on malicious activity
- Introduces some latency

| Property | IDS | IPS |
|---|---|---|
| Position | Off-path (mirror) | In-line |
| Action | Detect and alert | Block and alert |
| Latency | None | Some |
| Risk on failure | Misses attacks | Drops legitimate traffic |

## Related Concepts

- [[Firewall]]: complementary access-control layer
- [[Honeypot]]: decoy system, often considered part of the IDS ecosystem
- [[Indicator of Compromise]]: IDS/IPS detection rules are often based on IoCs
