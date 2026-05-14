---
title: CNuvS
aliases:
  - Computer Netzwerke und verteilte Systeme
tags:
  - fb20
  - bachelor
  - pflichtmodul
  - semester-4
  - 5CP
description: ""
draft: false
---
# Was ist ein verteiltes System?

Mehre Computer die eine Aufgabe erfüllen indem sie über ein Netzwerk kommunizieren

# Was ist ein Kommunicationsprotokoll?

Legt das Format und die Reihenfolge von Nachrichten und ausgeführte Aktionen fest.

Bei Schichten Architektur benutzten die verschiedenen Schichten immer das selbe Protokoll (IP Layer vom Sender == IP Layer vom Empfänger)

# Informationen, Data und Signale

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/34e921a8-2ab9-4eba-b803-ccc3eb24f0ae/Untitled.png)

# Übertragung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4182c53-93f4-4c8d-9578-48c1488107e8/Untitled.png)

Propagation delay := Entfernung / Verbreitungsgeschwindigkeit

Data rate := Bits / Sekunden

Error rate := Falsche Bits / Sekunde

# Simplex

- Nur eine Partei überträgt gleichzeitig
- Beispiele: Radio

# Half duplex

- Sender und Empfänger wechseln sich ab
- Beispiele: Konversation
- Umsetzung
    - Time division duplex (TDD) := Feste Zeitslots festlegen für Senden und Empfangen der Parteien
    - on-demand := Sender kündigt Übertragung an
        - Maximale Länge festelgen (ansonsten könnte Übertragung blockiert werden)
        - Empfänger muss Anküdigung von payload unterscheiden

# Full duplex

- Beide Parteien können zu jeder Zeit senden
- Umsetzung
    - Frequency Division Duplex (FDD) := Sender und Empfänger verwenden andere Frequenu für Übertragung
    - Time division duplex (TDD) := Kann Full dulpex ermöglichen
        - Parteien sammeln Datenpackte und nutzen hohe Übertragungsrate des Mediums (niemand muss somit warten)
        - Medium muss mindestens so schnell wie die Summe der Datenraten von Parteien sein

# Wie kann man über Switching Elements kommunizieren?

- Circuit Switching
    - Eine tatsächliche Verbindung zwischen den Geräten (Kabel) wird hergestellt (alte Telefone)
    - Braucht viele Resourcen (wenn nur 5 Kabel da können auch nur 5 kommunizieren)
    - Kein delay und simple
- Packet Switching
    - Daten werden auf Pakete aufgeteilt und dann zugestellt
    - Zusätzliche Informationen nötig (keine peer to peer)
    - Können zwischengespeichert werden (delay)

# Multiplexing

Reguliert die Nutzung eines geteilten von mehreren Nutzern geteiltes Medium

Time Division Multiplexing (TDM) := Packete werden nacheinander gesendet

Frequency Division Multiplexing (FDM) := Packete werden gleichzeitig aber mit verschiedenen Frequenzen übertragen

Code Division Multiplexing (CDM) := Signal wird mit zufälligen anderen Signal (Spreizcode) multipliziert um Signal einzigartig zu machen

Space Division Multiplexing (SDM) := Benutzt mehre Kabel oder Routen

# Upward und Downward Multiplexing

# OSI

- Protokoll := legt Format fest, Reihenfolge der Nachrichten, Aktionen die ausgeführt werden
- Layer := Unabhänige Schichten mit bestimmten Protokollen
- Service := Dienst mit wohldefinierter Schnittstelle die eine untere Schicht einer oberen Schicht zur Verfügung stellt.
    - Connection Establishment (CON) → Data Exchange (DAT) → Commection Release (DIS) (connection orienterd services)
    - Data Exchange (DAT) (connectionless services)
- Dateneinheiten
    - packet := Einheit für Transportationen (Transport Layer)
    - datagram := Eigenständiges Packete (connectionless)
    - frame := ready to send (fast unterste Schicht)
    - cell := kleines Packet mit statischer größe
- OSI Einheiten
    - PDU (Protocol Data Unit) := besteht aus PCI (Protocol Control Information) und SCU (Service Data Unit)

# Routing vs. Forwarding

- Routing beschreibt den Prozess des Planens und Berechnens der Routen
- Forwarding ist der Prozess der tatsächlichen weiterleitung über Knoten

# Routing vs. connections

|Merkmal|CONS (virtual circuit)|CLNS (datagram)|
|---|---|---|
|Verbindungsaufbau|Ja|Nein|
|Routing-Algorithmen|Bei Verbindugnsaufbau|Regelmäßig oder bei wahrgenommenen Netzwerkänderungen|
|Kenntnis der Verbindung|Jedes Zwischensystem weiß Bescheid|Nur Endsysteme wissen Bescheid|

# Welche Arten von Routing Algorithmen gibt es?

**Non-adaptive routing algorithms**

- berücksichtigen den aktuellen Zustand des Netzwerks nicht bei ihren Routing-Entscheidungen. (Beispiele: Flooding, Vorkonfiguration)

**Adaptive routing algorithms**

- berücksichtigen den aktuellen Zustand des Netzwerks bei ihren Routing-Entscheidungen. (Beispiele: Distanzvektor-Routing, Link-State-Routing)
- Passt sich nicht an den Netzwerkverkehr an (ändert sich zu schnell)

## Flooding (non-adaptive)

- Jedes ankommende Packet wir an jeden Nachbarn weitergesendet (außer zum Sender).
- Nachteil sind viele Duplikate (kann durch TTL oder Router merken sich Sequenznummer behoben werden)

Anwendungen

- Das Netzwerk sich schnell ändert und adaptives Routing zu langsam und fehleranfällig ist.
- Viele oder alle Nachrichten an viele Empfänger gesendet werden müssen.
- **Krisenanwendungen:**
    - In Krisensituationen ist es wünschenswert, dass viele Router verfügbar sind (alle Systeme fungieren als Router). Wenn ein Router ausfällt (z. B. durch eine Naturkatastrophe), kann Flooding die Nachrichten immer noch an ihre Ziele weiterleiten.
