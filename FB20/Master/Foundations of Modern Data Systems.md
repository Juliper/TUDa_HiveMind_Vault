---
aliases:
  - FOMO
tags:
  - fb20
  - master
  - pflichtmodul
  - semester-1
  - 6CP
  - klausur
  - master-informatik
  - status-in-bearbeitung
description: ""
---
## Überblick

## Kerninhalte

## Zusammenfassung

## Prüfungsvorbereitung

## Altklausuren


Backlog:

# Vorlesung 7: GPUs

### 1. Motivation & Trend
- **Multi-Core-CPUs skalieren kaum noch weiter**
- **Beschleuniger (Accelerators)** wie **GPUs, TPUs, FPGAs** werden immer wichtiger
- **GPUs** sind nicht nur für **KI**, sondern auch für **Datenbanken & allgemeine Workloads** dominant  
---
### 2. GPGPU – General Purpose GPU
- Ursprüngliche GPUs waren **nur für Grafik-Pipelines**
- **GPGPUs** sind für **allgemeine Rechenaufgaben**
- Design:
    - **CPU**: wenige, komplexe Kerne → **Latenz-optimiert**
    - **GPU**: sehr viele, einfache Kerne → **Durchsatz-optimiert**  
---
### 3. GPU-Architektur (Überblick)
- GPU besteht aus vielen **Streaming Multiprocessors (SMs)**
- Pro SM:
    - Recheneinheiten (CUDA Cores)
    - Register
    - L1-Cache & Local Memory
    - Recheneinheiten
	    - FP64, FP32,  INT, Tensor Core
- Gemeinsame Komponenten:
    - L2-Cache
    - Global Memory (HBM, sehr hohe Bandbreite)
- **GPU-Speicher kleiner als CPU-Speicher**, aber **viel höhere Bandbreite**  
---
### 4. CPU vs. GPU (Execution Model)

| CPU                    | GPU                         |
| ---------------------- | --------------------------- |
| Schwere Threads        | Sehr leichte Threads        |
| OS-verwaltet           | Kein OS                     |
| Unterschiedlicher Code | Alle Threads gleicher Code  |
| Latenz-fokussiert      | Durchsatz-fokussiert (SIMD) |

---
### 5. CUDA Programmiermodell

Es gibt auch OpenCL als GPU API
#### Grundbegriffe (sehr klausurrelevant!)
- **Kernel**: Funktion, die parallel ausgeführt wird
- **Grid**: Gesamtheit aller Threads
- **Block**: Gruppe von Threads auf einem SM
- **Warp**: **32 Threads**, kleinste physische Scheduling-Einheit (SM kann mehre ausfuhren)

> ⚠️ Warps sind **nicht explizit programmiert**, aber extrem wichtig!

---
### 6. Thread-Indizierung (Logisches Modell)
- `threadIdx` → Index innerhalb eines Blocks
- `blockIdx` → Block-Index im Grid
- `blockDim` → Threads pro Block
- Typische Formel:

```c
int idx = blockIdx.x * blockDim.x + threadIdx.x;
```
---
### 7. Warps & Branch Divergence
- **Alle Threads eines Warps führen dieselben Instruktionen aus**
- Wenn Threads in einem Warp unterschiedlich verzweigen:
    - → **Branch Divergence**
    - → Pfade werden **sequentiell** ausgeführt
    - → **Leistungsverlust**  

---
### 8. Physisches Execution Model
- **Pre-Volta**: Lock-Step-Ausführung (alle 32 Threads exakt synchron)
- **Volta und neuer**:
    - **Feingranulares Warp-Scheduling**
    - Teilmengen von Threads können interleaved werden
    - → Weniger Leerlauf, bessere Auslastung  

---
### 9. Latenz-Versteckung (Latency Hiding)
- Global Memory Zugriff: **~400 Zyklen**
- Idee:
    - Während ein Warp wartet → anderer Warp wird ausgeführt
- Faustzahlen:
    - ~6 Warps für Register-Latenz
    - ~100 Warps für Memory-Latenz
- **Viele Threads pro Block = wichtig**  
Rechnung:
- Warp schedule = 4 Cycles
- Register load data 24Cycles
- GLobal mem access = 400 cycles
- → 24/4 = 6 (heist 6 warps um register acc zu hiden)
- → 400/4 = 100 warps um mem accc zu hiden
- → Alle 8 cycles reg zugriff = 24/8 = 3 warps
- → Alle 8 cycle mem zugriff = 100/8 = 12.5

---
### 10. Memory Access & Stride
- **Speicherzugriffe sind der wichtigste Performance-Faktor**
- Best Case:
    - Threads eines Warps greifen **aufeinanderfolgend** zu
    - → **Memory Coalescing**
    - → 128 Byte = 1 Cache Line
- **Zu viele Threads** können **Occupancy senken** oder **Hardware-Limits** überschreiten
- Problemgröße ist oft **größer als sinnvoll startbare Thread-Anzahl**
- **Lösung:** Ein Thread verarbeitet **mehrere Elemente in einer Schleife**

---
### 11. Datenübertragung CPU ↔ GPU
- GPU-Speicher begrenzt → Daten oft in CPU-Memory
- PCIe-Bandbreite: **~16–64 GB/s**
- GPU Memory: **~900 GB/s**
- Zwei Modelle:
    1. **Run-to-Finish**: Alles passt in GPU
    2. **Batching**: Daten stückweise übertragen
- Ziel: **Datenübertragung und Rechnen überlappen**  

---
### 12. Regeln für GPU-Beschleunigung (Merken!)
#### GPU lohnt sich, wenn:
- Rechenintensiv
- SIMD-freundlich
- Daten passen (weitgehend) in GPU-Speicher
- CPU & GPU parallel arbeiten können
#### GPU lohnt sich NICHT, wenn:
- Kleine Datenmengen
- Hohe Latenzanforderungen
- Stark verzweigte / heterogene Berechnungen
- Sehr große, nicht partitionierbare Daten  

---
### 13. Klausur-Takeaways (Kurzliste)
✔ Unterschied CPU vs. GPU erklären können  
✔ Grid / Block / Warp sicher beherrschen  
✔ Branch Divergence erklären  
✔ Memory Coalescing & Stride verstehen  
✔ Warum viele Threads nötig sind (Latency Hiding)  
✔ Wann GPU sinnvoll ist – und wann nicht



# Vorlesung 8: Beschleuniger

