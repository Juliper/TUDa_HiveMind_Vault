---
title: NotPetya
aliases:
  - NotPetya Attack
  - Petya
tags:
  - cybersecurity
  - cyberattack
  - malware
  - wiper
description: "Destruktiver Cyberangriff von 2017, der als Ransomware getarnt war, aber tatsächlich ein Wiper war."
---

# NotPetya

**NotPetya** (Juni 2017) ist einer der destruktivsten Cyberangriffe der Geschichte. Er wurde zunächst für eine Variante der [[Ransomware]] *Petya* gehalten — tatsächlich war er jedoch ein **Wiper**: Verschlüsselter Inhalt konnte nie wiederhergestellt werden, da kein funktionierender Entschlüsselungsmechanismus existierte.

## Verbreitung

- Initiale Infektionsvektoren: kompromittiertes Update der ukrainischen Buchhaltungssoftware **M.E.Doc**
- Laterale Ausbreitung im Netzwerk über:
  - **EternalBlue** (NSA-Exploit für SMBv1, CVE-2017-0144) — dasselbe Tool wie bei [[WannaCry]]
  - **Mimikatz**-basiertes Credential-Harvesting → Ausführung über PsExec und WMIC

```mermaid
flowchart TD
    A[M.E.Doc Update\nkompromittiert] --> B[Erstinfektion\nukrainischer Unternehmen]
    B --> C{Laterale Ausbreitung}
    C -->|EternalBlue via SMBv1| D[Weiterer Host]
    C -->|Mimikatz + PsExec/WMIC| D
    D --> C
    D --> E[MBR + MFT\nüberschreiben]
    E --> F[System nicht\nmehr bootbar]
```

## Wirkung

- Überschreibt den **Master Boot Record (MBR)** → System nicht mehr bootbar
- Verschlüsselt zusätzlich die MFT (NTFS Master File Table)
- Ransom-Note war Ablenkung; keine echte Entschlüsselung möglich

## Schäden

| Organisation | Schaden |
|---|---|
| Maersk (Shipping) | ~$300 Mio., 45.000 PCs neu installiert |
| Merck (Pharma) | ~$870 Mio. |
| FedEx / TNT | ~$400 Mio. |
| Gesamtschaden (geschätzt) | **> $10 Mrd.** |

## Zuschreibung

Die USA, EU und mehrere Verbündete schrieben den Angriff dem russischen Militärgeheimdienst **GRU** (Einheit Sandworm) zu. Primärziel war die Ukraine, der Schaden breitete sich jedoch global aus (*Kollateralschaden durch Netzwerkvernetzung*).

## Lektionen

- Supply-Chain-Angriffe (kompromittiertes Software-Update) sind hocheffektiv
- Netzwerksegmentierung hätte die laterale Ausbreitung eingeschränkt
- Patch-Management (SMBv1 war bereits gepatcht durch MS17-010) ist kritisch