- **Verteilte Datenbanken:**
    - Mit Flooding können mehrere Datenbanken gleichzeitig mit einer einzigen Nachricht aktualisiert werden.
- **Netzwerke mit häufigen Topologieänderungen:**
    - Mobile/Ad-hoc-Netzwerke und P2P-Overlays sind Beispiele für Netzwerke mit häufigen Topologieänderungen. In diesen Netzwerken kann Flooding ein effektives Routing-Protokoll sein.

## Static Routing (non-adaptive)

- Jeder Router bekommt statische Routing Tabelle
- Wenn sich der Traffic im Laufe der Zeit erheblich ändert, ist eine enorme Überprovisionierung (d. h. große Kabel und Router überall) erforderlich, um das Netzwerk in allen Traffic-Situationen am Leben zu erhalten.
- Computer-Traffic ist oft "bursty", d. h. sehr variabel in der Intensität.

**Vorteile von statischem Routing**

- Einfach zu implementieren und zu verwalten.
- Robust und zuverlässig.
- Erfordert keine dynamischen Updates.

**Nachteile von statischem Routing**

- Nicht geeignet für dynamische Umgebungen.
- Kann zu unnötigen Überlastungen führen, wenn der Traffic stark schwankt.
- Kann nicht auf Netzwerkänderungen reagieren.

## Centralized Adaptive Routing

Routing Control Center (RCC) bekommt periodisch Updates von allen Knoten und updatet dann die besten Routen und teilt diese mit den Knoten.

Probleme:

- Vulnerability: Wenn RCC down dann non-adaptive
- Scalability: RCC bekommt viel Informationen
- Bottleneck: Viel Traffic bei RCC mögliches Bottleneck
- Aging: Nahe Router erfahren schneller von Änderungen

## Isolated Adaptive Routing

Routing wird nur mit lokalen Informationen gemacht

### Hot potato routing

- Paket wird so schnell wie möglich weitergeleitet (eigener port mit kleinster Warteschlange)

### Backward Learning Routing

- **Grundidee:**
    - Die Quelladresse und der Hop-Zähler werden in den Paketköpfen markiert. Router sammeln diese Daten, wenn Pakete vorbeikommen.
    - Router lernen (aktualisieren) ihr Wissen über das Netzwerk allmählich durch das Durchlaufen von Paketen.
- **Algorithmus:**
    - Router werden mit leeren Routing-Tabellen initialisiert.
        
    - Starten Sie mit dem Zufallsrouting (Hot Potato oder Flooding) und für jedes Paket:
        
        1. Wenn der Hop-Zähler == 1 ist, stammt das Paket von einem direkt angeschlossenen Knoten.
        2. Für Pakete mit Hop-Zähler n>1 befindet sich die Quelle n Hops entfernt (hinter der Eingangsverbindung).
    - Ständig den Hop-Zähler für jede Quelladresse mit dem minimal bekannten Hop-Zähler vergleichen; lernen, wenn ein neuer niedriger ist
        
        > bessere Route (Verbindung) zu diesem Ziel
        
    - **Bemerkung:** Um sich an die Verschlechterung von Routen (z. B. Linkfehler) anpassen zu können, muss die erworbene Information periodisch "vergessen" werden ("Soft-State").
        

## Distributed Adaptive Routing

### Welche Arten gibt es?

Dezentralisiert

- Router tauschen Informationen mit Nachbarn aus und berechnen selbst die Routen
- Beispiele: DVR (RIP und BGP)

Global

- Alle Router kennen das gesamte Netz
- Beispiel: LSR (OSPF und Dijkstra)

Statisch

- Routen verändern sich nur sehr langsam

Dynamisch

- Routen verändern sich schnell
- periodische Aktuallisierung und Reaktion auf Netzveränderungen

### Distance Vector Routing

1. Jeder Knoten hat eine eigene Routing Tabelle, die zu Beginn nur die Distanz zu den direkten Nachbarn hat
2. Jede Runde sendet jeder Knoten wenn es Änderung gab seine Tabelle an seine Nachbarn und aktualisiert die Werte

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f0371a72-631d-43ba-ab5b-326ddd75e086/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f3459152-0f53-4b92-b578-ad8eaee25dde/Untitled.png)

### Was tun gegen Count to infinity bei DVR Problem?

**Poisoned Reverse**

Wenn ein Knoten X den Nachbarknoten Y f ¨ur seine k ¨urzeste Route zu Z benutzt, schickt er an Y die Information, dass sein Abstand zu Z ∞ ist (damit Y nicht versucht, ¨uber X zu Z zu gelangen)

**Split Horizon**

Wenn ein Knoten X den Nachbarknoten Y f ¨ur seine k ¨urzeste Route zu Z benutzt, schickt er keine Informationen ¨uber seine Route zu Z an Y

### Link-State Routing (LSR)

1. Jeder Knoten flutet das Netzt mit seiner Routing Tabelle (nur direkte Nachbarn)
2. Danach mit z.B. Dijkstra kürzeste Pfade berechnen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/00209570-b0eb-4850-a7a1-659be1050fa8/Untitled.png)

### Dijkstra

Gegeben: Graph und Startknoten

1. Initalisierung: Gewicht zu allen anderen Knoten ist unendlich
2. Distanz zu den Nachbarn eintragen; Startknotent als Vorgänger eintragen; Startknoten als besuchten Knoten eintragen
3. Zu dem Knoten gehen mit der geringsten Distanz; Distanz des Startknoten zu den aktuellen Nachbarn eintragen; aktuellen Knoten als Vorgänger eintragen; aktuellen Knoten als besuchten Knoten eintragen
4. repeat

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/431b730b-2563-4fd1-afb8-c3a0b230bb9d/Untitled.png)

- P_i := Vorgänger Knoten von Knoten i
- C_i := Kosten um vom Startknoten zu i zukommen

### LSR vs. DVR