### 1. Motivation: Data / Compute Gap
**Problem:**
- Datenmenge wächst schneller als Rechenleistung
- Klassisches Scale-up (stärkere CPUs) reicht nicht mehr

**Lösungen:**
1. **Mehr parallele Rechenleistung**
    - Verteilung, Many-Core, GPUs
2. **Effizientere Rechenleistung**
    - **Spezialisierung** (Accelerators)

👉 **Klausur-Merksatz:**
> Spezialisierte Hardware schließt die Lücke zwischen Datenwachstum und Rechenleistung durch höhere Energieeffizienz.

---
### 2. Was zählt als Specialized Hardware?
Beispiele:
- **Compute**: GPUs, TPUs, FPGAs, CGRAs
- **Netzwerk**: SmartNICs, Smart Switches
- **Storage**: Smart SSDs, Computational Storage
- **Motherboards** mit Spezialchips

---

### 3. Energieeffizienz vs. Flexibilität

|Hardware|Flexibilität|Energieeffizienz|
|---|---|---|
|CPU|sehr hoch|gering|
|GPU|hoch|besser|
|FPGA / CGRA|mittel|sehr gut|
|ASIC|gering|**extrem gut (~100×)**|

👉 **Trade-off:**
- **Mehr Spezialisierung → mehr Effizienz**
- **Mehr Flexibilität → weniger Effizienz**

---

### 4. Integration von Accelerators (sehr wichtig!)
#### 1️⃣ In-Data-Path
- Accelerator arbeitet **während Daten fließen**
- Kaum Datenkopien
- Beispiel:
    - SmartNICs
    - Computational Storage
- **Schwierige Integration**

#### 2️⃣ On-the-Side
- CPU besitzt Daten
- Accelerator bekommt Kopien
- Einfach zu integrieren
- **Hoher Data-Movement-Overhead**
- Beispiel:
    - GPUs, TPUs

#### 3️⃣ Co-Processor
- Accelerator arbeitet direkt auf CPU-Daten
- Sehr niedrige Latenz
- System stark spezialisiert
- Beispiel:
    - NPUs, Vector Units in CPUs

👉 **Typische Klausurfrage:**
> Welches Integrationsmodell minimiert Datenbewegung? → _In-Data-Path_

---

### 5. Wann lohnt sich Spezialisierung?

**Sinnvoll, wenn:**
- Großer Teil der Rechenzeit auf wenigen Operationen liegt
- Workload stabil & wiederkehrend
- Hoher Energieverbrauch mit CPUs/GPUs

**Beispiel: Google TPU**
- Ziel: **10× besseres Cost/Performance-Verhältnis als GPUs**
- Fokus: **Inference** (nicht Training)
- Ergebnis:
    - **83× effizienter als CPU**
    - **28× effizienter als GPU**

---

### 6. Warum TPUs so effizient sind
- Keine klassische Von-Neumann-Architektur
- Nutzung von **Systolic Arrays**
- Sehr gleichförmige, homogene Rechenstruktur
	- Skalierbar und effizenten silicon nutzung
	- mehr performance pro watt
- Fokus auf:
    - Matrix-Multiplikation
    - CNNs / DNNs

👉 **Merksatz:**
> Spezialisierte Hardware kann Rechenmodelle nutzen, die auf CPUs/GPUs ineffizient sind.

---

### 7. Programmierung von TPUs

- Nicht direkt programmiert
- Nutzung über **TensorFlow**
- Komplexer Software-Stack:
    - Compiler
    - Runtime
    - Driver
- **Integration ins Software-Ökosystem ist kritisch**
    - „Achillesferse“ vieler Forschungsprojekte

---

### 8. Reconfigurable Hardware

Gernell simple chip struktur -> Effiziente silicon nutzung und gute skalierbarkeit
#### FPGA (Field Programmable Gate Array)
- Fein-granulare Logikblöcke
- Bit-Level-Konfiguration
- Vorteile:
    - Sehr flexibel
    - Sehr energieeffizient
- Nachteile:
    - Komplexe Programmierung
    - Jede Codezeile belegt Chipfläche
#### CGRA (Coarse-Grained Reconfigurable Array)
- Wort-Level statt Bit-Level
- Domänenspezifischer
- Weniger flexibel als FPGA
- Effizienter für bestimmte Workloads
- Adaptive Intelligence Engines (AMD)
	- Systolic array mit VLIW
	- Mehr effizienz weil weniger chipflache fur instruciton kram und nur compute

👉 **Positionierung:**  
CPU ← GPU ← FPGA / CGRA ← ASIC

---

### 9. FPGA-Programmierung

#### Ablauf:
1. Code (HDL oder HLS) = definiert die hardware
	1. Hardware description languagem high level synthese
2. **Synthese** → Erstellt Darstellung mit Logikgatter
3. **Place & Route** → physisches Layout
4. Ergebnis: **Schaltkreis**
#### Eigenschaften:
- Alles wird **Hardware** (jede Code Zeile)
- Pipeline-Design sehr wichtig
- Latenz = Anzahl Pipeline-Stufen
- Frequenz begrenzt durch langsamsten Pfad

---

### 10. Wichtige FPGA-Beschleunigungstechniken

1. **Dataflow / Pipelining**    
    - FIFO-Puffer
    - Streaming
2. **Data Parallelism**
    - Mehrere Recheneinheiten parallel
3. **Custom Datatypes**
    - z. B. < 8 Bit
    - Multiplikationen werden drastisch billiger

👉 **Beispiel:** Regex Matching mit >1 B Zeichen/Zyklus

---

### 11. Regeln & Grenzen von Spezialisierung

#### CGRA/FPGAs and ASICs Gut geeignet:
- Niedrige Latenz
- Vorhersagbare Performance
- Energieeffizienz
- Wiederkehrende Workloads
- Acc in Datapath immer gut weil kein datentransfer notig
#### Schlecht geeignet:
- Sehr großer, unvorhersagbarer Working state
- Hoher Datentransfer-Aufwand
- Stark wechselnde Algorithmen
#### ASIC > FPGA/CGRA, wenn:
- Algorithmus stabil
- Große Stückzahlen
- Hohe Frequenzen nötig

---

### 12. Offene Herausforderungen (typische Diskussionsfrage)

- Automatische Ableitung von Accelerators aus Workloads?
- Gemeinsame Nutzung (Multi-Tenancy)?
- Isolation von Daten & Performance?
- Wer konfiguriert & verwaltet die Hardware?

---

### 🎯 Klausur-Takeaways (kompakt)

