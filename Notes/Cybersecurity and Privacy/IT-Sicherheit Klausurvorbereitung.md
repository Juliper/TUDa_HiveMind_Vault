---
title: IT-Sicherheit Klausurvorbereitung
aliases:
  - IT-Sicherheit Klausur
  - IT-Sec Prüfungsvorbereitung
tags:
  - cybersecurity
  - network-security
  - exam-prep
description:
draft: false
---


### Basics

* What is Cybersecurity: the act of achieving a goal in the presence of an adversary.
* Vulnerability: a flaw, weakness of a software system that can be expploited by an attacker
* Threat: the entity that wants to compromise it sec goals (confidentiality, integrity usw.)
* Exploit: a pirce of code, data, command that takes advantage of a voulnerbility
* Risk: the potential loss or harm of an exploit
* Attack vector: path an attack uses to exploit target system
* Attack surface: total sum of vectors
* Secure by design
	* least privilege alles hat nur minimum access rights
	* defense in depth mehrere unabhängege system bieten protection
	* fail secure bei error in letzten sicheren zusatnd
	* segmentation: isolate components und nur das nötigste exposen
	* seperation of duties
	* no security through obsucrity
* STRIDE (um Angriffe zu kategorisieren)
	* Spoofing
	* Tampering
	* Repudiation
	* Information Disclosure
	* Denial of service
	* Escalating ppriviledges
* PASTA (Process for Attack Simulation and Threat Analysis)
	* Define Objective
	* Define Technical Scope
	* Application Decomposition & Analysis
	* Threat Analysis
	* Weakness & Vulnerability Analysis
	* Attacks Modeling & Simulation
	* Risk Analysis & Management
* Cyber Threat Intelligence (CTI) Prozess um angriffe zu analysieren und zu handeln
	* 

> [!example]- Erläutere erweiterte CIA-Schutzziele
> * Confidentiality
> * Integrity
> * Authenticity
> * Availability
> * Non-Repudiation

> [!example]- RIR, ROI, SPY???
### BGP

> [!example]- BGP Routing
> **Longest Prefix Match** > **Shortest Path Route**

> [!example]- Aufgabe: BGP Hijack
> ```
> 1.1.0.0/16    → AS1   (Path-Länge 1, direkter Nachbar)
> 1.1.0.0/17    → AS2
> 1.1.128.0/17  → AS2
> ```
> **Wie könnte das verhindert werden?** → **BGPsec** (kryptografische Absicherung der Pfad-Attribute, sodass gefälschte/spezifischere Prefixe nicht ungeprüft akzeptiert werden).

> [!abstract]- Gao-Rexford-Modell
> Beschreibt, **welche Routen ein AS aus wirtschaftlichem Interesse weitergibt**. Es gibt drei Beziehungstypen zwischen AS:
> - **Customer → Provider:** der Kunde zahlt den Provider für Transit.
> - **Peer ↔ Peer:** zwei AS tauschen kostenlos Verkehr aus (nur zwischen ihren eigenen Kunden).
> - **Provider → Customer:** der Provider liefert Transit an den Kunden.
>
> **Export-Regeln** (wem gebe ich eine gelernte Route weiter?):
>
> | Route gelernt von | wird weitergegeben an |
> |---|---|
> | Customer | **alle** (Customer, Peer, Provider) |
> | Peer | **nur Customer** |
> | Provider | **nur Customer** |
>
> **Merksatz:** Routen von Kunden bringen Geld → überall bewerben. Routen von Peers/Providern kosten Geld → nur an zahlende Kunden.
>
> **Folge:** Es entstehen nur **„valley-free" Pfade** (bergauf zu Providern, höchstens ein Peer-Schritt, dann bergab zu Kunden — nie „bergab und wieder bergauf"). Das verhindert, dass ein AS unbezahlten Transit für Fremde leistet, und hält Pfade kurz, kostengünstig und stabil.