**Message complexity**

- **Link state (LS):** With n nodes and E links, O(n*E) messages are sent each time.
- **Distance vector (DV):** Only exchange between neighbors.

**Speed of convergence**

- **LS:** n times execution of O(n^2) algorithm (requires O(n*E) messages, see above).
    - May lead to oscillations (if link cost is adjusted to heavy traffic changes or if heavy traffic renders links unusable).
- **DV:** Convergence time varies.
    - May lead to routing loops.
    - Count-to-infinity problem.

**Robustness**

- **LS:**
    - Node can advertise incorrect link cost.
    - Each node computes only its own table.
- **DV:**
    - DV node can advertise incorrect path cost.
    - Each node's table is used by other routers.
    - Errors propagate through the network.

# Routing im Internet

- Internet besteht aus AS um die Probleme von Skalierung und administrativer Autorität zu lösen.
    - Stub-AS sind kleine Unternehmen mit einer Verbindung zum Internet
    - Multihomed-AS große Unternehmen mit mehreren Verbindungen zum Internet (keine Transitdienste)
    - Transit-AS sind Internet Provider
- AS Router muss nur Routen innerhalb seines AS und Routen zu anderen AS wissen

Routing im Internet erfolgt auf zwei Ebenen

- Intra-AS-Routing: Admin wählt Routing-Protokoll (z.B. RIP, OSPF und IGRP)
- Inter-AS-Routing: Einheitliches Routing-Protokoll (BGP)
- Gateway Router implementieren beide Protokolle und ermöglichen die Komm. nach Außen

**RIP (Routing Information Protocol)**

- Distance-Vector-Routing-Protokoll
- einfaches und leicht zu implementierendes Protokoll, aber es ist nicht sehr skalierbar

**OSPF (Open Shortest Path First)**

- Link-State-Routing-Protokoll
- zuverlässigeres und skalierbareres Protokoll als RIP und komplexer
- bevorzugte Wahl für große Netzwerke

**BGP (Border Gateway Protocol)**

- Path-Vector-Routing-Protokoll (DVR)
- wird für das Inter-AS-Routing verwendet
- komplexes Protokoll, aber es ist die bevorzugte Wahl für die inter-AS-Routing, da es die Möglichkeit bietet, die Routen zu priorisieren und zu filtern.

## Was ist der Vorteil von verschieden Protokollen (Hierarchisches Routing)?

**Skalierung**

- spart Speicherplatz in der Routing-Tabelle
- einfachere Aktualliserung der Einträge (weil weniger)
- bessere Leistung (weil weniger Aktuallisierungsverkehr)

**Richtlinien**

- AS sind unabhängig und Admins daher flexibel

**Leistung**

- Intra-AS kann sich auf Leistung fokusieren
- Inter-AS ist flexibel

# Dynamic Source Routing

- RREQ: Route Request (broadcast) := Wird an alle Knoten gesendet um eine Route zu finden
    - RREQ(ID, 1,10,{1,3,5}) enthält ID, Sender, Ziel und bereits genommener Pfad
    - Wird von Knoten verworfen wenn ID schonmal gesehen wurde (noch im Cache)
- RERR: Route Error (unicast)
    - Wenn ein für die Route des Packets benötigter Link kaputt ist
    - Wird an Sender gesendet. Sender löscht alle cached paths und sollte dann RREQ senden
- RREP: Route Reply (unicast)
    - RREP(10,1,{3,5,9,10}) enthält Sender, Ziel und Route
    - Wenn RREQ Ziel erreicht sendet dieses eine RREP direkt an der Sender der RREQ

# Stretchfaktor

minimale Anzahl Sprünge in OVERLAY / minimale Anzahl Sprünge in UNDERLAY

# Border Gateway Protocol (BGP)

- AS bekommt von anderen AS Informationen über die erreichbaren Routern über anderes AS
- AS gibt diese Information an Router innerhalb des AS weiter
- “Gute” Routen zu Subnets werden festegelegt


# Internet Namen und Adressen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f920d6c3-4e8b-4b73-af57-5f403b62bf5d/Untitled.png)

# IP Header

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b0a8a7d1-319a-4382-af52-d697854ac5c8/Untitled.png)

# IP Address Classes

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/38d542ef-cd19-4ece-91a0-1b6b5c915e0b/Untitled.png)

# Special Addresses

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5cf4d0cb-0939-4037-8423-f41efda1634f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4fd0fe7-0079-4679-9162-2eaf492c8ab7/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2e959fd-9132-4cc5-9672-c7ea47e8c117/Untitled.png)

# Subnetzte

- Verbindungen von Router trennen → Anzahl Subnetzte (einzelne Kabel zwischen Routern zählen auch)
- Hostteil von IP-Adresse wird nochmal aufgeteilt
    - Subnetzteil hat feste Länge (ein Oktet)
    - Class A maximal 2 Subnetz Level und Class B maximal 1 Level
    - Anzahl der addresierbaren Hosts pro Subnetz ist gleich

## Variable Length Subnet Masks (VLSM)

- Keine Beschränkung mehr auf Oktete sondern Subnetzteil von nur einem Bit möglich
- Ermöglich Classless InterDomain Routing (CIDR)

## Classless InterDomain Routing

- Keine Klassen sondern beliebige Netzwerkteil
- a.b.c.d/x → Netzwerkteil der Länge x

# Route Aggregation

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8485cdd-d6db-473e-b4a1-baf259a94884/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7519ba01-b468-4358-b37b-ad6cc07cba98/Untitled.png)

200.23.18.0/23 wechselt ISP. Durch longest Prefix Matching Routing klappt alles, weil ISPs R USs spezifischeren Eintrag hat

# Wie bekommen Hosts ihre Adressen?

- statisch
- DHCP (Neuer Host stellt Request)

# Network Address Translation (NAT)

- sparrt IP Adressen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/408632ea-1f0f-4dde-8824-6e7058dfbb30/Untitled.png)