✔ Spezialisierung = Effizienz vs. Flexibilität  
✔ Integration (In-Data-Path / Side / Co-Processor) beherrschen  
✔ TPU als **Beispiel-ASIC** erklären können  
✔ FPGA vs. CGRA vs. ASIC vergleichen  
✔ Warum Software-Integration kritisch ist

**CGRA = Coarse-Grained Reconfigurable Array**
NIC = Network Interface Cards
Single Core Performance bleibt gleich → mehr parallelismus oder mehr specialisierte hardware


# Vorlesung 9: Networking

### 1. Überblick & Lernziele

Die Vorlesung behandelt:
- Klassisches **Socket-basiertes Networking**
- Vor- und Nachteile von **OS-basierter Netzwerkanbindung**
- **User-Space Networking** und **DPDK**
- **Remote Direct Memory Access (RDMA)**

Zentrales Thema:  
👉 **Netzwerke werden schneller, CPUs nicht → Software-Overhead wird zum Bottleneck**

---
### 2. Netzwerk-Stack (Schichtenmodell)

Klassische, modulare Architektur:

|Schicht|Aufgabe|
|---|---|
|Application|Anwendungen|
|Transport (TCP/UDP)|Ende-zu-Ende-Kommunikation|
|Network (IP)|Routing|
|Data Link (Ethernet)|Lokale Übertragung|
|Physical|Bits & Signale|

👉 Vorteil: Modularität  
👉 Nachteil: **Overhead durch viele Schichten**

---

### 3. Socket-basierte Programmierung

#### Socket API (klassisch):
- `socket(), bind(), listen(), connect(), accept(), close()`
- `send(), recv()`
- `select(), poll()`
#### Eigenschaften:
- Einfach zu benutzen
- OS übernimmt:
    - Buffer-Management
    - Scheduling        
    - Sicherheit & Isolation

👉 **Aber:** hoher Overhead durch Kernel-Beteiligung

---

### 4. Senden & Empfangen über Sockets (Linux)

#### Send-Pfad:
1. System Call → Wechsel in Kernel
2. Kopie in Kernel-Buffer
3. TCP/UDP-Verarbeitung
4. IP-Routing
5. NIC / DMA / Interrupts

#### Receive-Pfad:
- Asynchron
- Interrupts oder Polling
- Blocking vs. Non-Blocking I/O
- Empfange ist komplexer, weil asynchron und interrupts + polling
    - Entweder Blocking thread bis receive → Viele threads fur viele connections
    - Oder Non-Blocking → EIn thread kummert sich um mehrere

👉 **Viele Kopien + viele Kontextwechsel**

---

### 5. Das Kernproblem: CPU-Bottleneck
#### Trends:
- Netzwerkbandbreite:
    - Heute: **100–200 Gbps**
- CPU-Frequenz:
    - Seit Jahren ~3 GHz
- Kleinste Ethernet-Frames:
    - **~150 Mio. Pakete/Sekunde bei 100 Gbps**

👉 **OS + CPU können pro Paket kaum noch Arbeit leisten**

**Faustzahl:**
- DRAM-Zugriff: 60–100 ns
- Zeit zwischen Paketen bei 100 Gbps: **~6.7 ns**

➡️ **Schon ein Cache Miss ist zu teuer**

10Gbps; Ethernet Frame Size 84 bytes; 67ns zwischen packets (14.88 Mpps);
L1$ = 1 ns, L2$ = 5 ns, LLC$ = 30 - 40 ns, DRAM = 60 - 100 ns
- 84 bytes / 10GBps = 67ns
- 1s / 67 ns = 14,88 Mpps
- Allowed Cache misses → MAybe 1 DRAM Access

100Gbps
- 6,7 ns
- 148,8 Mpps
- Allowed Cache misses → Nur ein paar L1 und L2 erlaubt

---

### 6. Rolle des Betriebssystems (Overhead)

Warum OS-Netzwerk teuer ist:
- System Calls
- Ring-Wechsel (User ↔ Kernel)
- Security Checks
- Scheduling
- Interrupts

👉 Bei 10 Gbps: ~15 Mio. System Calls / Sekunde  
👉 Bei 100 Gbps: praktisch **nicht skalierbar**

---

### 7. Idee: User-Space Networking

#### Grundidee:
- **Netzwerk-Stack teilweise oder ganz in User Space**
- Trennung von:
    - **Data Path** = daten ubertragung (langsam, Verwaltung)
    - **Control Path** = Speicher reservieren, buffer managen, prozess schedulen (schnell, polling)
#### Vorteile:
- Keine System Calls im Datenpfad
- Keine Kernel-Interrupts
- Volle Kontrolle über Speicher & Threads
#### Nachteil:
- Mehr Verantwortung für Anwendung
- Sicherheit & Isolation schwieriger

---

### 8. DPDK (Data Plane Development Kit)

Data Plane Development Kit (DPDK)
● Data path - code path where the actual work is done
○ Try to make it straight forward, no blocking calls, everything is ready to go
● Control path - code where resources are managed
○ Slow(er), resourced need to be allocated and managed, can block/sleep
● Fast path - common case execution (typically few branches, very simple code)
○ E.g., the next TCP packet is a data packet in the expected order and “shape”
● Slow path - more sanity checks (more branches, hence poor(er) performance)
○ A TCP packet with special flags, retransmissions, etc.
#### Was ist DPDK?
- User-Space Networking Framework (Intel, seit ~2010)
- Heute: Industrie-Standard
- Einsatz:
    - Software Switches
    - Router
    - Cloud Networking
#### Zentrale Ideen:
1. **Polling statt Interrupts**
2. **Keine System Calls im Fast Path**
3. Core-Pinning & NUMA-Awareness
4. Lock-freie Queues (CAS)
5. Huge Pages (weniger TLB Misses)
6. Batch/Burst-Verarbeitung
#### Performance:
- ~**80 Mpps pro Core**    
- ~**33 CPU-Zyklen pro Paket**

👉 DPDK baut den Linux-Netzwerkstack praktisch **neu in User Space**

Data Plane Development Kit
- Von Intel um zu zeigen wie schnell ihre CPUs sind
- Ist der schnellste packet processing framework
- Control und Data Plane im user space
- Keine sys calls alles mit polling
- Keine treiber anpassung nptig

---

### 9. Motivation für RDMA

Frage:

> Können wir Netzwerkzugriffe so schnell machen wie lokale Speicherzugriffe?

