---
title: Firewall
aliases:
tags:
description: System of hardware/software components that restricts access between two networks based on rules.
---
A **firewall** is a system of hardware and/or software components designed to restrict access between two networks. It is part of the [[Digital Perimeter Security|defense perimeter]] designed to protect resources.

## What Firewalls Can Do

1. Monitor and filter network traffic
2. Log connections
3. Protect against unauthorized access
4. Help with regulation compliance

## What Firewalls Cannot Do

1. Protect against insider threats (traffic that originates inside the trusted zone)
2. Filter based on packet payloads (without deep packet inspection)

## Types of Firewalls

### Packet Filtering Firewalls

- Rely primarily on TCP/IP packet features and headers
- Apply a strict, ordered set of rules sequentially per packet until a match applies
- Rules consist of match conditions (Interface, Src/Dst IP, Proto, Src/Dst Port, ...) and an action (Accept, Drop)

#### Stateful Firewall

Filters ingress and outgoing traffic based on **active connections (sessions)**.

- Pre-defined security policy defining allowed sessions
- Keeps track of client-server connections
- Assigns all packets to one of the active sessions, otherwise drops

| Pro | Con |
|---|---|
| Easier to design | Resource heavy |
| Fewer rules needed | Expensive |
| More secure | |
| Smaller tables | |
#### Stateless Firewall

Filters ingress and egress traffic on a **per-packet basis**.

- No state information is generated or stored
- All policy nuances must be encoded directly in the rules table
- Communication flow tracked via the TCP/ACK flag (see [[TCP 3-Way Handshake]])

| Pro | Con |
|---|---|
| Lightweight | Complex to design |
| Cheap | Many more rules required |
| | Less secure / more porous |
| | Larger tables |

UDP is harder to handle: it has no ACK flag and no connection state.

### Proxy Firewall

**Application-specific** firewall that operates at the application layer.

- Protocol-specific
- Maintains connection state
- Can filter based on packet payloads (Deep Packet Inspection)
- Can also include rules based on IP/TCP/UDP packet headers

| Pro | Con |
|---|---|
| More secure than packet-filtering | Heavyweight / CPU-intensive |
| Easier audit of application traffic | Expensive |

A **Web Application Firewall (WAF)** is a type of proxy firewall designed to defend applications from app-specific attacks (e.g. SQL injection, XSS).

### Next Generation Firewall (NGFW)

Modern all-in-one solution that combines:

- Packet filtering and stateful inspection
- Deep packet inspection (proxy capabilities)
- [[Intrusion Detection System|IDS/IPS]] functionality

## Related Concepts

- [[Digital Perimeter Security]]: the broader perimeter the firewall is part of
- [[Intrusion Detection System]]: complementary monitoring layer
- [[TCP 3-Way Handshake]]: foundation for stateless filtering via the ACK flag
- [[Demilitarized Zone]]: typically separated from the internal network by firewalls