# Address Resolution Protocol (ARP)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/db82e2a0-8c97-4054-beef-1a07fc01c7c2/Untitled.png)

# (Virtually) no transport protocol provides

the following two protocol functions!

- Delay guarantees
- Bandwidth guarantees

# SDU, PCI und PDU (Segmentation/Reassembly)

PDU einer höheren Schicht wird von unteren Schicht verwendet und wird zur SDU dieser Schicht (Wenn zu groß wird aufgeteilt (Segmentierung)).

Service Data Unit (SDU): enthält Daten für bestimmte Schicht

Protocol Control Information (PCI): Control Informationen für bestimmte Schicht

Protocol Data Unit (PDU): Besteht aus SDU und PCI

# Wie reden Prozesse miteinander?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e4f4cd06-c270-4b41-aa15-0de9ea6a97ac/Untitled.png)

# Multiplexing/Demultiplexing

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9cd9c041-e3e8-4ea9-a383-3042392bffce/Untitled.png)

# Wie werden Prozesse eindeutig identifizieren

- OSI will nur PID benutzt
    - geht aber nicht, weil PIDs willkürlich udn wechseln
- Internet benutz aber PID und IPs
    - verletzt OSI Modell

# Bestimmte Ports

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e168993-5886-40d7-bacd-a0a81a554d6d/Untitled.png)

# Data Transfer Service Element/Release

# Three-Way-Handshake

# Flow Control

- Beschützt den Empfänger vor Überlast
- Kompliziert auf Transport Layer (Prozesse blockiern, PDUs haben verschiedenen größen)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4ba2da13-d24f-4564-a179-13b67ed2adf5/Untitled.png)

# Error Control

ARQ

# Congestion Control

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7970a42c-32bb-4ba1-a5dd-a91af5162651/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30df31f0-b406-4ddd-97b7-ee659f278858/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1116b74-2933-45e5-ba81-6da6c0270c4c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f1a4086a-7d53-4677-9fde-3541cd484339/Untitled.png)

## Proactive Actions wenn Router fast voll

- Choke Packets
    - kann Netzwerk noch mehr überlasten
- Warning Bits
- Random Early Detection RED
    - Dropped Pakete

# TCP (COTS)

Verlässliche, langsame und geordnete Übertragung

-Congestion control

-Flow control

-Connection setup / tear-down

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0f652b86-602c-4f6b-a3ca-4c431942268a/Untitled.png)

- Cumulative ACK

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b0b6684b-f570-491a-a776-f259ed2f39cb/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/30e08382-54fb-4ba6-82f0-92161b215ec0/Untitled.png)

# UDP (Connectionless)

Schnell, ohne Reihenfolge und unzuverlässig

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a855c24e-3739-4b6b-8fc8-4945efc6e366/Untitled.png)

# Internet Port und Socket Concept

Sockel (Prozess) wird durch IP-Addresse und Port Nummer identifiziert (verletzt OSI-Schicht)

# Prozess Adressierung (OSI vs. Internet Ports)

## OSI

# Connection Control (COTS)

1. Connection establishment phase (Connect)
2. Data transfer phase (Data)
3. Connection release phase (Disconnect)


# Kendall’s Notation

Format: A/S/m/N/K/SD

- A = Ankunftsprozess
- S = Serviceprozess
- m = Anzahl der Server
- N = Plätze im System (beschränkte Warteschlangenlänge), wenn nicht angegeben, dann angenommen 
- K = Populationsgröße (wir werden diese in CNuvS nicht berücksichtigen)
- SD = Warteschlangendisziplin (siehe oben, normalerweise FCFS)

Für A und S wird die folgende Notation verwendet:

- M = Exponentieller Prozess (M = Markovian)
- D = Deterministisch
- G = Allgemein


# Verschiedene Arten von Kommunikation

## Unicast

- Ein Sender und nur ein Empfänger

## Broadcast

- Ein Sender und alle anderen empfangen

## Multicast

- Ein Sender sendet an wohldefinierte Gruppe
    - Darf jeder Sender und Empfänger sein
    - Offene oder geschlossesene Gruppe? (closed Bedeutet Prozess muss Gruppe zuerst beitreten um zu senden)

# Verschiedene Arten von Multicast

## Multicast via unicast

Quelle sendet N Datagramme für alle N Empfqnger

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/523f0eb2-20b0-4028-b662-e2e844e89980/Untitled.png)

## Networking multicast

Quelle sendet nur eine Nachricht und Router dupliziert

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/735c00a3-d3cc-4761-9155-91197011bd0b/Untitled.png)

## Application-Layer multicast

Der Empfänger muss das Packet duplizieren und weiterleiten

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16bfc864-b20a-4406-868e-3eb25d5db0e3/Untitled.png)

# IP Multicast

- Multicast wird an Multicastgruppe addressiert
- Router kömmert sich um das weiterleiten an alle Mitglieder
- IP selbst speicher keine Liste der Mitglieder
- Gruppen werden IGMP verwaltet

Adressen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e3f47fff-223d-4fd7-b8a6-fb88b6f64c5b/Untitled.png)

## Übertragung der IP Multicast Datagramme

Lokale Zustellung

- Multicast addresse wird auf ethernet mulitcast adresse abgebildet

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2e7ccac-882d-4273-8653-4a348c578c74/Untitled.png)

Übers Internet

- Router Delivery trees werden aufgestellt mit Multicast Routing Protokoll
- Jeder Router hat zudem benutzt group membership protocoll (IGMP) um über seine lokalen Gruppen bescheid zu wissen

## Wie können Hosts einer Gruppe beitreten?

Router sendet immer wieder ein IGMP um zu überprüfen ob Host noch in Gruppe oder Host melden sich selbst

Lokal (IGMP)

- Host informatiert Router über beitritt

Wide area

- Router muss mit anderen Routern interagieren um mcast zu erhalten

# Multicast Routing

### Flooding

- Kein Baum nötig
- Ineffizient
- Router müssen sich Paket IDs merken

### Group-shared trees