> [!abstract]- RPKI (Resource Public Key Infrastructure)
> Kryptografische **Public-Key-Infrastruktur, die IP-Prefixe an das AS bindet, das sie announcen darf** — die Vertrauensbasis gegen BGP-Hijacking.
> - **ROA (Route Origin Authorization):** ein signierter Eintrag „Prefix `1.1.0.0/16` darf von **Origin AS1** angekündigt werden, maxLength /16". Ausgestellt vom rechtmäßigen Inhaber, verankert bei den fünf **RIRs** (RIPE, ARIN, …) als Trust Anchor.
> - **ROV (Route Origin Validation):** ein Router prüft ankommende BGP-Announcements gegen die ROAs → Ergebnis **valid / invalid / unknown**. `invalid`-Routen (falscher Origin oder Prefix spezifischer als `maxLength`) werden verworfen.
> - **Grenze:** RPKI/ROV sichert nur den **Origin** (wer den Prefix ansagt), **nicht den kompletten AS-Pfad** — dagegen braucht es BGPsec.

> [!abstract]- BGPsec
> Erweiterung von BGP, die den **gesamten AS-Pfad** kryptografisch absichert (setzt auf RPKI auf).
> - Jedes AS **signiert** beim Weiterleiten das Update inkl. des nächsten AS im Pfad. So entsteht eine **Signaturkette** über den ganzen Pfad.
> - Der Empfänger verifiziert jede Signatur → ein Angreifer kann **keinen gefälschten oder verkürzten Pfad** unterschieben (Path Forgery), nicht nur den Origin.
> - **vs. RPKI:** RPKI/ROV = nur Origin echt; BGPsec = **jeder Hop** des Pfads echt.
> - **Nachteil / warum kaum verbreitet:** teuer (Signatur pro Update/Hop), kein Aggregat-Schutz, hoher Rechen-/Speicheraufwand, funktioniert nur bei durchgängiger Unterstützung.

### DNS

> [!abstract]- Iterative DNS-Auflösung
> Der **Resolver** (meist beim Provider) arbeitet die Namenshierarchie selbst Schritt für Schritt ab; jeder gefragte Server antwortet entweder mit der Adresse oder **verweist** auf den nächsten zuständigen Server (Referral), statt selbst weiterzufragen.
>
> Beispiel `www.example.com`:
> 1. Resolver → **Root-Server**: „wer kennt `.com`?" → verweist auf **TLD-Server** `.com`.
> 2. Resolver → **TLD-Server**: „wer kennt `example.com`?" → verweist auf den **autoritativen Nameserver** von example.com.
> 3. Resolver → **autoritativer NS**: liefert die **A-Record-IP** von `www.example.com`.
> 4. Resolver cached das Ergebnis (TTL) und gibt es an den Client zurück.
>
> **Abgrenzung:** Beim **rekursiven** Query (Client → Resolver) übernimmt der Resolver die komplette Arbeit und liefert die fertige Antwort. Die einzelnen Schritte 1–3 laufen dann **iterativ**.

> [!abstract]- DNS-Tunneling
> Missbrauch des DNS-Protokolls, um **beliebige Daten in DNS-Anfragen/-Antworten zu schmuggeln** — DNS ist fast überall durch die Firewall erlaubt.
> - **Prinzip:** Der Angreifer betreibt einen autoritativen Nameserver für eine eigene Domain (`t.evil.com`). Das kompromittierte Gerät kodiert Daten in **Subdomains** (`<base32-daten>.t.evil.com`); der Resolver leitet die Query iterativ bis zum Angreifer-Server weiter, der antwortet (z. B. im TXT-Record) → **bidirektionaler Kanal**.
> - **Einsatz:** Datenexfiltration, Command-and-Control (C2), Umgehung von Captive Portals.
> - **Erkennung:** ungewöhnlich **lange/viele Subdomain-Anfragen**, hohe Query-Rate zu einer Domain, viel TXT-Traffic, hohe Entropie in den Labels.

### DHCP

> [!info]- Was ist DHCP?
> **DHCP (Dynamic Host Configuration Protocol)** ist ein Protokoll, mit dem ein Client beim Verbinden mit einem Netzwerk automatisch seine IP-Konfiguration — **IP-Adresse, Subnetzmaske, Default-Gateway und DNS-Server** — von einem Server zugewiesen bekommt, statt sie manuell konfigurieren zu müssen.
>
> **Ablauf (DORA):**
>
> | Paket | Bedeutung | Cast |
> |---|---|---|
> | **D**iscover | Client sucht DHCP-Server | Broadcast |
> | **O**ffer | Server bietet Konfiguration an | Unicast/Broadcast |
> | **R**equest | Client nimmt Angebot an | Broadcast |
> | **A**ck | Server bestätigt | Unicast |
>
> - **Gerät:** Router
> - **OSI-Schicht:** Layer 7 (Application)

