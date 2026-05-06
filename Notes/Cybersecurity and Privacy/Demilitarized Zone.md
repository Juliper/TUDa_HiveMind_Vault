---
title: Demilitarized Zone
aliases:
  - DMZ
tags:
description: Subnetwork that protects an organization's intranet from untrusted external networks.
---

A **Demilitarized Zone (DMZ)** is a subnetwork that protects an organization's intranet from untrusted external networks.

- Implements network segmentation as an extra layer of security
- Acts as a barrier between trusted and untrusted networks

## Architectures

### Single Firewall Architecture

- One firewall with multiple network interfaces
- Handles all traffic (Internet, DMZ, internal)
- Single point of failure
### Dual Firewall Architecture

- Two firewalls create an isolated DMZ segment between them
- DMZ network hosts client-facing services exposed to the Internet
- Multi-layered defense for internal networks
- Enhanced traffic monitoring
## Advantages

- Multi-layered access control
- Network reconnaissance prevention (attackers cannot directly probe the internal network)
- Improved security for internal assets

## Disadvantages

- Increased complexity and risk of misconfiguration
- Increased cost
- False sense of security (a DMZ is not a substitute for hardening)

## What Goes Inside a DMZ

Client-facing services: Web Servers, Mail Servers, Proxy Servers, DNS resolvers, Routers.

## What Does NOT Go Inside a DMZ

All internal and sensitive data and services not meant for direct access from external networks (e.g. databases with customer data, internal file shares, AD controllers).

## Related Concepts

- [[Digital Perimeter Security]]: the DMZ is a key part of the perimeter architecture
- [[Firewall]]: enforces the DMZ boundaries
- [[Secure by Design]]: compartmentalization principle in action