- Alle Sender benutzen den selben Baum (keine Schleifen)
- Minimal spanning trees MST (Steiner)
    - Benutzt man nicht (zu komplex)
- Core based trees CBT

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9077da85-a4ff-4bc3-9657-a950a62de050/Untitled.png)

### Source-based tree

- Sender benutzen verschiedenen Bäume
- Shortest path trees SPT
- Reverse path forwarding RPF

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/186735bc-10bd-4038-9b3c-d6ad164ef116/Untitled.png)

## Core Based Routing (shared tree)

- Ein Core Router über den alle Pfade gehen (viel Traffic)
- Baum wird Stück für Stück aufgebaut (wenn Paket auf den bereits vorhanden Baum stoßen wird der “Ast” angefügt)
- Kann Suboptimal sein

## Shortest path tress (sourced-based tree)

- benutzt einfach Dijkstra

## Reverse path forwarding (source-based tree)

- Wissen der Router wird verwendet (unicast routing table)
- Wenn Router ein mcast Datagramm über den kürzesten Weg vom Sender erhält wird das Datagramm an alle gefloodet
- sonst nicht
- Wenn Router keinen Host haben die in der Multicast Gruppe sind wird eine prune message zurückgesendet


# Was ist eine distributed Application?

- System, dass aus mehreren miteinander kommuniierenden Teilen besteht (PC mit mehreren Prozessen die über OS miteinander reden)
- Systeme mit Parozessen die über Netzwerk reden (kommunikation wieder über OS)

# Was genau wird verteilt?

- Daten
- Computation
- User

# Client Server Model

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3285da1d-c568-474a-97bd-ed69a865d796/Untitled.png)

## Iterative Servers

- Server verarbeitet jeweils nur eine Request (nichts gleichzeitig)

## Concurrent Servers

- Kann Request gleeichzeitig abarbeiten

# Beispiele für Server

## DNS Domain Name System

- verteilte Datenbank um Namen aufzulösen
    
- ist hierachisch organisiert (com, org, edu, …)
    
- Root Name Server wird konktakitiert falls Name nicht auflösbar; dieser leitet dann immer weiter
    
- Einträge in DNS sind Resource Records
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fde0c4da-18d2-458f-9ae9-93f619d10e90/Untitled.png)
    
    ### Arten von Anfragen an DNS
    
    Iterative
    
    - Host schickt Anfrage
    - Host bekommt gesagt wo er als nächstes Fragen soll wenn die Anfrage nicht erfolgreich war
    
    Rekursive
    
    - host schickt Anfrage
    - der angefragte regelt alles und gibt dann Antwort zurück

## WEB / HTTP 101

- nutzt TCP
- Zustandslos (kann mit Cookies überwunden werden)
- HTTP/1.0 muss für jedes Objekt neue TCP Verb. aufbauen (nonpersistent)
- HTTP/1.1 kann mehrere Objekte aufeinmal anfragen


# Übungen
# Multiplexing

## Time Division Multiplexing (TDM)

- Mehrere Nutzer verschicken **Datenpakete** über eine **geteilte physische Verbindung**
- Jeder Nutzer bekommt einen **anderen Zeitslot** zugeteilt

## Frequency Division Multiplexing (FDM)

- Mehrere Nutzer benutzen eine Verbindung, aber mit verschiedenen Frequenzen.

## Code Division Multiplexing (CDM)

- Die gesendeten Daten werden mit einem Spreizcode multipliziert, dadurch können mehrere Nutzer gleichzeitig über die gleiche Verbindung senden.

## Space Division Multiplexing (SDM)

- Es gibt mehrere Verbindungen zwischen Host und wenn Daten übermittelt werden wird eben ein Kabel eingenommen.

# OSI Schichten

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ceec5d58-5e5a-44eb-a898-2b0b2235cd0d/Untitled.png)

# OSI vs TCP/IP Layer

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a8645ed-de3a-4b17-98a6-959d8827ca6c/Untitled.png)

# Link State Routing vs. Distance Vector Routing

- LSR erzeugt großen Netzwerkverkehr durch das Flooding (exponentielles Wachstum)
- Im DVR kann count-to-infinity Problem auftreten
- Kann bei LSR nicht auftreten weil nur lokale Knoten informiert werden

# Checksum

1. Alle 16 bit wörter addieren
2. Übertrag auf LSB addieren
3. Komplement bilden

Wenn der IP Header mit Checksum addiert wird sollte 0 rauskommen damit Übertragung richtig war

# Classfull

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/02df16fa-64a3-4ac7-84f2-6d8302f661a7/Untitled.png)

# Networkpart, Subnet, host part

Class C IP: 207.63.71.12/27

- Class C also 24 Bit Netzworkpart
- 27 - 24 = 3 also 3 bit Subnetpart
- 32 - 27 = 5 also 5 bit host part

# Classfull vs classless

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c833d068-1fb5-44cd-8953-b466f068c0b0/Untitled.png)

# IP Address Aggregation

# Demultiplexing in the Internet

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7aee2103-633b-40ba-9280-30cfd4f2ab8d/Untitled.png)

# Two Army Problem

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4b76f18c-5f28-44bd-bd0c-3a33baa3d19d/Untitled.png)

# SDU, PCI und PDU

PDU einer höheren Schicht wird von unteren Schicht verwendet und wird zur SDU dieser Schicht (Wenn zu groß wird aufgeteilt (Segmentierung).

Service Data Unit (SDU):

-enthält Daten für bestimmte Schicht

Protocol Control Information (PCI):

-Control Informationen für bestimmte Schicht

Protocol Data Unit (PDU):

-Besteht aus SDU und PCI

# OSI vs Internet Ports

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ae2da5e9-74dd-4293-88b0-6177d8a77b53/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/366e1430-c11b-454d-af3a-67d64d547853/Untitled.png)

# OS, Prozesse und Protokoll Ports

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/34815f69-c5eb-43af-abbc-aca14e4f9a1e/Untitled.png)

