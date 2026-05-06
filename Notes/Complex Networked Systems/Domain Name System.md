---
title: Domain Name System
aliases:
  - DNS
  - Nameserver
  - Resolver
  - FQDN
  - Fully Qualified Domain Name
tags:
  - networking
  - cybersecurity
  - dns
description: "Globally distributed hierarchical database that maps human-readable hostnames to IP addresses — the phonebook of the internet."
---

The **Domain Name System (DNS)** is the phonebook of the internet. It maps human-readable hostnames (e.g. `tucan.tu-darmstadt.de`) to IP addresses, acting as the human interface to network addressing.

## Model

- Client-server model: client sends a query, server returns an answer
- Traditionally **UDP-based** (port 53), stateless communication
- Falls back to **TCP** when responses are too large or during zone transfers

## Architecture

DNS is a **globally distributed, hierarchical database**. The namespace is a tree:

```
. (root)                   ← DNS Root Zone
├── com / de / org / …     ← Top-Level Domain (TLD)
│   ├── google / tu-darmstadt / …   ← Second-Level Domain
│   │   └── scholar / tucan / …    ← Subdomain
```

| Term | Definition |
|---|---|
| **Domain** | Unique name identifying a specific area on the web |
| **Subdomain** | Prefix added to a domain to specify a distinct section |
| **Zone** | Portion of the domain namespace managed by a specific authority |
| **FQDN** | Fully Qualified Domain Name — the complete unambiguous name, always ends with `.` (e.g. `tucan.tu-darmstadt.de.`) |

### Key Components

**DNS Root Servers** — The highest nodes in the DNS hierarchy; starting point for all name resolutions. Logically there are 13 root servers (limitation from the old spec), but the 13 IPs are served by 600+ physical servers worldwide.

**Nameservers** — Servers that host and serve DNS data.

**Authoritative Nameservers** — Nameservers responsible for specific domains; hold the actual resource records.

**Resolver** — Middleware between client and the DNS infrastructure. Queries nameservers to resolve domain names on behalf of the client. Caches results to reduce load.

## Resource Records (RR)

DNS data is stored as **Resource Records**. The most important types:

| Type | Example | Function |
|---|---|---|
| `A` | `12.233.89.54` | IPv4 Address |
| `AAAA` | `28:98:fe43::3` | IPv6 Address |
| `CNAME` | `alt.domain.com` | Alias for a domain name |
| `TXT` | `"some text"` | Additional info in text form |
| `NS` | `ns.domain.com` | Nameserver for the domain |
| `MX` | `mx.domain.com` | Mail server for the domain |
| `SOA` | — | Start of Authority: admin info about a zone |
| `DNSKEY` | `257 3 1 AWA56bd…` | Public key for signing DNS RRs (DNSSEC) |
| `DS` | `31589 8 2 C6744W…` | Hash of KSK from the child zone (DNSSEC) |
| `RRSIG` | `A 13 3 60 230018…` | Cryptographic signature over an RRset (DNSSEC) |

## DNS Zones

A **zone file** defines all resource records for a zone. Key directives:

- `$TTL` — Time-To-Live: how long resolvers may cache the zone data
- `$ORIGIN` — Base domain name; relative names in the file are appended to this
- `*` (wildcard) — Matches requests for any non-existing subdomain and assigns it default RR values

**SOA record** fields:
| Field | Meaning |
|---|---|
| Serial | Zone file version; incremented on every update |
| Refresh | How often secondary nameservers poll the primary for the SOA record |
| Retry | Retry interval if refresh fails |
| Expiry | Time after which secondary stops serving data if it can't reach the primary |
| nxdomain TTL | Negative caching time (how long to cache "does not exist" answers) |

## Related Concepts

- [[IP Addressing]]: the underlying addressing system DNS resolves to
- [[Network Address Translation]]: interacts with DNS in NAT environments