### TCP/IP-Schichtenmodell

> [!note]- Die vier Schichten (+ Physical)
> | Schicht | |
> |---|---|
> | Application | |
> | Transport | |
> | Internet | |
> | Network | |
> | Physical | |

---

## Firewalls

> [!abstract] Grundlagen stateful vs. stateless
> **Stateful** — der Router merkt sich aktuelle Verbindungen (Conntrack).
>
> | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|
> | eth0 / lan | ip | ip | TCP / UDP | 443 / 21 / 22 / 80 | 443 / 21 / 22 / 80 | Established / New | Accept / Drop |
>
> **Stateless** — betrachtet jedes Paket isoliert.
>
> | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | ACK | Action |
> |---|---|---|---|---|---|---|---|
> | eth0 / lan | ip | ip | TCP / UDP | 443 / 21 / 22 / 80 | 443 / 21 / 22 / 80 | Yes / No | Accept / Drop |

> [!tip] Konventionen für alle Aufgaben
> - `eth0` = außen / Internet, `lan` bzw. `wlan0` = innen / Client
> - **Abort on first match** — die erste passende Regel entscheidet, Catch-all-Drop immer zuletzt
> - `*` = Wildcard

> [!note] Übersetzungstabelle stateful ↔ stateless
> | Stateful | Stateless | Bedeutung |
> |---|---|---|
> | `New` | `ACK = No` | nur das SYN |
> | `Established` | `ACK = Yes` | alles außer dem SYN |
> | `New` + `Established` (eine Richtung) | `ACK = *` | Aufbau **und** Datenverkehr |

### Beispielaufgaben

> [!example]- 1 — Client darf raus (HTTP), niemand darf rein
> **Blockt:** alle eingehenden Verbindungsversuche. **Erlaubt:** ausgehende HTTP-Verbindungen des Clients und deren Antwortpakete. Der Klassiker — das Heimnetz-Szenario.
>
> **Stateful**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | * | * | TCP | * | 80 | New | Accept |
> | 2 | * | * | * | TCP | * | * | Established | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> **Stateless**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | ACK | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | * | * | TCP | * | 80 | * | Accept |
> | 2 | eth0 | * | * | TCP | 80 | * | Yes | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> > [!warning] Stolperstein
> > Regel 1 braucht `ACK = *`, nicht `No` — sonst geht nur das SYN raus, aber keine Daten.

> [!example]- 2 — Server im eigenen Netz (HTTPS), sonst dicht
> **Blockt:** alle ausgehenden Verbindungsversuche. **Erlaubt:** eingehende HTTPS-Verbindungen zum Server 78.123.5.5 und bestehende Verbindungen. Spiegelbild von 1 — der Server ist Ziel, nicht Initiator.
>
> **Stateful**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | eth0 | * | 78.123.5.5 | TCP | * | 443 | New | Accept |
> | 2 | * | * | * | TCP | * | * | Established | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> **Stateless**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | ACK | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | eth0 | * | 78.123.5.5 | TCP | * | 443 | * | Accept |
> | 2 | lan | 78.123.5.5 | * | TCP | 443 | * | Yes | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> > [!warning] Stolperstein
> > In Regel 2 die **SrcIP mitnehmen**. Nur `SrcPort 443 + ACK=Yes` wäre zu weit — jeder interne Host dürfte dann mit gefälschtem SrcPort 443 Daten nach außen schicken (Covert Channel).

> [!example]- 3 — Beides gleichzeitig: Client raus + Server rein
> **Blockt:** alles außer: ausgehendes HTTP/HTTPS vom LAN und eingehendes HTTPS zum Server.
>
> **Stateful**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | * | * | TCP | * | 80 | New | Accept |
> | 2 | lan | * | * | TCP | * | 443 | New | Accept |
> | 3 | eth0 | * | 78.123.5.5 | TCP | * | 443 | New | Accept |
> | 4 | * | * | * | TCP | * | * | Established | Accept |
> | 5 | * | * | * | * | * | * | * | Drop |
>
> **Stateless**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | ACK | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | * | * | TCP | * | 80 | * | Accept |
> | 2 | lan | * | * | TCP | * | 443 | * | Accept |
> | 3 | eth0 | * | * | TCP | 80 | * | Yes | Accept |
> | 4 | eth0 | * | * | TCP | 443 | * | Yes | Accept |
> | 5 | eth0 | * | 78.123.5.5 | TCP | * | 443 | * | Accept |
> | 6 | lan | 78.123.5.5 | * | TCP | 443 | * | Yes | Accept |
> | 7 | * | * | * | * | * | * | * | Drop |
>
> > [!note] Merke
> > Jede erlaubte Verbindungsart braucht stateless **zwei** Zeilen (Hin- und Rückrichtung). Stateful reicht **eine** `New`-Zeile plus die gemeinsame `Established`-Zeile.