# Port Ranges

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dfd0a7af-324f-4abc-b35f-836c1f87e267/Untitled.png)

# Flow Control

Managed die Übermittlungsrate zwischen zwei Knoten und beschützt langsame Empfänger for überlastung.

Probleme auf Transportschicht:

- PDUs haben verschiedene Größen
- Prozesse benutzten die Transportschicht und diese können blockieren wenn sie auf andere Resourcen warten
- Der Empfänger muss Nachrichten zwischenspeichern

Rate-based:

- Jeder Knoten bekommt durchschnittliche Übertragungsrate zugeteilt
- Gut für high-speed-networks

Window-based:

- Übertragung wird an window größe bzw. Rückmelderate angepasst
- hohes feedback delay

# TCP vs. UDP

TCP

- Überprüft ob Pakete ankommen
- Überträgt jedes Paket mit Sequenznummern

UDP

- Überprüft NICHT ob Pakete ankommen
- Hat keine Sequenznummern
- Schneller (keine Flow Control oder Congestion Control)
- Verlorene Packte werden nicht neuübertragen
- Weniger Overhead durch simplen Header im Vergleich zu TCP
- no connection management (flow control, message acknowledgements, packet ordering)
- no congestion control/flow control (can overwhelm the network if not implemented manually)

# QUIC

- Efficiency/Low latency: QUIC combines TCP and TLS handshake. This reduces the setup time of a connection.
- Use of streams: Data is organized in streams. Streams don’t block other streams if packets get lost.
- QUIC uses UDP for sending and receiving data. In addition, QUIC establishes a reliable connection. It’s necessary to use UDP because middleboxes inspect IP packets. The middleboxes block unknown Transport Layer protocols. With the use of UDP, middleboxes don’t need to know the QUIC protocol.

# TCP: Flow Control vs. Congestion Control

Additive Increase Multiplicative Decrease (AIMD) scheme

Flow Control:

- Flow control is mainly done on the receiver side, to adjust how much data the sender is injecting into the network.

Congestion Control:

- Congestion control is mainly done on the sender side, trying to sense congestion on the network by the timing of ACK-Packets to adjust the volume of data sent to the corresponding situation.

# TCP: Congestion Control

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a161921a-0312-4f94-b1bc-487667897f76/Untitled.png)

## Phases

### Slow Start Phase

- exponentielles Wachstum des Congestion Window (für jedes ACK Fenster + 1)
- Verbindung erreicht dadurch schneller das Maximum
- Kein additive increase weil es lange dauern würde
- Endet wenn threshold ist erreicht

### Congestion Avoidance Phase

- Ab threshhold nur noch lineares Wachstum des windows
- Endet wenn dreimal ein ACK für selbes Paket kommt oder timeout
- inccw(n) = MSS * (MSS / sizecw(n))
- sizecw(n) = sizecw(n - 1) + inccw (n)

### After Timout

- Threshold wird auf die Hälfte des Windows gesetzt
- Und Window wird auf 1 MSS gesetzt

### After triple ACK

- Threshold wird auf die Hälfte des Windows gesetzt
- Window Size wird auf Threshold gesetzt

# Retransmission Scenarios

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb47ab57-0090-4335-a3f0-fe9b203cbe30/Untitled.png)

Acknowledgement für Paket geht verloren -> Paket wird neu übertragen.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4db23075-183e-4b16-8f12-664417ce9278/Untitled.png)

Sender schickt Pakete 1,2,3,4,5 und Paket 2 geht verloren. -> Empfänger schickt ACK für Paket 1 und schickt duplicate ACK für Paket 2 für jedes weitere ankommende Paket, bis Paket 2 endlich da ist. Wenn das Paket erfolgreich übertragen wurde, wird sofort ein ACK für Paket 5 geschickt.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c8e47913-18bf-41c7-af2e-2cf9814d903e/Untitled.png)

Zwei Pakte werden gesendet und einzeln acknowledget, wobei das ACK vom 1. Paket wegen Timeout verloren geht. -> Sender übermittelt 1. Paket erneut und Empfänger bestätigt Empfang von Paket 1 und 2.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/80d825e5-8151-41ff-914c-e1a1ef500883/Untitled.png)

Paket wird gesendet und ACK geht verloren, aber Sender schickt bereits ein neues Paket. -> Empfänger schickt einfach ACK für beide Pakete.

# Nagle’s Algortihm

Small messages can cause the network to be overloaded. This Problem can be dealt with by using Nagle’s Algorithm. Nagle’s Algorithm buffers data until either the packet has reached its maximum size or there is no unacknowledged/unconfirmed data in the pipe.

# Proactive Algorithms

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/59373f9f-d175-4460-838d-1ad4b810dda0/Untitled.png)

RED nimmt an, dass all dropped packets are caused by congestion or a congestion avoidance mechanism. If packets are dropped for a different reason, like a faulty link or an unstable connection like WiFi, the transmission rate is reduced unnecessarily.

# Queueing

## Was ist M/M/m

- Modell mit m Servern
- Verteilung von Paket Ankunft und Service sind “Markovian” bzw. exponential

## Was sind Markov Prozesse

- Stochastischer Prozess
- Nächster Zustand hängt nur vom aktuellen ab
- Zustandsübergang ist unabhängig von der Beobachtungszeit des aktuellen Zustands sein
- Prozesse müssen memoryless sein, das bedeutet, dass der nächste Zustand unabhängig von der verbrachten Zeit im vorherigen Zustand ist
- Die Verteilung der Prozesszeiten ist hierbei exponentiell verteilt

## Was ist ein Birth-Death Prozess

- Ist ein Markov Prozess
- Übergänge sind nur zu direkten Nachbarn möglich also k kann zu k+1 und k-1

# Multicast

## Multicast via unicast

Quelle sendet N Datagramme für alle N Empfqnger

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/523f0eb2-20b0-4028-b662-e2e844e89980/Untitled.png)

## Networking multicast