Antwort:  
👉 **RDMA (Remote Direct Memory Access)**

---

### 10. RDMA – Grundidee

#### Eigenschaften:
- Kein Socket-Modell
- Eigene API & Abstraktionen
- Sehr geringe Latenz
- Sehr hohe Bandbreite
- Minimale CPU-Beteiligung
#### Ziel:
> Netzwerk ≈ Speicherzugriff

---

### 11. RDMA-Konzepte

#### Neue Objekte:
1. **Registrierte Speicherbuffer**
2. **Queue Pairs (QP)** – Send/Recv Queues
3. **Control Queues**

#### Work Requests (WR):
- Beschreiben Netzwerkoperationen
- Unterstützen:
    - Scatter/Gather
    - Batching
    - Ordering

⚠️ Wichtig:
> RDMA darf **nur auf vorregistrierte Speicherbereiche** zugreifen
- Aber was wenn mehrere clients auf selbe speicher schreiben?
- RDMA kopiert daten nur in NIC und nicht wie bei socket base die daten als copy in client side
---

### 12. One-Sided vs. Two-Sided Communication

#### Two-Sided (ähnlich Sockets):
- Sender & Empfänger aktiv
#### One-Sided (RDMA):
- **READ:** Client liest direkt aus Remote-Speicher
- **WRITE:** Client schreibt direkt in Remote-Speicher
- Remote CPU / OS **nicht beteiligt**

👉 Enormer Performance-Gewinn

---

### 13. RDMA-Architektur (vereinfacht)
1. local buffer address “laddr” in NIC speichern
2. Server teil client mit wo daten gespeichert werden
3. Wenn client lesen will Read request an server NIC
4. Server NIC liest mit DMA DRAM und sendet es an client
5. Client NIC speihert es dann mir DMA in DRAM
6. Client NIC gibt OS bescheid das ubertragung fertig ist

* RDMA mit DRAM aber auch mit GPU DRAM moglich

- NICs übernehmen:
    - DMA
    - Datenübertragung
- CPU nur:
    - Initiale Konfiguration
    - Completion-Notification

➡️ **RNIC = Netzwerk + Endhost**

---

### 14. RDMA-Performance

Vergleich TCP vs. RDMA:
- Bandbreite:
    - TCP: ~33 Gbps
    - RDMA: ~97 Gbps
- Latenz:
    - Bis zu **10× niedriger**
- CPU-Auslastung:
    - RDMA: **~0 % im Datentransfer**

👉 Besonders stark bei **kleinen Nachrichten**

---

### 15. Einsatzgebiete von RDMA

Vor allem **im Rechenzentrum**:
- Key-Value Stores
- Caches
- RPCs
- Shared Memory
- Locking & Synchronisation
- Dateisysteme
- Infrastruktur-Services (Cloud)

Nicht geeignet:
- Internet-WAN (hohe RTTs)

---

### 16. Herausforderungen von RDMA

#### Probleme:
● Debugging
○ Operation failed, connection down, what went wrong?
○ Logging and introspection can be hard, e.g., log4j, printf -> string manipulation@10s of usec!
● Performance
○ Takes a while to get used to the new way of writing code - event driven
○ Performance isolation (e.g., local PCIe vs remote NIC traffic BUG)
○ Quality of service, traffic management, firewall, filtering, compliance
● Fragility
○ In the cloud (performance vs. flexibility, e.g. VM migration)
○ Correctness and verification (e.g., 32 bit ADD circuit on 64-bit addresses in one RNIC)
○ Small eco-system and vendors
● Scalability
○ How many concurrent socket connections can you support in your server?
○ How many memory buffers an RNIC can remember? 

👉 Sehr leistungsfähig, aber **komplex & fragil**

---

### 17. Klausur-Takeaways (sehr wichtig!)

✔ Warum OS-Netzwerk zum Bottleneck wird  
✔ Socket vs. User-Space Networking  
✔ DPDK: Polling, Fast Path, kein Kernel  
✔ RDMA: One-Sided Communication  
✔ RDMA ≠ Socket (völlig anderes Modell)  
✔ Performance vs. Programmierkomplexität


# Vorlesung 10: Cloud

### 1. Motivation: Warum Cloud?

#### Früher (On-Prem):
- Unternehmen kaufen & betreiben eigene Hardware
- Hohe **CapEx** (Investitionskosten)
- Hardware oft **stark unterausgelastet** (~15 %)
#### Heute (Cloud):
- Hardware & Software als **Service**
- **Pay-per-use**
- **OpEx statt CapEx**
- Skalierung ohne große Vorabinvestitionen

👉 **Klausur-Merksatz:**
> Die Cloud senkt Einstiegskosten und verbessert Ressourcenauslastung durch Sharing.

---
### 2. Hyperscaler & Markt

- Große Anbieter: **Amazon, Microsoft, Google, Alibaba, Meta, Tencent**
- Eigenschaften:
    - Betreiben riesige Rechenzentren
    - Dominieren den Servermarkt
    - **Bauen eigene Hardware**
- Folge:
    - Weniger Standardisierung
    - Mehr **Spezialisierung**
---

### 3. Cloud-Economics: CapEx vs. OpEx
#### Vorteile Cloud:
- Keine hohen Anfangsinvestitionen
- Elastische Skalierung
- Kosten proportional zur Nutzung
#### Nachteile Cloud:
- Dauerhafte hohe Auslastung → On-Prem evtl. günstiger
- Vendor Lock-in
- Cloud-Services können teuer werden

👉 **Prüfungsargument:**
> Cloud ist nicht automatisch billiger – es hängt vom Nutzungsprofil ab.

---

### 4. Hardware On-Prem vs. Cloud

#### Gemeinsam:
- Server-grade CPUs (x86, ARM)
- GPUs
- Virtualisierung erlaubt HW-Zugriff
#### Unterschiede:
- Proprietäre Hardware:
    - Amazon Nitro
    - Google TPUs
- Ressourcenformate vom Anbieter vorgegeben
- Wechsel zwischen Clouds schwierig

---

### 5. Cloud Service Modelle (sehr wichtig!)

#### IaaS – Infrastructure as a Service
- Virtuelle Maschinen / Bare Metal
- Nutzer verwaltet OS & Software
- you get the computers, you build the rest
- Beispiel: **AWS EC2**
#### PaaS – Platform as a Service
- Infrastruktur + Middleware (Autoscalers, load balancers, distributed caches)
- Fokus auf Applikation
- ou get the computers + middleware, you build the application
- Beispiel: **Elastic Beanstalk**
#### SaaS – Software as a Service
- Fertige Anwendung
- Nutzer liefert nur Daten
- you get the application, you provide the data to populate it
- Beispiele:
    - Office 365
    - Gmail
    - Snowflake (nutz viele cloud anbieter im hintergrund aber wir sehen nur analytics engine)