> [!example]- 4 — Nur ein bestimmter Host darf raus
> **Blockt:** alles außer HTTPS-Verkehr von 10.0.0.5. Alle anderen internen Hosts kommen nicht ins Internet.
>
> **Stateful**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | 10.0.0.5 | * | TCP | * | 443 | New | Accept |
> | 2 | * | * | * | TCP | * | * | Established | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> **Stateless**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | ACK | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | 10.0.0.5 | * | TCP | * | 443 | * | Accept |
> | 2 | eth0 | * | 10.0.0.5 | TCP | 443 | * | Yes | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |

> [!example]- 5 — Ausnahme von der Regel (Blacklist-Host)
> **Blockt:** SSH-Zugriffe von 10.0.0.66. **Erlaubt:** SSH von allen anderen Hosts des Subnetzes. Hier ist die **Reihenfolge zwingend** — die Drop-Ausnahme muss vor die Accept-Regel.
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | 10.0.0.66 | * | TCP | * | 22 | * | **Drop** |
> | 2 | lan | 10.0.0.0/24 | * | TCP | * | 22 | New | Accept |
> | 3 | * | * | * | TCP | * | * | Established | Accept |
> | 4 | * | * | * | * | * | * | * | Drop |
>
> > [!warning] Stolperstein
> > Vertauscht man 1 und 2, ist Regel 1 **tot** (Shadowing) — sie wird nie erreicht.

> [!example]- 6 — DNS erlauben (UDP)
> **Blockt:** alles außer DNS-Anfragen an 1.1.1.1. Wichtig, weil ohne DNS praktisch kein Surfen möglich ist.
>
> **Stateful**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | * | 1.1.1.1 | UDP | * | 53 | New | Accept |
> | 2 | * | * | * | UDP | * | * | Established | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> **Stateless**
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | ACK | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | lan | * | 1.1.1.1 | UDP | * | 53 | * | Accept |
> | 2 | eth0 | 1.1.1.1 | * | UDP | 53 | * | * | Accept |
> | 3 | * | * | * | * | * | * | * | Drop |
>
> > [!important] Kernaussage für die Klausur
> > UDP hat **kein ACK-Bit**. Stateless muss die Rückrichtung mit `ACK = *` pauschal aufmachen — jeder, der SrcIP 1.1.1.1 und SrcPort 53 fälscht, kommt durch. Stateful trackt den UDP-Flow per Timeout und ist hier klar überlegen.

> [!example]- 7 — DMZ-Szenario (drei Interfaces)
> **Blockt:** direkten Zugriff vom Internet ins LAN und vom LAN-fremden Verkehr in die DMZ. **Erlaubt:** Internet → DMZ-Webserver, LAN → Internet.
>
> | Rule | Interface | SrcIP | DstIP | Proto | Src Port | Dst Port | State | Action |
> |---|---|---|---|---|---|---|---|---|
> | 1 | eth0 | * | dmz-web | TCP | * | 443 | New | Accept |
> | 2 | lan | * | * | TCP | * | 443 | New | Accept |
> | 3 | lan | * | * | TCP | * | 80 | New | Accept |
> | 4 | * | * | * | TCP | * | * | Established | Accept |
> | 5 | * | * | * | * | * | * | * | Drop |
>
> > [!note] Sinn der DMZ
> > Kein Eintrag erlaubt `eth0 → lan` mit `New`. Wird der Webserver kompromittiert, kommt der Angreifer nicht weiter ins LAN.