Quelle sendet nur eine Nachricht und Router dupliziert

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/735c00a3-d3cc-4761-9155-91197011bd0b/Untitled.png)

## Application-Layer multicast

Der Empfänger muss das Packet duplizieren und weiterleiten

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16bfc864-b20a-4406-868e-3eb25d5db0e3/Untitled.png)

## routing and delivery for multicast

Flooding

Group-shared tree

Source-based tree

## Steiner Trees

- Braucht Informationen des gesamten Netzwerkes
- Muss rerun wenn router joint oder leaved

## Wie tritt man einer Multicastgruppe bei?

Internet Group Management Protocol (IGMP) wird verwendet

Host:

- Send IGMP report when application joins mcast group
- Send Host Membership Report msg to indicate group membership

Router

- Periodically send IGMP/ Host Membership query

## Welche IP für Multicast

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4156d06a-5529-4a72-b4fe-916d8c55e931/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/beb5007d-bd38-41eb-b2d3-5556a778dc31/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7266f61f-d0ef-409d-9e4c-f41478e4a1b2/Untitled.png)

## Warum werden ACKs für reliable Multicast nicht verwendet?

- ACKs in multicast can cause an “ACK explosion” overloading the receiver.
- As the multicast delivery is (assumed to be) mostly successful, negative acknowledgement (NACKs) are used to indicate a non-delivery (and cause re-transmission).

# Was sind verteilte Systeme?

Systems of combined, communicating components. Basis: Inter Process Communication (IPC) over physically “long” distances

Pros:

- Allows for remote resource utilization

Cons:

- Communication channels may have adverse properties
    - Delay
    - Jitter
    - Faulty transmission
    - Packet loss
- These properties can hardly be hidden from application developer completely

# Open vs. proprietary protocols

Open protocols (HTTP, FTP, SMTP)

- open specification available to everyone
- Goal: different implementations by different groups/vendors can interoperate
- most protocols commonly used in the Internet are defined in RFCs

Proprietary protocols (KaZaA, Skype, MS Exchange)

- defined by a vendor without intent to make it “open”
- hence, specification often not publicly available

# Socket API operations

The socket API is similar to the file access API.

A connection is always defined by a socket pair, and fully defined by 5‐tupel: (protocol, local‐address, local‐process/local-port, foreign‐address/foreign port, foreign‐process)

connection-less protocols

- create
- open (bind)
- read (recv)
- write (send)
- close

connection-oriented protocols

- create
- open (bind)
- read (recv)
- write (send)
- close
- listen
- accept

# DNS

## Services

- Hostname zu IP addresse translation
- Host aliasing (Canonical and alias names)
- Mail server aliasing
- Load distribution - Replicated Web servers: set of IP addresses for one canonical name

## Typen von DNS-Servern

### Authoritative Servers

- maintain authoritative content of a complete DNS zone
- are pointed to in the parent zone as authoritative
- can serve as load balancers

### Recursive (Caching) Server

- serve as local proxies for DNS requests
- cache content for specified period of time (soft‐state with TTL)
- process requests recursively if data is not in the cache

### Resolvers

- run on client’s machines (part of the OS)
- delegate request to local server
- support recursive requests only (no support for iterative requests)

## Zentraler DNS?

Schlecht, weil

- Single point of failure
- Traffic volume
- Distant centralized database
- Maintenance does not scale!

## Wie sieht eine DNS anfrage aus für [www.google.com](http://www.google.com)

