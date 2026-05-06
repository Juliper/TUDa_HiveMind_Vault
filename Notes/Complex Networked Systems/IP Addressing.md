---
title: IP Addressing
aliases:
tags:
description: "Addressing on the Internet: IPv4, IPv6, classful and CIDR notation, and address allocation."
---

**IP Addresses** are unique identifiers for Internet-facing devices, used like postal addresses to enable direct communication between devices on the Internet.

## IPv4

- Total address space: $2^{32}$ = **4,294,967,296** addresses
- Not enough for the modern Internet
- IPv4 addresses have been officially exhausted; they are now scarce and expensive

## IPv6

- 128-bit addresses, written as 8 groups of hexadecimals
- Total address space: $3.4 \times 10^{38}$ addresses
- Designed to last for the foreseeable future

## Class-Based Addressing (Outdated)

Before 1993, IPv4 addresses were divided into five fixed classes:

| Class | Range | Subnet Mask | Blocks | IPs per Block |
|---|---|---|---|---|
| A | 0.0.0.0 - 127.255.255.255 | /8 | 128 | 16,777,216 |
| B | 128.0.0.0 - 191.255.255.255 | /16 | 16,384 | 65,536 |
| C | 192.0.0.0 - 223.255.255.255 | /24 | 2,097,152 | 256 |
| D (Multicast) | 224.0.0.0 - 239.255.255.255 | n/a | n/a | n/a |
| E (Reserved) | 240.0.0.0 - 255.255.255.255 | n/a | n/a | n/a |

Problems:

- Predefined block sizes wasted addresses (limited flexibility)
- Routing tables grew rapidly, almost outgrowing routing capacity in the 1990s

## CIDR Notation

**Classless Inter-Domain Routing (CIDR)** replaces classful addressing.

- Network prefixes have variable length based on client needs
- Hierarchical address allocation
- Routers can aggregate prefixes, keeping routing tables smaller

CIDR notation has two parts:

- Base IP address
- Subnet mask defining the size of the network

Example: `15.24.12.0/24` means the network covers all addresses where the first 24 bits match `15.24.12.X`.

### Private (Non-Routable) Networks

Reserved for private use; not routed on the public Internet:

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

These ranges are typically used together with [[Network Address Translation]].

## Related Concepts

- [[Network Address Translation]]: maps private IPs to public IPs to extend IPv4 lifespan