> [!example]- 8 — Passives ICMP (Ping raus, nicht rein)
> **Blockt:** Pings von außen (verhindert Netzwerk-Scanning). **Erlaubt:** Pings von innen nach außen.
>
> | Rule | Interface | SrcIP | DstIP | Proto | Typ | State | Action |
> |---|---|---|---|---|---|---|---|
> | 1 | lan | * | * | ICMP | Echo Request | New | Accept |
> | 2 | eth0 | * | * | ICMP | Echo Reply | Established | Accept |
> | 3 | * | * | * | * | * | * | Drop |
>
> > [!note] Hinweis
> > ICMP hat keine Ports und kein ACK-Bit. Stateless kann nur über den **ICMP-Typ** unterscheiden (8 = Request, 0 = Reply) — das ist trivial fälschbar.

### Checkliste vor dem Abgeben

> [!check]- Sieben Punkte durchgehen
> 1. **Richtiger Port?** HTTP = 80, HTTPS = 443, SSH = 22, FTP = 21, DNS = 53, SMTP = 25, DHCP = 67/68
> 2. **Richtiges Protokoll?** DNS/DHCP = UDP, Rest meist TCP
> 3. **Beide Richtungen abgedeckt?** Stateless braucht pro Verbindung zwei Zeilen
> 4. **`ACK = *` in der Initiator-Richtung**, `ACK = Yes` in der Antwortrichtung
> 5. **Catch-all-Drop ganz unten**
> 6. **Keine toten Regeln** — spezifisch vor allgemein
> 7. **Ephemeral Ports als `*`** lassen, nie festlegen

### Warum stateless schwächer ist (Standard-Transferfrage)

> [!question]- Schwächen von stateless + Vorteil
> | Problem | Erklärung |
> |---|---|
> | **ACK-Spoofing** | Angreifer setzt ACK = 1 selbst → Paket sieht aus wie Antwort, kommt durch. Stateful verwirft mangels Conntrack-Eintrag. |
> | **UDP/ICMP** | Kein ACK-Bit, kein Handshake → Richtung nicht unterscheidbar. |
> | **Aktives FTP** | Datenverbindung wird von außen auf dynamischem Port aufgebaut → stateless muss alle Ports > 1024 öffnen; stateful nutzt Conntrack-Helper. |
> | **Fragmentierung** | Nur das erste Fragment enthält den TCP-Header mit Ports/Flags. |
>
> **Vorteil stateless:** kein Zustand → kein Speicherüberlauf bei DDoS, sehr schnell, beliebig auf mehrere Geräte skalierbar. Deshalb Standard für Router-ACLs im Backbone.

### Fragenkatalog Routing (wahr/falsch)

> [!question]- 9 Aussagen aus der Testklausur
> | Aussage | |
> |---|---|
> | DNS-Cache-Poisoning off-path möglich | **Wahr** (Kaminsky: TXID + Port raten) |
> | Switch braucht IP-Ebene | **Falsch** (Layer 2, MAC) |
> | In IPv6 kann jeder Gateway behaupten zu sein | **Wahr** (Rogue RA / NDP unauthentifiziert) |
> | TTL-Hack (GTSM) setzt TTL auf 1 | **Falsch** (auf **255**) |
> | Transportschicht adressiert Prozesse | **Wahr** (Ports) |
> | IPv6 hat 4-mal größeren Adressraum | **Falsch** (4× Bits, aber 2⁹⁶× Adressen) |
> | Host Discovery in IPv6 unmöglich | **Falsch** (Multicast `ff02::1`) |
> | Amplification = Paketgröße spoofen | **Falsch** (Quell-**IP** spoofen) |
> | DNS-Poisoning ermöglicht MitM | **Wahr** |

---

## Fuzzing

> [!abstract] Kurz erklärt
> **Fuzzing** = automatisiertes Testen mit massenhaft zufälligen/mutierten/ungültigen Eingaben, um Crashes, Hänger oder Memory Corruption auszulösen.
> - **vs. Code-Auditing:** skalierbar, kein Quellcode nötig, reale reproduzierbare Crashes (wenig False Positives) — aber testet nur erreichbaren Code; tiefe „bewachte" Pfade und reine Logikfehler bleiben verborgen (coverage-abhängig).
> - **Coverage-Guided (z. B. AFL):** Programm wird instrumentiert; Eingaben mit **neuer** Coverage (Basic Blocks/Edges) werden als Seeds behalten und weiter mutiert → Rückkopplungsschleife in unerforschte Programmteile.
> - **Corpus:** Sammlung repräsentativer, **gültiger, minimaler, diverser** Seed-Inputs. PDF-Parser → kleine PDFs mit verschiedenen Features (Text, Bilder, Fonts, Formulare, verschlüsselt, mehrseitig).
> - **CVE** = Common Vulnerabilities and Exposures, standardisierte öffentliche ID einer Schwachstelle (z. B. CVE-2014-0160 = Heartbleed).

