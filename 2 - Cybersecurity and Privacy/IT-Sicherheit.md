---
title: IT-Sicherheit
aliases:
  - IT Security
  - ITS
tags:
  - fb20
  - master
description:
draft: false
---
# Syllabus

| Moodle       | [Link](https://moodle.informatik.tu-darmstadt.de/course/view.php?id=1994) |
| ------------ | ------------------------------------------------------------------------- |
| Dozent       | Donika Mirdita                                                            |
| Prüfungsform | Klausur + Sec-Lab (Bonus)                                                 |

## Notes
 * Lecture 2 Sec-Lab-1-Hint
* DNS Zones Sec-Lab-2-Hint
* RR Lecture 4 - relevant für lecture und exam
## Lecture 2 - Security Fundamentals

### Security Basics
- [[What is Cybersecurity?]]
- [[CIA Triad]]
- TODO - Add "Kerckhoffs' principle"
### Building Secure Systems
- [[Secure by Design]]
- [[Zero Trust Architecture]]
- TODO - Maybe add "Scenario: BuildHub"?
### Threat Modelling and Intelligence
- [[Threat Modelling]]
- [[Cyber Threat Intelligence]]
- [[Indicator of Compromise]]
- [[MITRE ATT&CK]]

### Threat Actors and Vulnerability Management
- [[Advanced Persistent Threat]]
- [[Vulnerability Management]]

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
