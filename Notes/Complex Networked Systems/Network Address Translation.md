---
title: Network Address Translation
aliases:
  - NAT
  - PAT
  - NAT64
tags:
  - networking
  - cybersecurity
description: "Method that maps local IP addresses to globally routable IP addresses."
---

**Network Address Translation (NAT)** is a method that maps local IP addresses to a set of globally routable IP addresses.

## Purposes

1. Address [[IP Addressing|IPv4]] scarcity and depletion
2. Conceal internal IPv4 addresses
3. Enable communication between devices using incompatible IP protocols (e.g. IPv6 and IPv4)

## Types

| Type | Mapping |
|---|---|
| **Static NAT** | Every internal IP is permanently mapped to a unique public IP |
| **Dynamic NAT** | Internal IPs are assigned random public IPs from a pool |
| **Port Address Translation (PAT)** | Multiple internal IPs share a single public IP, distinguished by unique source port numbers per session |
| **NAT64** | Allows devices on an IPv6-only network to communicate with IPv4-only services |

> **Identifying types from a NAT table:** if all rows share the same public IP but differ by port, it is PAT. If the public IPs vary, it is dynamic NAT. If each internal IP always maps to the same public IP, it is static NAT.

## Benefits

- Save money on IP address licenses; extend IPv4 lifespan
- Mask internal network structure
- Decrease attack surface

## Disadvantages

- Breaks end-to-end connectivity (a core Internet design principle)
- Single point of failure
- Increased latency and configuration complexity

## Security Considerations

NAT was not designed as a security mechanism, but it does provide some implicit protection by hiding internal addresses. This protection is fragile: see [[NAT Slipstreaming]] for an attack that bypasses NAT entirely from an outside attacker.

## Related Concepts

- [[IP Addressing]]: NAT relies on private (non-routable) ranges from CIDR
- [[NAT Slipstreaming]]: attack that exploits NAT/ALG behavior
- [[Digital Perimeter Security]]: NAT devices are typically part of the perimeter