> [!question]- Testklausur-Fragen Fuzzing
> - **Instrumentation-Counter:** einen pro Basic Block — an jedem Funktionseinstieg und jedem Verzweigungsziel (im Beispiel ~7–8).
> - **Welcher Code besser testbar?** Byte-für-Byte-Prüfung (mehrere `if`) — jeder Branch gibt **Teilfortschritt** als neue Coverage (`A`→`AB`→`ABC`). Ein einzelner String-Vergleich = **ein** Branch → alles-oder-nichts (Magic-Value-Problem).
> - **Zwei Schritte nach einem Crash:** (1) reproduzieren + Eingabe minimieren (Test Case Minimization), (2) Root-Cause / Exploitability im Debugger, deduplizieren, Fix/Report.

---

## Injections

> [!abstract] Angriffe klassifizieren
> | Szenario | Angriff |
> |---|---|
> | Bank-Link per Mail, Klick löst Transaktion via URL-Parameter aus | **CSRF** |
> | Firewall umgangen, SQL direkt an DB-Server | **kein Injection** (direkter unautorisierter DB-Zugriff) |
> | Username mit `<script>`, beim Anzeigen ausgeführt | **XSS** (stored) |
> | Python2 `input()` evaluiert Eingabe | **Code Injection** |
> | Viele Requests legen Server lahm | **DoS** |

### SQL Injection

> [!abstract] Kurz erklärt
> Einschleusen von SQL über nicht bereinigte Eingaben, sodass die Eingabe die **Struktur/Bedeutung** der Query verändert. **Gegenmittel:** Prepared Statements (korrekt parametrisiert).