#### FaaS – Functions as a Service
- **Serverless**
- Funktionen statt VMs
- Automatische Skalierung
- Abrechnung pro Millisekunde
- Beispiel: **AWS Lambda**

👉 **Merksatz:**
> Je höher die Abstraktion, desto weniger Kontrolle – aber desto weniger Aufwand.

---

### 6. Storage in der Cloud

#### Speicherarten:
1. **Local Disk (VM-lokal)**
    - Schnell
    - Keine Fault Tolerance
2. **Block Storage (EBS)**
    - Netzwerkbasiert
    - Elastisch, repliziert
3. **Object Storage (S3)**
    - Hohe Latenz
    - Sehr skalierbar & langlebig

👉 **No one size fits all**

---

### 7. Cloud Applications: Was läuft in der Cloud?
1. Klassische Anwendungen → Cloud migriert
2. Cloud-native Anwendungen:
    - In-house
    - Als Service für andere

---

### 8. Architekturen für Cloud-Anwendungen

#### Historische Entwicklung:
- 1-Tier (Mainframe) = alles auf einem server
- 2-Tier (Client-Server) = mehrere Serrver
- **3-Tier / N-Tier (Cloud)** = startk verteilt

In the datacenter and cloud: 3 Tier (N Tier) applications
• Presentation/Application/Data Tier architecture
• Middleware-based architecture
• Microservice architecture
![[Pasted image 20260118141612.png]]
3-Tier vs Tier 2

#### Advantages:
• Reduce the number of necessary interfaces:
• clients and local applications see only one system (the middleware)
• Centralize control and provide a common integration platform
• Make necessary functionality widely available to all clients
• Can implement functionality that otherwise would be difficult (e.g., transactions)
• Help deal with application heterogeneity and integration
#### Disadvantages:
• Yet another indirection level  extra complexity, extra latency
• No “standardized” way of assembling the components

---

### 9. Microservices

#### Motivation:
- Große Teams
- Schnelle Entwicklung
- Globale Systeme
#### Eigenschaften:
- Viele kleine Services
- Kommunikation über Netzwerk
- Unabhängige Skalierung
- Lose Kopplung

👉 **Achtung:**
> Microservices erhöhen Latenz und Systemkomplexität

---

### 10. Kommunikation in Cloud-Systemen

| Stil                 | Latenz       | Kopplung  | Beispiele     |
| -------------------- | ------------ | --------- | ------------- |
| Shared Memory / RDMA | sehr niedrig | sehr eng  | DBs, ML       |
| RPC (gRPC)           | niedrig      | eng       | Microservices |
| REST (HTTP)          | mittel       | lose      | Public APIs   |
| Message Queues       | hoch         | sehr lose | Kafka, SQS    |

---

### 11. Tail Latency (extrem klausurrelevant!)
- Cloud-Anwendungen haben **hohen Fan-Out**
- Langsamste Komponente bestimmt Antwortzeit
- **p99 wichtiger als Durchschnitt**

👉 **Merksatz:**
> Average latency is meaningless in large-scale cloud systems.

---

### 12. Scale-Up vs. Scale-Out
#### Scale-Up:
- Größere Maschinen
- Früher gut (Moore’s Law, dennard sclaing)
	- Moores Law verdopplung der Transistoren
	- Leistungsdichte bleibt konstant (also Transsitoren werden nicht nur kleiner sondern auch effizeinter)
- Heute limitiert
#### Scale-Out:
- Viele kleine Knoten
- Standard im Cloud
- Mehr Flexibilität
- Aber:
    - Netzwerk-Overhead
    - Verteilte Systeme sind komplex

---

### 13. Warum Scale-Out?

- Big Data passt nicht auf eine Maschine
- Parallelisierung
- Fehlertoleranz
- Best-Effort Ergebnisse möglich

---

### 14. Klausur-Takeaways (merken!)

✔ Cloud = OpEx statt CapEx  
✔ IaaS / PaaS / SaaS / FaaS klar unterscheiden  
✔ Storage ≠ gleich Storage  
✔ N-Tier & Microservices sind Standard  
✔ Tail Latency > Average Latency  
✔ Scale-Out dominiert moderne Cloud-Systeme

These architectures are the result of a combination of
• Increasingly complex systems (systems instead of programs)
• The need to meet Service Level Agreements (performance, reliability constraints)
• Growing use of open-source systems for many tasks
• Proliferation of specialized solutions (specialized databases)
• The underlying hardware architecture

---






# Vorlesung 11: Virtualization (Cloud)

### 1. Was ist Virtualisierung?
- Virtualisierung = **virtuelle Darstellung einer physischen Ressource**
- Fügt eine **Indirektionsebene** zwischen Software und Hardware ein
- Ziel:
    - **Ressourcen teilen**
    - **Isolation & Sicherheit**
    - **Flexibilität**

👉 Wichtig:
> Virtualisierung ist **nicht dasselbe wie Abstraktion** – sie versteckt Details nicht zwingend.

---

### 2. Warum Virtualisierung in der Cloud?
- Mehrere Nutzer teilen sich Hardware **sicher**
- Bessere Auslastung (Server Consolidation)
- Lastverteilung
- Migration von VMs
- Checkpoint / Restore

👉 **Ohne Virtualisierung keine Public Cloud**

---

### 3. Virtuelle Maschinen (VMs) – Grundbegriffe
- **Host**: physische Maschine
- **Guest**: VM mit eigenem OS + Apps
- **VMM / Hypervisor**: Software, die Virtualisierung umsetzt
#### Zentrale Eigenschaften:
Partitionierung (aufteilung uber mehrer mieter)
- **Resource Sharing**
- **Isolation** von den Mietern
Encapsulation
- **Migration** vm bewegen
- **Checkpoint / Restore**
- Execution Replay

---

### 4. Arten von Virtual Machines

- **System VMs**: virtualisieren komplette Maschine  
    → z. B. KVM, Xen, VMware
- **Process VMs**: virtualisieren nur Ausführungsumgebung  
    → z. B. Java Virtual Machine JVM

👉 Fokus der Vorlesung: **System VMs**

