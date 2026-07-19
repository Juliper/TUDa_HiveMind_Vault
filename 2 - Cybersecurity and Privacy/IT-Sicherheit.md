---
title: IT-Sicherheit
aliases:
  - IT Security
  - ITS
tags:
  - fb20
  - master
description: Ausgewählte Konzepte der IT-Sicherheit (Kryptographie; Sicherheitsmodelle; Authentifikation; Zugriffskontrolle; Sicherheit in Netzen; Trusted Computing; Security Engineering; Privatsphäre und Datenschutz; Web- und Browser-Sicherheit; Informationssicherheitsmanagement, IT-Forensik, Cloud Computing)
draft: false
---
# Syllabus

| Moodle       | [Link](https://moodle.informatik.tu-darmstadt.de/course/view.php?id=1994) |
| ------------ | ------------------------------------------------------------------------- |
| Dozent       | Donika Mirdita                                                            |
| Prüfungsform | Klausur + Sec-Lab (Bonus)                                                 |
# Lecture
## Notes
* Sec-Lab-1-Hint: Lecture 2 is relevant
* Sec-Lab-2-Hint: DNS Zones are relevant
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
- [[Digital Perimeter Security]]
### Network Management
- [[IP Addressing]]
- TODO - Add "Network Address Translation" note
- [[NAT Slipstreaming]]

## Lecture 4 - DNS Security
TODO - Finish lecture

### DNS Fundamentals
- [[Domain Name System]]

## Lecture 5 - Routing Security

### Internet Structure and BGP Fundamentals
- [[Autonomous System]]
- [[Border Gateway Protocol]]

### BGP Route Selection
- [[Gao-Rexford Model]]

### Attacks on BGP
- [[BGP Hijacking]]

### BGP Security Measures
- [[Internet Routing Registry]]
- [[Resource Public Key Infrastructure]]
- [[BGPSec]]
# Klausurvorbereitung
## Klausurfragen

### Kurze Fragen
* Was ist DHCP -> DHCP (Dynamic Host Configuration Protocol) ist ein Protokoll, mit dem ein Client beim Verbinden mit einem Netzwerk automatisch seine IP-Konfiguration — IP-Adresse, Subnetzmaske, Default-Gateway und DNS-Server — von einem Server zugewiesen bekommt, statt sie manuell konfigurieren zu müssen.

### BGP Routing
Gegeben Tabelle mit Prefix, From Router und Path length -> longest prefix match 

### BGP Hijack
1.1.0.0/16    → AS1   (Path-Länge 1, direkter Nachbar)
1.1.0.0/17    → AS2
1.1.128.0/17  → AS2

Wie könnte das verhindert werden? BGPSec
### DHCP
Was ist DHCP -> DHCP (Dynamic Host Configuration Protocol) ist ein Protokoll, mit dem ein Client beim Verbinden mit einem Netzwerk automatisch seine IP-Konfiguration — IP-Adresse, Subnetzmaske, Default-Gateway und DNS-Server — von einem Server zugewiesen bekommt, statt sie manuell konfigurieren zu müssen.

Pakete:
Discover: Client sucht DHCP Server (broadcast)
Offer: Server bietet config an
request: client nimm an (broadcast)
ack: server besetätigt

Gerät: Router
Osi Schicht: Layer 7 (Application)

### TCP/IP
Application
Transport
Internet
Network
Physical

### Firewall
statefull (router merkt sich aktuelle verbindungen)

| Interface  | SrcIP | DstIP | Proto     | Src Port           | Dst Port           | State             | Action        |
| ---------- | ----- | ----- | --------- | ------------------ | ------------------ | ----------------- | ------------- |
| eth0 / lan | ip    | ip    | TCP / UDP | 443 / 21 / 22 / 80 | 443 / 21 / 22 / 80 | Established / New | Accept / Drop |
stateless (betrachtet jedes paket isoliert)

| Interface  | SrcIP | DstIP | Proto     | Src Port           | Dst Port           | ACK      | Action        |
| ---------- | ----- | ----- | --------- | ------------------ | ------------------ | -------- | ------------- |
| eth0 / lan | ip    | ip    | TCP / UDP | 443 / 21 / 22 / 80 | 443 / 21 / 22 / 80 | Yes / No | Accept / Drop |
#### Beispiele
- `eth0` = außen / Internet, `lan` bzw. `wlan0` = innen / Client
- **Abort on first match** — die erste passende Regel entscheidet, Catch-all-Drop immer zuletzt
- `*` = Wildcard

Übersetzungstabelle:

|Stateful|Stateless|Bedeutung|
|---|---|---|
|`New`|`ACK = No`|nur das SYN|
|`Established`|`ACK = Yes`|alles außer dem SYN|
|`New` + `Established` (eine Richtung)|`ACK = *`|Aufbau **und** Datenverkehr|

---

#### 1. Client darf raus (HTTP), niemand darf rein

**Blockt:** alle eingehenden Verbindungsversuche. Erlaubt: ausgehende HTTP-Verbindungen des Clients und deren Antwortpakete. Der Klassiker — das Heimnetz-Szenario.

#### Stateful

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|*|*|TCP|*|80|New|Accept|
|2|*|*|*|TCP|*|*|Established|Accept|
|3|*|*|*|*|*|*|*|Drop|

#### Stateless

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|ACK|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|*|*|TCP|*|80|*|Accept|
|2|eth0|*|*|TCP|80|*|Yes|Accept|
|3|*|*|*|*|*|*|*|Drop|

> **Stolperstein:** Regel 1 braucht `ACK = *`, nicht `No` — sonst geht nur das SYN raus, aber keine Daten.

---

### 2. Server im eigenen Netz (HTTPS), sonst dicht

**Blockt:** alle ausgehenden Verbindungsversuche. Erlaubt: eingehende HTTPS-Verbindungen zum Server 78.123.5.5 und bestehende Verbindungen. Spiegelbild von 1 — der Server ist Ziel, nicht Initiator.

### Stateful

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|eth0|*|78.123.5.5|TCP|*|443|New|Accept|
|2|*|*|*|TCP|*|*|Established|Accept|
|3|*|*|*|*|*|*|*|Drop|

### Stateless

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|ACK|Action|
|---|---|---|---|---|---|---|---|---|
|1|eth0|*|78.123.5.5|TCP|*|443|*|Accept|
|2|lan|78.123.5.5|*|TCP|443|*|Yes|Accept|
|3|*|*|*|*|*|*|*|Drop|

> **Stolperstein:** In Regel 2 die **SrcIP mitnehmen**. Nur `SrcPort 443 + ACK=Yes` wäre zu weit — jeder interne Host dürfte dann mit gefälschtem SrcPort 443 Daten nach außen schicken (Covert Channel).

---

## 3. Beides gleichzeitig — Client raus + Server rein

**Blockt:** alles außer: ausgehendes HTTP/HTTPS vom LAN und eingehendes HTTPS zum Server.

### Stateful

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|*|*|TCP|*|80|New|Accept|
|2|lan|*|*|TCP|*|443|New|Accept|
|3|eth0|*|78.123.5.5|TCP|*|443|New|Accept|
|4|*|*|*|TCP|*|*|Established|Accept|
|5|*|*|*|*|*|*|*|Drop|

### Stateless

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|ACK|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|*|*|TCP|*|80|*|Accept|
|2|lan|*|*|TCP|*|443|*|Accept|
|3|eth0|*|*|TCP|80|*|Yes|Accept|
|4|eth0|*|*|TCP|443|*|Yes|Accept|
|5|eth0|*|78.123.5.5|TCP|*|443|*|Accept|
|6|lan|78.123.5.5|*|TCP|443|*|Yes|Accept|
|7|*|*|*|*|*|*|*|Drop|

> Merke: Jede erlaubte Verbindungsart braucht stateless **zwei** Zeilen (Hin- und Rückrichtung). Stateful reicht **eine** `New`-Zeile plus die gemeinsame `Established`-Zeile.

---

## 4. Nur ein bestimmter Host darf raus

**Blockt:** alles außer HTTPS-Verkehr von 10.0.0.5. Alle anderen internen Hosts kommen nicht ins Internet.

### Stateful

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|10.0.0.5|*|TCP|*|443|New|Accept|
|2|*|*|*|TCP|*|*|Established|Accept|
|3|*|*|*|*|*|*|*|Drop|

### Stateless

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|ACK|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|10.0.0.5|*|TCP|*|443|*|Accept|
|2|eth0|*|10.0.0.5|TCP|443|*|Yes|Accept|
|3|*|*|*|*|*|*|*|Drop|

---

## 5. Ausnahme von der Regel (Blacklist-Host)

**Blockt:** SSH-Zugriffe von 10.0.0.66. Erlaubt: SSH von allen anderen Hosts des Subnetzes. Hier ist die **Reihenfolge zwingend** — die Drop-Ausnahme muss vor die Accept-Regel.

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|10.0.0.66|*|TCP|*|22|*|**Drop**|
|2|lan|10.0.0.0/24|*|TCP|*|22|New|Accept|
|3|*|*|*|TCP|*|*|Established|Accept|
|4|*|*|*|*|*|*|*|Drop|

> Vertauscht man 1 und 2, ist Regel 1 **tot** (Shadowing) — sie wird nie erreicht.

---

## 6. DNS erlauben (UDP)

**Blockt:** alles außer DNS-Anfragen an 1.1.1.1. Wichtig, weil ohne DNS praktisch kein Surfen möglich ist.

### Stateful

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|*|1.1.1.1|UDP|*|53|New|Accept|
|2|*|*|*|UDP|*|*|Established|Accept|
|3|*|*|*|*|*|*|*|Drop|

### Stateless

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|ACK|Action|
|---|---|---|---|---|---|---|---|---|
|1|lan|*|1.1.1.1|UDP|*|53|*|Accept|
|2|eth0|1.1.1.1|*|UDP|53|*|*|Accept|
|3|*|*|*|*|*|*|*|Drop|

> **Kernaussage für die Klausur:** UDP hat **kein ACK-Bit**. Stateless muss die Rückrichtung mit `ACK = *` pauschal aufmachen — jeder, der SrcIP 1.1.1.1 und SrcPort 53 fälscht, kommt durch. Stateful trackt den UDP-Flow per Timeout und ist hier klar überlegen.

---

## 7. DMZ-Szenario (drei Interfaces)

**Blockt:** direkten Zugriff vom Internet ins LAN und vom LAN-fremden Verkehr in die DMZ. Erlaubt: Internet → DMZ-Webserver, LAN → Internet.

|Rule|Interface|SrcIP|DstIP|Proto|Src Port|Dst Port|State|Action|
|---|---|---|---|---|---|---|---|---|
|1|eth0|*|dmz-web|TCP|*|443|New|Accept|
|2|lan|*|*|TCP|*|443|New|Accept|
|3|lan|*|*|TCP|*|80|New|Accept|
|4|*|*|*|TCP|*|*|Established|Accept|
|5|*|*|*|*|*|*|*|Drop|

> Kein Eintrag erlaubt `eth0 → lan` mit `New` — genau das ist der Sinn der DMZ. Wird der Webserver kompromittiert, kommt der Angreifer nicht weiter ins LAN.

---

## 8. Passives ICMP (Ping raus, nicht rein)

**Blockt:** Pings von außen (verhindert Netzwerk-Scanning). Erlaubt: Pings von innen nach außen.

|Rule|Interface|SrcIP|DstIP|Proto|Typ|State|Action|
|---|---|---|---|---|---|---|---|
|1|lan|*|*|ICMP|Echo Request|New|Accept|
|2|eth0|*|*|ICMP|Echo Reply|Established|Accept|
|3|*|*|*|*|*|*|Drop|

> ICMP hat keine Ports und kein ACK-Bit. Stateless kann nur über den **ICMP-Typ** unterscheiden (8 = Request, 0 = Reply) — das ist trivial fälschbar.

---

## Checkliste vor dem Abgeben

1. **Richtiger Port?** HTTP = 80, HTTPS = 443, SSH = 22, FTP = 21, DNS = 53, SMTP = 25, DHCP = 67/68
2. **Richtiges Protokoll?** DNS/DHCP = UDP, Rest meist TCP
3. **Beide Richtungen abgedeckt?** Stateless braucht pro Verbindung zwei Zeilen
4. **`ACK = *` in der Initiator-Richtung**, `ACK = Yes` in der Antwortrichtung
5. **Catch-all-Drop ganz unten**
6. **Keine toten Regeln** — spezifisch vor allgemein
7. **Ephemeral Ports als `*`** lassen, nie festlegen

## Warum stateless schwächer ist (Standard-Transferfrage)

|Problem|Erklärung|
|---|---|
|**ACK-Spoofing**|Angreifer setzt ACK = 1 selbst → Paket sieht aus wie Antwort, kommt durch. Stateful verwirft mangels Conntrack-Eintrag.|
|**UDP/ICMP**|Kein ACK-Bit, kein Handshake → Richtung nicht unterscheidbar.|
|**Aktives FTP**|Datenverbindung wird von außen auf dynamischem Port aufgebaut → stateless muss alle Ports > 1024 öffnen; stateful nutzt Conntrack-Helper.|
|**Fragmentierung**|Nur das erste Fragment enthält den TCP-Header mit Ports/Flags.|

Vorteil stateless: kein Zustand → kein Speicherüberlauf bei DDoS, sehr schnell, beliebig auf mehrere Geräte skalierbar. Deshalb Standard für Router-ACLs im Backbone.