> [!question]- Testklausur-Payloads (Notenverwaltung)
> - **Fremdes Ergebnis sehen** — `OR` hebelt die `matrnr`-Bedingung aus:
>   ```
>   examid: ' OR '1'='1
>   ```
>   → `... WHERE matrnr='0' AND examid='' OR '1'='1'` liefert **alle** Zeilen, Code gibt `result[0]` aus.
> - **Blind/Boolean-Injection** (existiert eine 1,0?):
>   ```
>   examid: ' OR examid='ITSEC-SS24' AND grade='1,0
>   ```
>   Am **binären Signal** (Ergebnis vs. „nichts gefunden") ablesen.
> - **Note ändern** (Stacked Query, `multi=True`):
>   ```
>   examid: '; UPDATE exam SET grade='1,0' WHERE matrnr=1337 AND examid='ITSEC-SS24'; --
>   ```
>   `-- ` kommentiert das schließende `'` aus.

### Code Injection (Buffer Overflow)

> [!abstract] Kurz erklärt
> Ungeprüfte Länge + fehlender Bounds-Check → Schreiben über den Puffer hinaus (**Stack-Buffer-Overflow**), überschreibt `saved rbp` und `saved rip` → **Kontrollflussübernahme**.

> [!question]- Testklausur-Fragen Code Injection
> - **Zielindex** = `(saved_rip − arr[0]) / 8`. Im Beispiel `(0x48−0x20)/8 = 5` → `len = 6` Schreibvorgänge; Shellcode in `arr[0..1]`, `saved rip` auf dessen Stackadresse (`0x7fffffffdd20`) setzen. Kein PIE/ASLR → Adresse fest.
> - **DEP / W⊕X:** Seiten sind entweder schreibbar **oder** ausführbar. Stack schreibbar, aber nicht ausführbar → eingeschleuster Shellcode lässt sich **nicht ausführen**.
> - **DEP umgehen:** **ROP** / Return-to-libc — vorhandene Gadgets (enden auf `ret`) bzw. Bibliotheksfunktionen (`system("/bin/sh")`) verketten, statt eigenen Code einzuschleusen.

---

## Web Security

> [!question]- Fragenkatalog Web (wahr/falsch)
> | Aussage | |
> |---|---|
> | Prepared Statements verhindern SQLi | **Wahr** |
> | Referrer-Header-Verifikation schützt effektiv gegen CSRF | **Falsch** (oft leer/entfernt → Token nötig) |
> | XSS nur bei gespeicherter Eingabe | **Falsch** (reflected & DOM-based) |
> | Private Browsing schützt effektiv gegen Tracking | **Falsch** (Fingerprinting, IP bleiben) |
> | Blacklisting schützt nicht gegen XSS | **Wahr** (Whitelisting/Encoding nötig) |
> | Same-Origin-Policy wird vom Browser umgesetzt | **Wahr** |
> | Cookies nicht für SQLi nutzbar | **Falsch** (Cookies = Nutzereingabe) |
> | XSS durch HTTPS verhinderbar | **Falsch** (TLS sichert Transport, nicht Inhalt) |

### XSS

> [!abstract] Reflektierter XSS (nicht-persistent)
> 1. Angreifer baut Link zur **verwundbaren, vertrauenswürdigen Seite** mit `<script>` im Parameter.
> 2. Opfer klickt → Payload geht an den echten Server.
> 3. Server **reflektiert** die Eingabe ungefiltert in die Antwort.
> 4. Browser führt das Skript **im Origin der vertrauenswürdigen Seite** aus → stiehlt z. B. Session-Cookies an den Angreifer.
>
> Nicht-persistent, weil der Payload nur in dieser einen Antwort steckt (nicht serverseitig gespeichert).
>
> **Phishing:** Täuschung des Menschen zur Preisgabe von Zugangsdaten. **TLS hilft nicht** — die Phishing-Domain kann ein gültiges Zertifikat haben; angegriffen wird der Mensch, nicht die Leitung.

### SSRF (Server-Side Request Forgery)

> [!abstract] Kurz erklärt
> Der Angreifer bringt den **Server** dazu, in seinem Namen HTTP-Requests an eine vom Angreifer kontrollierte Ziel-URL zu schicken. Der Server wird als Proxy missbraucht.
> - **Gefahr:** erreicht **interne Ressourcen**, die von außen gesperrt sind — andere Hosts im internen Netz, `localhost`-Dienste und besonders **Cloud-Metadaten-Endpunkte** (z. B. `http://169.254.169.254/` → Zugangs-Tokens). Firewall wird umgangen, weil die Anfrage vom vertrauenswürdigen Server ausgeht.
> - **Typische Stelle:** Funktionen, die eine URL vom Nutzer entgegennehmen (Webhook, „Bild von URL laden", PDF-Renderer, Link-Preview).
> - **Gegenmittel:** Ziel-URLs gegen **Whitelist** prüfen, interne/private IP-Bereiche und `localhost` blocken, Redirects nicht ungeprüft folgen, unnötige Protokolle (`file://`, `gopher://`) verbieten.

### PKI

> [!abstract] Kurz erklärt
> - **MitM auf Diffie-Hellman:** klassisches DH ist **nicht authentifiziert**. Eve führt **zwei** DH-Handshakes (je einen mit Alice und Bob), sitzt dazwischen, ent-/verschlüsselt beide Seiten.
> - **Fix:** DH-Nachrichten (`g^a`, `g^b`) **signieren**; Empfänger prüft mit dem öffentlichen Schlüssel. Voraussetzung: **authentischer Public Key** des Gegenübers vorher bekannt.
> - **Hierarchische PKI (ohne Out-of-Band):** vertrauenswürdige **CA** signiert Zertifikate (Identität ↔ Public Key); Verifikation entlang der **Vertrauenskette** Root → Intermediate → End-Entity gegen vorinstalliertes Root-Zertifikat.

> [!question]- CRL vs. OCSP
> | | CRL | OCSP |
> |---|---|---|
> | Prinzip | CA-signierte **Liste** widerrufener Seriennummern | **Echtzeit-Abfrage** eines einzelnen Zertifikats |
> | Abruf | periodischer **Download**, lokal geprüft | Online beim Responder (good/revoked/unknown) |
> | Nachteil | groß, zwischen Updates **veraltet** | Responder erfährt besuchtes Ziel (→ Datenschutz; Fix: OCSP Stapling) |
