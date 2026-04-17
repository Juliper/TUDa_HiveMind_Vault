---
title: Major Cyberattacks
aliases:
  - Cyberangriffe
tags:
  - moc
  - cybersecurity
description: "Map of Content: Bedeutende Cyberangriffe und ihre Techniken."
---

# Major Cyberattacks

## Angriffe

| Angriff | Jahr | Typ | Technik |
|---|---|---|---|
| [[WannaCry]] | 2017 | Ransomware | EternalBlue (SMBv1) |
| [[NotPetya]] | 2017 | Wiper | EternalBlue + Mimikatz, Supply Chain |
| [[XZ Utils Attack]] | 2024 | Backdoor | Supply Chain, Social Engineering |
| [[NFS Buffer Overflow]] | — | Remote Exploit | Stack Buffer Overflow |

## Nach Angriffstyp

### Supply-Chain-Angriffe
- [[NotPetya]] — kompromittiertes M.E.Doc-Update als Einfallstor
- [[XZ Utils Attack]] — Backdoor über mehrjährigen Vertrauensaufbau eingeschleust

### Exploit-basierte Angriffe
- [[WannaCry]] — EternalBlue-Wurm mit Kill Switch
- [[NFS Buffer Overflow]] — klassischer Stack Overflow gegen privilegierten Daemon

## Gemeinsame Werkzeuge & Exploits

- **EternalBlue** (CVE-2017-0144) — von der NSA entwickelt, durch Shadow Brokers geleakt; genutzt von [[WannaCry]] und [[NotPetya]]