---

### 5. Anforderungen an Virtualisierung

Nach Popek & Goldberg:
1. **Safety** – Isolation zwischen Gästen & VMM
2. **Equivalency** – gleiches Verhalten wie ohne VM
3. **Efficiency** – möglichst wenig Overhead

---

### 6. Privilegien & Traps (Grundlage!)

- **Privilegierte Instruktionen**: dürfen nur im Kernel-Modus laufen
- **Trap**: Übergang in privilegierten Modus
- **Interrupt**: asynchron von device (z. B. I/O)
- **Exception**: synchroner Fehler (z. B. Page Fault)

👉 Klassische CPU-Ringe:
- Ring 0: Kernel
- Ring 3: User

Examples of privileged instructions
• Update memory address mapping
• Flush or invalidate data cache
• Read or write system registers
• Change the voltage and frequency of processor
• Reset a processor
• Perform I/O operations
• Context switch; change from kernel mode to user mode

---

### 7. Virtualisierungsansätze (sehr klausurrelevant!)
#### 1️⃣ Hosted Interpretation

- VMM läuft als User-Programm auf Host-OS
- Alles wird emuliert
**Pro:** Complete isolation; no guest instruction is directly executed on host HW, Easy to handle priviledged instructions
**Contra:** extrem langsam (~100×), Emulating a modern processor is difficult

---
#### 2️⃣ Trap-and-Emulate

- Guest läuft direkt auf Hardware schneller als interpretation
- Privilegierte Instruktionen → Trap → VMM
**Problem:**
- Funktioniert nur, wenn **alle sensitiven Instruktionen auch traps auslösen**
- Immernoch langsam
- the processor needs to be “virtualizable”
![[Pasted image 20260118211940.png]]

---
#### Virtualisierbarkeit (Popek & Goldberg)

- Alle sensitiven Instruktionen müssen privilegiert sein
	- Sensitive instructions are those that change the HW configuration (allocations, mappings, …) or whose outcome depends on the HW configuration
	- Priviledged instructions are those that cause a trap when executed in user mode.
- Need at least two execution modes (kernel & user)
- **Alte x86-Architekturen waren nicht virtualisierbar**

---
#### 3️⃣ Binary Translation

- VMM schreibt kritische Instruktionen **dynamisch um**
- Guest OS bleibt unverändert
**Pro:** läuft auch auf nicht-virtualisierbarer Hardware, Can run unmodified guest OSes and apps, Most instructions run at bare-metal speed
**Contra:** komplex, Performance-Kosten, Implementing the VMM is difficult and
translation impacts performance.

---
#### 4️⃣ Para-Virtualisierung

- Guest OS wird **modifiziert** to remove
sensitive-but-unpriviledged instructions.
- OS arbeitet bewusst mit VMM zusammen
**Pro:** schneller als Binary Translation 
	fewer context switches
	less bookkeeping
**Contra:** OS muss angepasst werden

Beispiel: **Xen**

---
#### 5️⃣ Hardware-unterstützte Virtualisierung (Standard heute)

- Intel **VT-x**, AMD-V
- Neuer Modus: **VT Root Mode**
- Guest OS läuft direkt in Ring 0
- **VM Entry / VM Exit**
- Steuerung über **VMCS**
- Fast and supported on most CPUs today.

👉 **Das ist der heute dominante Ansatz**

---

### 8. Virtualisierung von Speicher (Memory)

#### Problem:
- Guest glaubt, er hat eigenen physischen Speicher (also zusammenhangend und zerp based), VMM muss das vorspielen
#### Ohne Hardware-Support:
- **Shadow Page Tables**
- Hoher Overhead
- Viele VM Exits fur shadow tbale verwalten
- Viel Speicherverbrauch
![[Pasted image 20260118213104.png]]
---
#### Mit Hardware-Support: Extended Page Tables (EPT)
- Zwei Stufen:
    - Guest Virtual → Guest Physical
    - Guest Physical → Host Physical
- Keine VM Exits bei Page Faults
- Weniger Speicherbedarf

⚠️ **Aber:**
> TLB Miss extrem teuer (bis zu **24 Page Walks**)
![[Pasted image 20260118213349.png]]
![[Pasted image 20260118212728.png]]![[Pasted image 20260118212800.png]]
---
![[Pasted image 20260118213730.png]]
![[Pasted image 20260118213852.png]]
![[Pasted image 20260118213905.png]]
### 9. I/O-Virtualisierung
#### Problem:
- Viele unterschiedliche Geräte
- Treiber fur VMM unrealistisch da schon fur OS existiert
#### Lösung
- Virtuelle Geräte für Gäste
- Host übernimmt echte Hardware
#### Methoden:
- Device Emulation
- Para-virtualisierte Geräte
- **SR-IOV**:
    - Ein Gerät erscheint als mehrere virtuelle Geräte
    - Sehr performant (z. B. NICs)

---

### 10. Performance-Overheads von VMs
- Häufige Kontextwechsel schecht
- TLB-Pressure wgene viel speicherzugriff
- mehr streit um speicher hirachy(caching)
- Längere I/O-Pfade
- Mehr Cache-Contention
- Geteilte Ressourcen

👉 **VMs = starke Isolation, aber Performance-Kosten**

---

### 11. Container

#### Was ist ein Container?
- **OS-Level-Virtualisierung**
- Alle Container teilen sich den Kernel
- Kein guest kernel
- kein hypervisor
- Isolation durch:
    - Namespaces
    - cgroups
#### Vorteile:
- Sehr leichtgewichtig
- Schneller Start
- Nahezu Bare-Metal-Performance
- Keine anpassung wegen speicher oder so
#### Nachteile:
- Schwächere Isolation
- Kernel-Sicherheitslücken kritisch

---

### 12. Docker (Container-Ökosystem)
- Standard für Container
- Konzepte:
    - **Image** (read-only Vorlage)
    - **Container** (laufende Instanz)
    - **Registry**
    - **Dockerfile**
- Images bestehen aus **Layern**
- Ermoglicht ienfaches packaging
- Baut auf LXC
	- Hat cgroups und namespaces geadded

---

### 13. VMs vs. Container

||VM|Container|
|---|---|---|
|Isolation|stark|schwächer|
|Overhead|höher|sehr gering|
|Startup|langsam|schnell|
|OS|eigenes OS|geteilter Kernel|

👉 Praxis:
- **VMs für Sicherheit** (weil container wie process)
- **Container für Effizienz**
- Containers sind ein linux ding nicht windows
![[Pasted image 20260118215131.png]]
---

