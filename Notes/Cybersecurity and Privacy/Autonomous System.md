---
title: Autonomous System
aliases:
  - AS
  - Autonomes System
  - ASN
tags:
  - network-security
  - routing
description: "A collection of IP prefixes owned and managed by a single entity, identified by a unique Autonomous System Number (ASN)"
draft: false
---

> [!NOTE] Definition
> An Autonomous System (AS) is a collection of IP network prefixes owned and managed by a single entity (e.g., an ISP, university, or corporation) that presents a common routing policy to the Internet.

Each AS is identified by a globally unique **Autonomous System Number (ASN)**, assigned by Regional Internet Registries (RIRs).

## How It Works

The Internet is organized as a network of interconnected ASes. Each AS controls its own internal routing but uses [[Border Gateway Protocol]] (BGP) to exchange reachability information with neighboring ASes via **BGP routers** at the edges.

### IP Address Distribution Hierarchy

IP addresses flow from IANA through a hierarchical delegation:

```mermaid
graph TD
    IANA["IANA<br/>Global IP Pool"] --> ARIN["ARIN<br/>North America"]
    IANA --> RIPE["RIPE NCC<br/>Europe/Middle East"]
    IANA --> APNIC["APNIC<br/>Asia-Pacific"]
    IANA --> LACNIC["LACNIC<br/>Latin America"]
    IANA --> AFRINIC["AFRINIC<br/>Africa"]
    RIPE --> AS1["AS (Child)<br/>e.g. 1.1.0.0/16"]
    RIPE --> AS2["AS (Child)<br/>e.g. 1.2.0.0/16"]
    AS2 --> AS3["AS (Grandchild)<br/>e.g. 1.2.1.0/24"]
```

The five **Regional Internet Registries (RIRs)** are responsible for managing and distributing IP addresses within their geographic areas.

## Example

TU Darmstadt operates its own AS with a unique ASN. It manages a set of IP prefixes and uses BGP to announce reachability of those prefixes to its upstream providers.

## Related Concepts

- [[Border Gateway Protocol]]: the protocol ASes use to exchange routing information
- [[Gao-Rexford Model]]: models business relationships between ASes
- [[Resource Public Key Infrastructure]]: cryptographically binds prefixes to their owning ASN