1. Client queries a root server to find com DNS server
2. Client queries com DNS server to get [google.com](http://google.com/) DNS server
3. Client queries [google.com](http://google.com/) DNS server to get IP address for [www.google.com](http://www.google.com/)

## Was bringt ein Cache

- schnellere Antwortzeiten
- Weniger Network Traffic
- Offline verfügbar
- Mehr Sicherheit

## Mögliche Bedrohungen für DNS

- Data corruption
- Impersonating master
- Impersonating cache
- cache pollution
- Altered Zone data
- Unauthorized updates

## Was bringt DNSSEC

Verhindert

- Impersonating master
- cache pollution
- Altered Zone data

# HTTP

## Was machst HTTP/2 besser zu HTTP/1.0 und HTTP/1.1

- Multiplexing: Group several requests in a single connection where responses are sent back in any order.
- Server-initiated pushing of content.
- Stream priority (dependency levels between requests).
- Data compression (now including header, which is often highly redundant).

## Client/Server model

- Client: Browser that requests, receives, “displays” Web objects
- Server: Web server sends objects in response to requests

## Nonpersistent and Persistent HTTP

Nonpersistent

- At most one object is sent over a TCP connection
- Requires 2 RTTs per object.
- OS must work and allocate host resources for each TCP connection.
- HTTP/1.0 uses nonpersistent HTTP

Persistent

- Multiple objects can be sent over single TCP connection between client and server.
- Server leaves connection open after sending response
- Subsequent HTTP messages between same client/server are sent over connection
- HTTP/1.1 uses persistent connection in default mode

## TTP response codes

- 403 Forbidden: Access is permanently blocked.

## Was machen eigentlich Cookies?

HTTP as such is a stateless protocol. Cookies are used to enable state tracking in HTTP sessions. This enables, among others:

- Authorization
- Shopping carts
- Recommendations
- User session state (e. g. for Web e‐mail)

## GET /somedir/page.html HTTP/1.1

- The GET method is used to retrieve or fetch a resource from the server. It is one of the most common HTTP methods and is primarily used for retrieving data.
- /somedir/page.html is the path to the desired resource on the server. In this case, it is requesting a resource called ”page.html” located within the ”/somedir” directory
- The HTTP version indicates the protocol being used for the request. In this case, it is HTTP/1.1.

# Longest Prefix Matching



# Altklausuren

# Themen

## SoSe 2022

Was ist Duplex

Was ist Informationen, Daten und Signalen

Was sind verteilte Systeme

Was ist ein Kommunikationsprotokoll

Netwerk Downloadrate usw.

DVR

Count to infinity

LSR

Overlay Routing (Stretchfaktor)

DSR

Warum brauchen wir NAT?

Subnetzmaske berechnen

Warum ist Classfull kacke

Wie groß sind die Subnetze, wenn …

IP in Bit, Hex und Dec

Spezielle IP Adressen (127.0.0.0/8)

Was machen die OSI Schichten

Was macht AIMD

Congestion Windows Size berechnen nach X ACKs

TCP Flow Control (Uhrenaufgabe)

Lamport Clocks

Multicast Algorithmen (Flooding, Group und Source based)

Multicast Duplizierungsarten

Wann wird Unicast, Multicast, Broadcast verwendet

Two Army Problem

Schneeballeffekt der Congestion Control

Baum in CBT, schnellste Route bestimmen

Warteschlangen Rechenkram

Was ist DNS

Client/Server Modell

negative Aspekte von Kommunikationsprotokollen auf Application Layer

Unterschied persistent/nonpersistent HTTP

## WiSe 22/23

Definition Socket

TCP UDP

Multicast, Unicast, Broadcast

Count to infnity (warum nicht bei LSR)

Dateneinheiten (Paket, Datagramm, …)

Informationen, Signale, Daten

Bekannte Ports nennen

UDP vs. TCP

Was ist ein Kommunikationsprotokoll

Up- vs. Downwards Multicasting

Window berechnen

Subnetzmaske und CIDR

Warum ist classfull kacke

spezielle IPs

ARP-Verfahren

Wie kann ein Host seine MAC-Adresse herausfinden

IPv4 und IPv6 Tunnel

LSR

Overlay Routing

Sliding Window

Warteschlangen



# Hilfsblatt 

# Algorithmen

## Lamport Clocks

- Clock wird bei jedem Event um 1 erhöht
- Außer es ist ein empfangenes Event, dann wird das Maximum von der eigenen Clock und der des gesendeten Events genommen und um eins erhöht. Das ist dann die neue Clock

## DVR

1. Jeder Knoten hat eine eigene Routing Tabelle, die zu Beginn nur die Distanz zu den direkten Nachbarn hat
2. Jede Runde sendet jeder Knoten wenn es ein neues Minimum gibt seine Tabelle an seine Nachbarn und aktualisiert die Werte

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f0371a72-631d-43ba-ab5b-326ddd75e086/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f3459152-0f53-4b92-b578-ad8eaee25dde/Untitled.png)

## LSR

1. Jeder Knoten flutet das Netzt mit seiner Routing Tabelle (nur direkte Nachbarn)
2. Danach mit z.B. Dijkstra kürzeste Pfade berechnen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7d713914-94c1-4e3c-9b59-0bb446e6da63/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7da3f626-df86-445c-8014-426bd0546cd5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b1f256ff-7fca-40bb-bd59-f06836e795df/Untitled.png)

## Dijkstra

1. Initalisierung: Gewicht zu allen anderen Knoten ist unendlich
2. Distanz zu den Nachbarn eintragen; Startknotent als Vorgänger eintragen; Startknoten als besuchten Knoten eintragen
3. Zu dem Knoten gehen mit der geringsten Distanz; Distanz des Startknoten zu den aktuellen Nachbarn eintragen; aktuellen Knoten als Vorgänger eintragen; aktuellen Knoten als besuchten Knoten eintragen
4. repeat

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/431b730b-2563-4fd1-afb8-c3a0b230bb9d/Untitled.png)

- P_i := Vorgänger Knoten von Knoten i
- C_i := Kosten um vom Startknoten zu i zukommen

## DSR

- Route Discovery wird gestartet wenn aktuell keine Route vorhanden ist
- Knoten verwirft Request wenn er bereits eine gesehen hatte
- Cache der Knoten merkt sich die Routen für alle KNoten die mehr als 1 Hop entfernt sind

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0065f926-b91c-4465-9154-cf33df386d14/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e1075f6e-c0c8-44db-84bb-a1138c616507/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d68d7338-b229-4148-a7fd-dd1abc6ed4dd/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25acebc0-635b-4a78-821a-0067f13c28f1/Untitled.png)

## Overlay Routing

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5edb8e9f-2378-4444-bc80-6ed9776151ce/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eb87b48f-0bfa-4a7e-aee2-bd2b217f2ae9/Untitled.png)

## Alternating Bit Protocol

Number of Packets := Data Size / Packet Size

Transmission Time per Packet := Packet Size / Data Rate

Transmission time per acknowledgement := Transmission Time per Packet **(sonst wie angegeben)**

Transfer Time := Number of Packets * (Propagartion Delay + Transmission Time per Packet + Propagartion Delay + Transmission time per acknowledgement)

Transfer Time (nur ein ACK am Ende) := Propagartion Delay + Number of Packets * Transmission Time per Packet + Propagartion Delay + Transmission time per acknowledgement

## Checksum

1. Alle 16 Bit worte aufaddieren (Übetrag auf LSB)
2. Komplement ist dann die Checksum

## TCP Flow Control

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe1b9360-8348-4ec9-89ec-9accbad5f6ff/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/45814ac3-8b8d-47ee-af61-f014dd7a1370/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/50bf70f0-6faa-4a26-a55a-bad22fd5fc40/Untitled.png)

## AIMD / Congestion Window

AI

- inccw(n) = MSS * (MSS / sizecw(n))
- sizecw(n) = sizecw(n - 1) + inccw (n)

## Queueing

$\lambda$ := Requests pro Zeiteinheit

$\mu$ := Responses pro Zeiteinheit

$\rho$ := average utilization

$T$ := average system time of requests

$N$ := average number of requests in the system

$p_n$ := Wahrscheinlichkeit, dass n Requests im System sind

$p_{0} \cdot t$ := average idle time in a intervall of t

## Three Way Handshake

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e64eaa2b-0beb-462a-982b-ce9d7516810f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ec5ecfb2-71cf-42fb-99a7-7a7591a91ba7/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f9cf6689-4cde-4cf3-b7dc-6731da4866df/Untitled.png)