### 14. WebAssembly (Wasm)
Noch weniger overhead als container

- Portables Binärformat
- Sehr schnell & sicher
- Kein direkter System-Call-Zugriff
- Extrem kleiner Footprint
- Einsatz:
    - Browser
    - Cloud
    - Edge Computing

---

### 15. Vergleich aller Virtualisierungstechniken

||VM|Container|Wasm|
|---|---|---|---|
|Isolation|stark|mittel|stark|
|Performance|geringer|hoch|sehr hoch|
|Startup|langsam|schnell|instant|
|Footprint|groß|mittel|sehr klein|
|Flexibilität|sehr hoch|hoch|eingeschränkt|
![[Pasted image 20260118215407.png]]

---

### 16. Klausur-Takeaways (sehr wichtig!)

✔ Warum Virtualisierung essenziell für Cloud ist  
✔ Unterschiede: VM vs Container vs Wasm  
✔ Trap-and-Emulate / Binary Translation / VT-x  
✔ Memory-Virtualisierung & EPT  
✔ Performance-Kosten von Virtualisierung  
✔ Isolation vs Effizienz Trade-off

---

### 🎯 Gesamtfazit für die Klausur

Diese Vorlesung wird **sehr gerne abgefragt**, besonders:
- **Warum Hardware-Unterstützung nötig war**
- **Warum Container schneller, aber unsicherer sind**
- **EPT & TLB Misses**
- **Vergleich VM / Container / Wasm**

---









---
# Fragensammlung

### **Frage 1 – CPU vs. GPU (Grundlagen)**

**Nenne zwei zentrale Unterschiede zwischen CPU- und GPU-Architekturen** und erkläre kurz, **warum GPUs für Throughput-Workloads besser geeignet sind**.

---
### **Frage 2 – CUDA Execution Model**

Erkläre die Begriffe:
- **Grid**
- **Block**
- **Warp**

👉 Welche dieser Einheiten ist die **kleinste physisch geschedulte Einheit** auf der GPU?

---
### **Frage 3 – Thread-Indexierung**

Gegeben ist ein CUDA-Kernel mit:
- `blockDim.x = 256`
- `blockIdx.x = 3`
- `threadIdx.x = 7`

**Welchen globalen Index (`idx`) berechnet der Thread?**  
Formel angeben und Ergebnis berechnen.

---

### **Frage 4 – Branch Divergence**

**Was ist Branch Divergence?**  
Warum führt sie zu **Performanceverlust** auf der GPU?

---
### **Frage 5 – Warps & Latency Hiding**

Erkläre kurz:
- **Was bedeutet „Latency Hiding“?**
- **Warum braucht eine GPU viele Warps pro SM, um hohe Performance zu erreichen?**

---
### **Frage 6 – Memory Access & Stride**

Zwei Varianten eines Kernels:
- **Variante A:** Stride = 1
- **Variante B:** Stride = Grid Size

👉 **Welche Variante ist in der Regel schneller und warum?**  
(Bezug auf Memory Coalescing!)

---
### **Frage 7 – Datenübertragung CPU ↔ GPU**

Warum ist es **problematisch**, für kleine oder sehr kurze Berechnungen eine GPU zu nutzen?  
Nenne **zwei Gründe**.

---
### **Frage 8 – Motivation & Trends**

Erkläre kurz den **Data / Compute Gap**.  
Welche **zwei grundsätzlichen Strategien** werden eingesetzt, um ihn zu schließen?

---
### **Frage 9 – CPU vs. GPU**

Nenne **drei Unterschiede** zwischen CPU- und GPU-Architekturen  
und erkläre, **für welche Art von Workloads GPUs besser geeignet sind**.

---
### **Frage 10 – CUDA Execution Model**

Erkläre die Begriffe:
- **Kernel**
- **Grid**
- **Block**
- **Warp**

👉 Welche Einheit ist die **kleinste physisch geschedulte Einheit**?

---
### **Frage 11 – Warps, Branch Divergence & Scheduling**

a) Was ist **Branch Divergence**?  
b) Warum führt sie zu Performanceverlust?  
c) Wie helfen **Volta+ GPUs** dabei, die Auswirkungen zu reduzieren?

---
### **Frage 12 – Memory Access auf GPUs**

a) Was bedeutet **Memory Coalescing**?  
b) Warum ist es entscheidend für GPU-Performance?  
c) Warum kann **Stride = grid size** in bestimmten Fällen schneller sein als **Stride = 1**?

---
### **Frage 13 – Latency Hiding**

Erkläre das Konzept des **Latency Hiding** auf GPUs.  
Warum sind **viele Warps pro SM** notwendig?

---
### **Frage 14 – Accelerator Integration**

Nenne und erkläre die **drei Integrationsoptionen** für Accelerators:
- In-Data-Path
- On-the-Side
- Co-Processor

👉 Welche minimiert **Datenbewegung**?

---
### **Frage 15 – Spezialisierung & Effizienz**

Warum sind **ASICs** deutlich energieeffizienter als CPUs/GPUs?  
Welcher **grundsätzliche Trade-off** steht dahinter?

---
### **Frage 16 – TPU**

a) Für welchen Workload wurde die **Google TPU** entwickelt?  
b) Warum ist sie so viel effizienter als GPUs?  
c) Wie wird sie programmiert?

---
### **Frage 17 – FPGA vs. CGRA vs. ASIC**

Vergleiche **FPGA, CGRA und ASIC** hinsichtlich:
- Flexibilität
- Energieeffizienz
- Programmierbarkeit

👉 Wann wäre ein **ASIC** die beste Wahl?

---
### **Frage 18 – FPGA Programmiermodell**

Beschreibe den Weg **von Code zur Schaltung** bei einem FPGA  
(Schritte + wichtigste Eigenschaften).

---
### **Frage 19 – Regeln & Grenzen**

Nenne **zwei Situationen**, in denen sich **Spezialisierung NICHT lohnt**,  
und erkläre warum.

---
### **Frage 20 – Grundlagen**

Erkläre kurz das **Schichtenmodell des Netzwerks**.  
Warum wird dieses Modell in der Praxis zum **Performance-Problem**?

---
### **Frage 21 – Socket-basiertes Networking**

a) Nenne **zwei Vorteile** der klassischen Socket-API.  
b) Nenne **drei Hauptquellen von Overhead** beim OS-basierten Networking.

