---
title: IT-Sicherheit
aliases:
  - IT Security
  - ITS
tags:
  - fb20
  - master
description: "IT Security lecture, TU Darmstadt - FB20 Master"
---
## Notes
 * Lecture 2 Sec-Lab-1-Hint
* DNS Zones Sec-Lab-2-Hint
* RR Lecture 4 -relevant für lecture und exam

## Lecture 1
[[Major Cyberattacks]]

## Lecture 2 - Security Fundamentals

### Security Basics
- [[What is Cybersecurity?]]: definition, why security is hard, vocabulary (vulnerability, threat, exploit, risk, attack vector/surface)
- [[CIA Triad]]: Confidentiality, Integrity, Authenticity, Availability, Non-Repudiation, plus trade-offs

### Building Secure Systems
- [[Secure by Design]]: principles - least privilege, fail secure, compartmentalization, separation of duties, Kerckhoffs' principle
- [[Defense in Depth]]: layered defense (application, network, host, data, physical)
- [[Zero Trust Architecture]]: "trust nothing by default"; PDP/PEP; ZTA migration challenges

### Threat Modelling and Intelligence
- [[Threat Modelling]]: the four driving questions; STRIDE framework; PASTA (7 phases)
- [[Cyber Threat Intelligence]]: raw data -> information -> intelligence
- [[Indicator of Compromise]]: IoC types; Pyramid of Pain
- [[MITRE ATT&CK]]: Tactics, Techniques, Procedures (TTPs); ATT&CK matrix

### Threat Actors and Vulnerability Management
- [[Advanced Persistent Threat]]: APT groups; attack phases; case study APT29/SolarWinds
- [[Vulnerability Management]]: CVE, CWE, CVSS; patch strategies; case study CrowdStrike 2024

## Lecture 3 - Network Security

### Digital Perimeter Security
- [[Digital Perimeter Security]]: overview of perimeter defenses (firewall, IDS/IPS, DMZ, honeypot)
- [[Firewall]]: packet filtering (stateful and stateless), proxy firewalls, WAF, NGFW; what firewalls can and cannot do
- [[TCP 3-Way Handshake]]: SYN/SYN-ACK/ACK; foundation for stateless filtering via the ACK flag
- [[Intrusion Detection System]]: IDS (passive, off-path) vs IPS (active, in-line); NGFW as all-in-one
- [[Honeypot]]: decoy systems; high vs low interaction; AI-powered honeypots
- [[Demilitarized Zone]]: single vs dual firewall architectures; what does and does not belong in the DMZ

### Network Management
- [[IP Addressing]]: IPv4/IPv6, classful (outdated) and CIDR notation, IANA/RIRs, private ranges
- [[Network Address Translation]]: Static, Dynamic, PAT, NAT64; benefits and limitations
- [[NAT Slipstreaming]]: attack bypassing NAT via JavaScript and ALG abuse; v1 (single victim) and v2 (any internal device via H.323)

## Lecture 4 - DNS Security

### DNS Fundamentals
- [[Domain Name System]]: globally distributed hierarchical database; client-server over UDP/53; FQDN; domain/subdomain/zone distinction; root servers (13 logical, 600+ physical); authoritative nameservers vs. resolvers; Resource Records (A, AAAA, CNAME, MX, NS, SOA, TXT); zone files ($TTL, $ORIGIN, SOA fields, wildcards); DNSSEC record types (DNSKEY, DS, RRSIG)
