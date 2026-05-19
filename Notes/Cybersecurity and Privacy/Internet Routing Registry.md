---
title: Internet Routing Registry
aliases:
  - IRR
tags:
  - network-security
  - routing
description: "A network of public distributed databases where resource owners document their routing policies to help validate BGP announcements"
draft: false
---

> [!NOTE] Definition
> The Internet Routing Registry (IRR) is a network of public, distributed databases maintained by the Regional Internet Registries (RIRs) and other third parties, where resource owners document their routing policy information.

## How It Works

Resource owners register information in IRR databases including:

- **Origin ASN**: which AS is authorized to originate a prefix
- **AS/resource manager**: who manages the resources
- **Peering set**: with whom the AS peers
- **AS set**: customers and providers
- **Routing policy**: how routes should be propagated

[[Border Gateway Protocol|BGP]] routers can query IRR data to validate the contents of BGP announcements and verify that the announced origin AS matches the registered owner.

### Major IRR Databases

Multiple IRR databases exist, often mirroring each other:
- RIPE, APNIC, RADB, JPIRR, Level3, NTTCom, among others

## Limitations

> [!WARNING]
> IRR has significant reliability issues that limit its effectiveness.

- **No central authority** to check and validate database content
- **Conflicting data** across different IRR databases
- **Often outdated** because operators neglect to update entries
- Despite these flaws, it remains **very widely used**

Because IRR lacks strong authentication, hijackers can impersonate legitimate resource holders, making [[BGP Hijacking]] still possible even with IRR-based filtering.

## Related Concepts

- [[Border Gateway Protocol]]: the protocol whose announcements IRR helps validate
- [[Resource Public Key Infrastructure]]: the cryptographic successor that addresses IRR's trust issues
- [[Autonomous System]]: the entities whose routing policies are registered