---
### **Frage 22 – Send/Receive Path**

Beschreibe vereinfacht den **Send-Pfad eines TCP-Pakets** von der Anwendung bis zur NIC.  
Nenne **mindestens vier Schritte**.

---
### **Frage 23 – CPU-Bottleneck**

Warum wird die **CPU zum Bottleneck**, obwohl Netzwerke immer schneller werden?  
Beziehe dich auf **Bandbreite, Paketgröße und CPU-Latenzen**.

---
### **Frage 24 – Blocking vs. Non-Blocking I/O**

Erkläre den Unterschied zwischen:
- **Blocking I/O**
- **Non-Blocking I/O (select/poll)**

👉 Welche Variante skaliert besser bei vielen Verbindungen – und warum?

---
### **Frage 25 – User-Space Networking**

a) Was ist die Grundidee von **User-Space Networking**?  
b) Welche **OS-Funktionen werden aus dem Fast Path entfernt**?

---
### **Frage 26 – DPDK**

a) Was ist **DPDK** und wofür wird es eingesetzt?  
b) Nenne **vier zentrale Design-Ideen** von DPDK.

---
### **Frage 27 – Polling vs. Interrupts**

Warum setzt DPDK auf **Polling statt Interrupts**?  
Nenne **zwei Gründe**.

---
### **Frage 28 – RDMA Grundlagen**

a) Was ist **RDMA**?  
b) Worin unterscheidet sich RDMA **grundlegend von Sockets**?

---
### **Frage 29 – RDMA Communication Model**

Erkläre den Unterschied zwischen:
- **Two-sided Communication**
- **One-sided Communication**

👉 Warum ist **One-sided RDMA** besonders performant?

---
### **Frage 30 – RDMA Architektur**

Welche Rolle spielen:
- **RNIC**
- **DMA**
- **Registrierte Speicherbereiche**

in einem RDMA-System?

---
### **Frage 31 – Einsatz & Grenzen von RDMA**

a) Nenne **zwei typische Einsatzgebiete** von RDMA.  
b) Nenne **zwei Herausforderungen oder Nachteile** von RDMA.

---
### **Frage 32 – Cloud Motivation**

a) Erkläre den Unterschied zwischen **CapEx** und **OpEx**.  
b) Warum hat die Cloud den Wechsel von CapEx zu OpEx ermöglicht?  
c) Warum ist die Cloud **nicht immer** die günstigere Option?

---
### **Frage 33 – Hyperscaler**

Was sind **Hyperscaler**?  
Nenne **zwei Merkmale**, die sie von klassischen IT-Anbietern unterscheiden.

---
### **Frage 34 – Cloud Service Modelle**

Erkläre kurz:
- **IaaS**    
- **PaaS**
- **SaaS**
- **FaaS**

👉 Ordne jeweils **ein konkretes Beispiel** zu.

---
### **Frage 35 – Storage in der Cloud**

Vergleiche:
- **Local Disk**
- **Block Storage (z. B. EBS)**
- **Object Storage (z. B. S3)**

hinsichtlich:
- Performance
- Fehlertoleranz
- Typischer Einsatz

---
### **Frage 36 – Cloud Application Architectures**

a) Was ist eine **3-Tier / N-Tier Architektur**?  
b) Nenne **zwei Vorteile** und **einen Nachteil** dieser Architektur.

---
### **Frage 37 – Microservices**

a) Warum setzen moderne Cloud-Anwendungen auf **Microservices**?  
b) Nenne **zwei Vorteile** und **zwei Nachteile** von Microservice-Architekturen.

---
### **Frage 38 – Kommunikation in Cloud-Systemen**

Vergleiche **RPC**, **REST** und **Message Queues** hinsichtlich:
- Latenz
- Kopplung
- Typischer Einsatz

---
### **Frage 39 – Tail Latency**

a) Was ist **Tail Latency**?  
b) Warum ist **p99-Latenz** in Cloud-Systemen oft wichtiger als der Durchschnitt?

---
### **Frage 40 – Scale-Up vs. Scale-Out**

a) Erkläre den Unterschied zwischen **Scale-Up** und **Scale-Out**.  
b) Warum dominiert **Scale-Out** in der Cloud?

---
### **Frage 41 – Virtualisierung Grundlagen**

a) Was ist Virtualisierung?  
b) Warum ist Virtualisierung **zentrale Voraussetzung** für Cloud Computing?

---
### **Frage 42 – Virtual Machines**

Erkläre die Begriffe:
- **Host**
- **Guest**
- **VMM / Hypervisor**

👉 Nenne **zwei zentrale Eigenschaften** von VMs, die für die Cloud wichtig sind.

---
### **Frage 43 – Virtualisierungsanforderungen**

Nenne und erkläre die **drei Anforderungen an Virtualisierung** nach  
**Popek & Goldberg**.

---
### **Frage 44 – Virtualisierungsansätze**

Vergleiche kurz:
- **Trap-and-Emulate**
- **Binary Translation**
- **Para-Virtualisierung**
- **Hardware-unterstützte Virtualisierung**

👉 Welcher Ansatz wird **heute hauptsächlich** verwendet – und warum?

---
### **Frage 45 – Memory Virtualization**

a) Warum ist Speicher-Virtualisierung schwierig?  
b) Was sind **Shadow Page Tables** und warum sind sie teuer?  
c) Wie lösen **Extended Page Tables (EPT)** dieses Problem?

---
### **Frage 46 – TLB & Performance**

Warum sind **TLB Misses** in virtualisierten Systemen besonders teuer?

---
### **Frage 47 – I/O Virtualization**

a) Warum ist I/O-Virtualisierung schwierig?  
b) Was ist **SR-IOV** und warum ist es performant?

---
### **Frage 48 – Container**

a) Was ist ein Container?  
b) Vergleiche **Container** und **VMs** hinsichtlich:
- Isolation
- Performance
- Startup-Zeit

---
### **Frage 49 – Docker**

Erkläre die Begriffe:
- **Image**    
- **Container**
- **Registry**
- **Dockerfile**

---
### **Frage 50 – WebAssembly**

a) Was ist **WebAssembly (Wasm)**?  
b) Nenne **zwei Vorteile** gegenüber VMs oder Containern.  
c) Warum ist Wasm **stärker eingeschränkt**?

---
### **Frage 51 – Gesamtvergleich**

Ordne **VMs, Container und WebAssembly** nach:
- Flexibilität
- Isolation
- Performance

👉 Begründe kurz.

---
