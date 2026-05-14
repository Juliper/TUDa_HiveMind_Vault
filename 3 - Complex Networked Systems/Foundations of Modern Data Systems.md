---
title: FOMO
aliases:
  - Foundations of Modern Data Systems
tags:
  - fb20
  - master
  - semester-1
  - 6CP
description: ""
draft: false
---
## 📊 Vorlesung 1: Experiment Design & Statistik (gesehen)

### **Experimente - Motivation**

- performance requirements finden/capazität planen
- system vergleichen/tunen
- bottleneck finden

### Experimentt - Aufbau

1. **Preparation**: SUT und Hypothese definieren, richtige Workload finden, unwichtige Faktoren minimieren
2. **Experimentation**: Workloads ausführen, Wiederholungen, Statistiken sammeln
3. **Analysis**: Ergebnisse im Kontext der Hypothese berichten, ggf. wiederholen

### **Experimente - Hypothese**

- Experimente immer mit **Hypothese** durchführen (sonst sinnlos)
- Ohne Hypothese: viel "Noise" und irrelevante Trends
- Erwartung explizit formulieren → Mock-Graphen erstellen → mit Realität vergleichen

### **Metriken**

- **Throughput (TPUT)**: Erfolgreich abgeschlossene Requests pro Zeiteinheit
- **Response Time (RT)**: Zeit für eine Operation (Latency)

Zusammenhänge

- TPUT = 1/RT (bei keinen Parallelismus)
- TPUT = N/RT (bei N Maschinen)

### Workload

- Mix von Operationen, die Anwendung ausmachen
- Arten: Traces (realistisch), generalisiert, synthetisch (flexibel)
- Micro-Benchmark vs. vollständiger Workload

### Messaufbau

- **Black Box**: Keine Kenntnis interner Komponenten
- **White Box**: Messung auch interner Komponenten möglich
- SUT-Messung: innen (Code-Instrumentation) oder außen (Client)

### **System-Typen**

- **Closed System**: Begrenzte synchrone Clients → selbstregulierend
- **Open System**: Unbegrenzte/asynchrone Clients → Rate unabhängig vom Server

### **System-Verhalten**

- **Warm-up**: Caches füllen, JIT-Compiler, Daten laden
- **Stable Operation**: Hier messen wir normalerweise
- **Cool-down**: Clients stoppen asynchron

**Throughput-Verhalten**

- **Normal Operation**: System unter normaler Last
- **Saturation**: System erreicht Maximum
- **Over-loaded** (nur Open Systems): Performance bricht ein (Latenz steigt linear mit load)

### **Statistik**

![image.png](attachment:a15febd3-23ba-4e31-b3fe-536df8e6a292:image.png)

- **Accuracy vs. Precision**: Genauigkeit (nah am wahren Wert) vs. Präzision (geringe Streuung)
- **Average (Mean)**: Einfach, aber kann Details verstecken
- **Standard Deviation (STDEV)**: Streuung der Daten
    - Bei Normalverteilung: ~68% innerhalb 1σ, ~96% innerhalb 2σ
- **Median**: 50. Perzentil
- **Percentiles**: X-tes Perzentil = X% der Werte sind kleiner
    - Wichtig für Cloud: 99th Percentile optimieren (Tail Latencies)
    - Besser als Average bei nicht-normalen Verteilungen
- Viele System-Metriken haben andere Verteilungen
- Dann: Perzentile und CDFs (Cumulative Distribution Functions) nutzen

**Wichtige Regeln**

- Messungen sind Stichproben einer Zufallsvariable
- Verteilung meist unbekannt, oft Normalverteilung angenommen
- Wiederholungen durchführen
- Stabile Phase messen (nicht Warm-up/Cool-down)
- Overhead des Benchmarkings minimieren

## 📦 Vorlesung 2: Storage (gesehen)

### **Storage Hierarchy - Überblick**

- **Von schnell zu langsam**: Registers → L1/L2/L3 Caches → DRAM → Persistent Storage (SSD/HDD) → Archival Storage (Tape)
- **Management**: Cache-Hierarchie wird von Hardware verwaltet, persistent storage von Software
- **NUMA (Non-Uniform Memory Access)**: In Multi-Socket-Systemen ist lokaler Speicherzugriff schneller als remote

### **Data Movement**

- Registers ↔ Caches: **Words** (4-8 bytes)
- Caches ↔ Memory: **Cache Lines** (typisch 64 bytes)
- Memory ↔ Disk: **Pages** (typisch 4KB, bestehen aus mehreren Disk Blocks)

### **Storage-Zwecke**

- **Persistence/Durability**: Logging, Checkpointing → Sequential Access, Write Bandwidth wichtig
- **Extension of Main Memory**: Swap, LSM Trees → Mix von Sequential/Random, Read/Write
- **Data Exchange**: S3, Kafka → Coarse-grained, mit Replication/Load Balancing

### **Wann ist Storage Performance wichtig?**

- Wenn Latency signifikanten Teil der Response Time ausmacht
- Wenn Access Rate den System-Throughput limitiert

### Storage Mediums

**Hard Disk Drives (HDDs)**

- **Komponenten**: Platters, Disk Head, Arm, Tracks, Sectors, Blocks
- **Access Latency** = Seek Time + Rotational Delay + Transfer Time
    - Seek Time: Arm zur richtigen Track bewegen (~1-20ms)
    - Rotational Delay: Auf richtigen Block warten (~0-10ms)
    - Transfer Time: Daten lesen/schreiben (~<1ms für 4KB)
- **Sequential vs. Random Access**: Sequential ist viel schneller (nur 1× Seek + Rotational Delay für viele Blocks)
- **Latency**: 2-10ms | **Bandwidth**: 100s MB/s

**Solid State Drives (SSDs)**

- **Aufbau**: Flash Controller + interne CPU + internes Memory + Flash Chips
- **Vorteile**: Efficient Random Access, interne Parallelität, kein Seek/Rotation
- **Latency**: 10-100s μs | **Bandwidth**: mehrere GB/s (aber nur mit vielen parallelen Requests!)
- **Besonderheiten**:
    - **Erase before Write**: Unit of Write ≠ Unit of Erase
    - **Garbage Collection**: Nicht mehr genutzte Blocks aufräumen
    - **Write Amplification**: Physisch geschriebene Daten ≥ logisch geschriebene Daten
    - **Wear Leveling**: Cells/Blocks werden über Zeit fehlerhaft
    - **Unpredictable Latencies**: Wenn Request nach Write mit GC feststeckt

**RAID (Redundant Array of Independent Disks)**

- Mehrere Disks geben Illusion einer großen Disk
- **Data Striping**: Daten partitioniert über mehrere Disks → paralleler Zugriff
- **Redundancy**: Erlaubt Rekonstruktion bei Disk-Ausfall
- Verschiedene RAID-Level je nach Striping/Redundancy-Strategie

**Disk Controller**

- Computation Unit in Disk
- Mappt logische → physische Adressen (kann sich ändern bei Fehlern)
- Remapping fehlerhafter Blocks
- Internes Caching (forced-write für Persistence)
- **In SSDs komplexer**: Flash Translation Layer (GC, Wear Leveling)

### **File Systems (OS)**

- **Zweck**: Abstraktion über Disk-Storage
    - **Disk Management**: Organisation von Daten in Files
    - **Naming**: Files über Namen statt Block-IDs finden
    - **Security**: Permission Control
    - **Durability**: Kein Datenverlust bei Failures
- **Linux Disk-Layout**: Boot Block | Super Block | Bitmap | Inode Table | File Blocks
    - **Super Block**: Metadata über FS (Größe, #Inodes, Offsets, FS-Typ)
    - **Inode**: Metadata über File (Größe, Permissions, Timestamps, Block Numbers)
    - **Inode Table**: Mapping inode# → inode
    - **Bitmap**: Welche Blocks belegt (1) oder frei (0)
    - **File Blocks**: Eigentliche Daten (typisch 4KB)
    - **Boot Block**: boot block starts/boots the OS
- **Buffer Cache**: OS cached häufig genutzte Blocks in Main Memory

### From Memory to Files

Data in memory cannot be directly stored to disk (pointers, structure implicit in application)

**Storage Formats**

- **CSV (Comma Separated Values)**:
    - Text-basiert, zeilenweise
    - Keine Metadata (Typen, Ranges)
    - Sehr einfach, universell nutzbar
    - Langsam zu parsen (~10s MB/s), nicht parallelisierbar
    - Ineffizient (ASCII vs. Binary)
    - Externe Compression/Encryption
- **Parquet**:
    - Page-basiert, spaltenorientiert, binär
    - Reichhaltige Metadata
    - Braucht Library
    - Schnell zu parsen (>100s MB/s)
    - Random Access möglich (Pages)
    - Effizient (binary + compression)
    - **De-facto Standard** in Data Systems

### **OS vs. App-Managed Storage**

- **Mit OS/File System**:
    - OS versucht reasonable Performance für alle Apps
    - Overhead durch File System
    - Moderne async I/O (io_uring) möglich
- **App-managed (z.B. DBMS)**:
    - Eigene Hierarchie in wenigen großen Files
    - Oder: OS komplett bypassen (SPDK)
    - App übernimmt alle Management-Aspekte
    - Dupliziert OS-Features

**DBMS Storage Management**

- **Disk-Based DBMS**: Primary Storage auf non-volatile Disk
- **Pages**: Fixed-length Storage units of transfer between buffer and disk
    - **Page ID**: Unique Identifier, mappt zu Disk-Location und Buffer Frame
    - **Page Table**: Page ID → Disk Offset oder Memory Address
    - **Slotted Pages**: Header + Slot Array (Offsets) + Tuple Data (back-to-front)
    - Typische Größen: 1KB (SQLite), 4KB (Oracle), 8KB (PostgreSQL/SQL Server), 16KB (MySQL)
- **Buffer Pool**: In-Memory Cache für "hot" Pages
    - Managed data movement zwischen Disk und Memory
    - Memory typisch gepinnt
- **Record ID (RID)**: Pointer zu Tuple = Page ID + Slot#

## 📚 Lecture 3: Main Memory & Caching (gesehen)

### **Memory Technologies**

- **ROM (Non-Volatile)**: ROM, PROM, EPROM, Flash
- **RAM (Volatile)**:
    - **SRAM**: Flip-Flop basiert (2-6 Transistoren), schnell, teuer → für Caches
    - **DRAM**: Capacitor basiert (1 Transistor + 1 Capacitor), braucht Refresh, günstiger → für Main Memory

### **Memory Design**

- **Volatility**:
    - Non-volatile: Behält Daten ohne Strom (ROM, Flash, NVM)
    - Static volatile: Behält Daten mit Strom (SRAM)
    - Dynamic volatile: Verliert Daten auch mit Strom über Zeit (DRAM) → benötigt Refresh
- **Access**:
    - Random: Jede Location direkt zugreifbar (RAM, ROM)
    - Sequential: Locations nacheinander (Tape)
    - Associative: Location über Tag/Content (TCAMs)
    - Stack: Top of Stack (Stack Pointer)
- **Organization**:
    - Uniform Access: Alle Locations gleich schnell
    - NUMA: Access-Zeit abhängig von CPU-Position relativ zum Memory
- **Memory Cell**: Kleinste Einheit (1 Bit)
    - SRAM: Flip-Flop (2-6 Transistoren)
    - DRAM: Capacitor (1 Transistor)
- **Memory Location**: Gruppe von Cells (8/16/32 Bits), addressierbar
    - Hat Address + Content

### SRAM vs DRAM

**SRAM Structure**

- **Komponenten**: Address Decoder, Memory Locations, Data Amplifier, Control Unit
- Linear oder Matrix Organization

**DRAM Structure**

- Braucht refreshing
- Komplexer als SRAM
- **Bank**: Daten in Rows & Columns
    - Access: Row-first, dann Column
- **Chip**: Mehrere Banks → Capacity
- **Rank**: Mehrere Chips an gleichen Adressen → Bandwidth
- **DIMM**: Mehrere Ranks, separat zugreifbar
- **Typical Bandwidth per DIMM**:
    - DDR3: 12-15 GB/s
    - DDR4: 12-25 GB/s
- **Moderne Server**: Bis zu 16 DIMMs pro CPU

### **HBM (High Bandwidth Memory)**

- DRAM in 3D-gestacktem Package
- High Bandwidth durch breitere Busse (>512 bit Cache Lines!)
- Meist in GPUs/Compute Accelerators
- Typisch auf gleichem Package wie Processing Element
- **HBM4 (2025)**: 32×64 bit, 16 dies × 4 GB = 64 GB, 2048 GB/s

### Virtual Memory

- **Illusion**: Jede App hat kontinuierlichen Address Space, nur für sie
- **Mapping**: Virtual Address → Physical Address (oder andere Devices)
- **Overhead**: Mapping bei jedem Access!
- **Implementierung**: OS + CPU Hardware (MMU - Memory Mapping Unit) arbeiten zusammen
- **Granularität**: Pages (typisch 4KB, MB, GB)
- **Page Table**: Wird im Memory gespeichert (!)
- **Benefits**: Einfacheres Programming, Flexibilität, bessere Security

**Virtual Memory - Details**

- **Allokation**: Beim Allocate wird kein Physical Memory berührt
- **Access**: Bei R/W wird Virtual Address in Physical Address übersetzt oder allokiert
- **TLB (Translation Lookaside Buffer)**: Cache für Page Table
    - Content Addressable Memory, 1000s Entries
    - TLB Miss → Extra Memory Reads
- **TLB Structure**: Multi-Level

**Huge Pages**

- **Default**: 4KB Pages
- **Modern CPUs**: Unterstützen MB/GB-sized Huge Pages
- **Vorteile**:
    - Weniger TLB-Einträge nötig → weniger TLB Misses
    - Physisch zusammenhängend → besser für DMA
- **Nachteile**: Memory Fragmentation

### CPU Caches

**Principle of Locality**

- **Programme nutzen Daten & Instructions mit Adressen nahe den kürzlich genutzten**
- **Temporal Locality**: Kürzlich referenzierte Items werden bald wieder referenziert
- **Spatial Locality**: Items mit nahen Adressen werden zeitlich nah referenziert
- **Grund**: Warum Storage Hierarchy so designed ist!

**Caching - General Concept**

- **Ziel**: Locality erhöhen → Access Latency für häufig genutzte Daten reduzieren
- **Inclusivity**: Daten in niedrigeren Levels auch in höheren Levels (meist)
- **Replacement**: Policy wenn kein Platz mehr
- **Modified Data**: Write-through (sofort) vs. Write-back (bei Replacement)

**CPU Cache Internals**

- **Cache Lines**: Typisch 64 Bytes
    - Nur ganze Cache Lines laden/evict
    - Writeback nicht sofort → Dirty Lines
- **Block-wise Transfers**: Gut von DRAM unterstützt
- **Unterstützt**: Spatial + Temporal Locality

**CPU Cache - Mapping**

- **Challenge**: "Suchen" einer Memory Line im Cache muss konstant sein
- **Lösung**: Viele Main Memory Addresses mappen zu einer/wenigen Cache Line(s)
- **Conflict**: Mehrere Adressen konkurrieren um gleiche Cache Line
- **Cache Coloring**: Durch Kenntnis der Cache-Properties Daten so layouten, dass Konflikte vermieden werden
- **Mapping-Arten**:
    - Direct Mapped: Jede Memory Location → genau 1 Cache Location
    - N-Way Associative: Jede Memory Location → N Cache Locations

**Multi-Level Cache**

- **Reads**: Bringen Cache Line in L1
- **Eviction**: Policy bewegt CLs durch die Levels
- **Writeback**: Wenn aus LLC evicted und dirty → write to DRAM
- **Non-Allocating Load**: Spezielle Instructions für non-cached read

**Multi-Core Cache Coherency**

- **Problem**: Dirty Cache Line in L1 von Core 1, Core 2 will laden?
- **Lösung**: Koordination zwischen Cores bei jedem Memory Access
- **Methode**: Snooping Protocol (Messages auf Interconnect zwischen Cores + MMU)
- **High-Level Idea**: Cache Lines mit State getaggt:
    - Modified, Exclusive, Shared, Invalid (MESI)
    - In Praxis mehr States: MOESI, MOSIF
- **Before Read/Write**: Intention wird broadcast, State ändert sich lokal + remote
- **Directory-Based Cache Coherency**:
    - Zentralisiert oder verteilt (HW Resource)
    - Resource-Overhead + Latency-Overhead
- **Einsatz**:
    - Across NUMA Regions
    - Zwischen CPU Cache und einigen Accelerators (z.B. CXL-based)
    - PCIe selbst ist **nicht** cache coherent!

**Hardware Prefetching**

- **Next-Line**: Miss a → fetch a+1
- **Stream**: Miss a, a+1 → fetch a+2, a+3
    - ✓ Begünstigt Sequential Access & Spatial Locality
- **Branch Prediction**: Behandelt Branches/Function Calls teilweise
- **Stride**: Miss a, a+20 → fetch a+40, a+60
    - Behandelt Pointer Chasing (für Indexes) teilweise
- ✗ **Data Pointer Chasing**: Schwierig für Prefetcher
- **Real Hardware**: Prefetchers bleiben einfach (bessere Accuracy = mehr Komplexität!)

**Excursion: Caching & Prefetching from Storage**

- **Caching & Write Buffers**: ✅
    - OS cached Daten, flushed Writes nicht sofort
    - HDDs/SSDs haben interne DDR
    - Manche SSDs haben verschiedene Flash-Tiers
- **Ist transparentes Prefetching gut?** 🤔
    - Prefetching nicht so nützlich: Cost von falscher Speculation zu hoch
    - Aber Locality (temporal + spatial) bleibt wichtig!
    - Vorsicht: Spatial Data Layout in Flash kann für Software opak sein
- **"Prefetching" from App**: ✅ Gute Idee
    - Overlap Computation & Data Access
    - Pipelined Processing
    - Asynchronous Access

**Best Practices - Efficient Cache & TLB Use**

- **TLB**: Random Access über viele Pages vermeiden
    - Alternative Organisation? (Sorted Array vs. Hashtable für Ranges)
    - Huge Pages?
- **Prefetching**: Random Access mit Pointer Chasing vermeiden
    - Kann man Teile der "pointed to" Daten in High-Level DS hochziehen?
- **Cache Size**: Working Sets > LLC vermeiden
    - In Batches verarbeiten und dann kombinieren? (Extra Arbeit kann Speedup durch Caches wert sein!)
- **Tools**: perf mit CPU Performance Counters nutzen für Memory Hierarchy Issues!

**Summary**

- Memory Hierarchy: Caches + Main Memory – viele Layers mit verschiedenen Tradeoffs
- Management von Caches & Virtual Memory – Cost ist Benefit wert
- General Notions: Caching, Prefetching, Cache Coherence
- Konkretes Beispiel: Moderne CPU Cache Architecture

## 🖥️ Lecture 4: Inside a CPU (gesehen)

**Hardware Prefetching**

- **Next-Line Prefetching**: Miss a → fetch a+1
- **Stream Prefetching**: Miss a, a+1 → fetch a+2, a+3
    - ✓ Begünstigt Sequential Access & Spatial Locality
- **Stride Prefetching**: Miss a, a+20 → fetch a+40, a+60
    - Behandelt Pointer Chasing teilweise
- ✗ **Probleme**:
    - Instructions: Branches, Function Calls (Branch Prediction hilft)
    - Data: Pointer Chasing – üblich für Data Indexes (schwierig für Prefetcher)
- **Real Hardware**: Prefetchers bleiben einfach (bessere Accuracy = mehr Komplexität!)

**Caching & Prefetching from Storage**

- **Caching & Write Buffers**: ✅
    - OS cached Daten, flushed Writes nicht sofort
    - HDDs/SSDs haben interne DDR
    - Manche SSDs haben verschiedene Flash-Tiers (low latency / high capacity)
- **Transparentes Prefetching**: 🤔
    - Prefetching nicht so nützlich: Cost von falscher Speculation zu hoch
    - Aber Locality (temporal + spatial*) bleibt wichtig!
    - *Vorsicht: Spatial Data Layout in Flash kann für Software opak sein
- **"Prefetching" from App**: ✅ Gute Idee
    - Overlap Computation & Data Access
    - Pipelined Processing
    - Asynchronous Access

**Non-Uniform Memory Access (NUMA)**

- **Multi-Socket Systems**: Mehrere CPUs mit jeweils eigenem Memory
- **Threads kommunizieren durch Memory (Cache Hierarchy!)**
    - Threads auf gleichem Core: L1/L2 (wenn lucky)
    - Threads auf gleicher CPU: L3 (wenn lucky)
    - Threads auf verschiedenen CPUs: Main Memory
- **Cache Coherency Protocol**: Stellt sicher dass:
    - Daten nie korrupt sind bei Writes (physical view!)
    - Daten nie stale sind bei Reads (physical view!)
- **Coordination Cost**: Skaliert superlinear mit #Cores und #Sockets!

**Communication Latencies Across Cores**

- **Same Core** (L1/L2): <5 ns
- **Same CPU** (L3): ~80 ns
- **Different CPUs** (Main Memory): ~160 ns
- **Rule of Thumb**: 1:2 Ratio

**Communication Bandwidth Across Cores**

- **Same CPU**: 60-90 GB/s
- **Different CPUs**: 20-30 GB/s
- **Rule of Thumb**: 2:1 to 3:1 Ratio

**Linux & NUMA**

- **Default**: Prozesse werden random über CPUs gescheduled
- **Problem**: Physical Memory wird beim ersten Touch allokiert – Problem wenn Prozess herum-springt!
- **numactl**: Get statistics & pin processes
    - `numactl -H`: Zeigt NUMA Nodes, CPUs, Memory Sizes, Distances
    - `numactl --cpunodebind=0 --membind=0 someapp`: Pinne App zu Node 0

**Best Practices - Efficient Cache & TLB Use**

- **TLB**: Random Access über viele Pages vermeiden
    - Alternative Organisation? (Sorted Array vs. Hashtable für Ranges)
    - Huge Pages nutzen?
- **Prefetching**: Random Access mit Pointer Chasing vermeiden
    - Kann man Teile der "pointed to" Daten in High-Level DS hochziehen?
- **Cache Size**: Working Sets > LLC vermeiden
    - In Batches verarbeiten und dann kombinieren? (Extra Arbeit kann Speedup durch Caches wert sein!)
- **Tools**: perf mit CPU Performance Counters nutzen für Memory Hierarchy Issues!

**CPU Evolution**

- **Around 2005**: Dennard Scaling stopped
    - Single-Core CPUs → Multicore CPUs → Multisocket Multicore CPUs
    - Switching to Multicores kept Moore's Law alive
- **Moore's Law**: "Anzahl der Transistoren in einem dichten IC verdoppelt sich ca. alle 2 Jahre"
- **Dennard Scaling**: "Power Density bleibt konstant wenn Transistoren kleiner werden"
    - → **Für Moore's Law praktisch nutzbar braucht man Dennard Scaling!**
- **Ab 2005**: Transistor-Counts weiter gestiegen, aber Power & Clock Speeds hit the wall

**Types of Hardware Parallelism**

- **Vertical Parallelism** (Implicit - Almost Free Lunch):
    - **Single-Core**: Instruction & Data Parallelism
    - **Simultaneous Multithreading**: Threads teilen Execution Cycles auf gleichem Core
- **Horizontal Parallelism** (Explicit - Must Work Hard):
    - **Multicores**: Mehrere Threads laufen parallel auf verschiedenen Cores
    - **Multisocket Multicores**: Mehrere CPUs in einer Maschine
    - **Distributed Systems**: Programm läuft über mehrere Maschinen

**Instruction Stages (Simplified RISC CPU)**

1. **Fetch**: Instruction aus Cache holen
2. **Decode**: Operation + benötigte Inputs identifizieren
3. **Execute**: Operation ausführen
4. **Memory**: Memory Access falls nötig
5. **Write**: Ergebnisse in Register schreiben

**Subscalar CPU (No Implicit Parallelism)**

- **One Instruction at a Time**
- Mehrere Cycles pro Instruction (5+ Cycles für eine einfache Instruction)
- Sehr ineffizient

**Instruction Pipelining**

![image.png](attachment:566250b7-5d33-4118-a1c7-a12fc3cc8a33:image.png)

- **Fundamental Way to Parallelize Implicitly**
- Stages verschiedener Instructions überlappen
- → Mehrere Instructions gleichzeitig in verschiedenen Stages
- Deutlich effizienter als Subscalar

**Superscalar CPU**

- **Issuing Multiple Instructions in a Cycle**
- Beispiel: 4-Way Superscalar CPU = 4 Instructions parallel fetchbar/decodierbar/...
- **Modern Processors**: Hyper-Threading basiert darauf

**Out-of-Order (OoO) Execution**

- **Idee**: Prozessor führt Instructions basierend auf **Data Availability** aus, nicht strikt nach Program Order
- **Beispiel**:
    - (1) r1 ← r2 / r3
    - (2) r4 ← r1 + r5 (abhängig von (1))
    - (3) r6 ← r7 * r8 (unabhängig!)
    - → (3) kann parallel zu (1)+(2) oder sogar **vor** (1)+(2) ausgeführt werden
- **Hyper-Threading**: Nutzt OoO Execution um Ressourcen busy zu halten

**Branch Prediction 101**

- cpu merkt in decode step when sprung oder so un instruction nicht ausgeführt werden soll
- **Branch Prediction Unit (BPU)**: Beantwortet:
    - a) Wird der Branch bei Address @ genommen?
    - b) Wenn ja, zu welcher Target Address?
- **Verschiedene Branch-Typen**: CPUs predicten Loops, Jumps, IFs mit unterschiedlicher Logik
- **Implementierung**: In Hardware, komplex!
- **1-bit Last-Time Predictor**: "Toy Example"
    - Verwendet Branch History Table (BHT): 1 Bit pro Branch speichert ob letztes Mal taken
- **Modern CPUs**: Betrachten viel Execution History
    - Manche AMD Prozessoren hatten sogar **Neural Network-based Predictors**!

**Branch Prediction - With vs. Without**

- **Ohne Branch Prediction**:
    - Nach Jump: Fetch/Decode/Execute der nachfolgenden Instructions → dann verwerfen (Pipeline Flush)
    - Mehrere Cycle Penalty
- **Mit Branch Prediction**:
    - CPU "rät" Jump Target bereits im Decode-Stage
    - Bei korrekter Prediction: Kein Stall!
    - Bei falscher Prediction: Pipeline Flush (aber seltener)

**How to Remove Branching Code?**

- **Trade-off**: Mehr Compute für keine Branches
- **Beispiel**:
    - **Mit Branch**: `if ([prev.date](<http://prev.date>).month<[cur.date](<http://cur.date>).month) then months.insert(i); m++; changed=true; end if`
    - **Ohne Branch**: `mdelta = [cur.date](<http://cur.date>).month - [prev.date](<http://prev.date>).month; m+=mdelta; months[m]=i; changed=mdelta`
- **Annahme**: Monate monoton steigend, keine "Löcher"
- Macht Sinn wenn Branch schwer vorhersagbar

**CISC vs. RISC**

- **CISC (Complex Instruction Set Computing)**:
    - Instructions intern komplex (Micro-Code)
    - Variable Execution Time
    - Spart Memory, einfacher zu kompilieren
    - Genutzt in **x86 CPUs**
- **RISC (Reduced Instruction Set Computing)**:
    - Instructions führen in vorhersagbarer (gleicher) Zeit aus
    - Komplexer zu kompilieren, mehr Memory (heute kein problem mehr)
    - Genutzt in **ARM CPUs**
- **In Praxis**: Moderne CPUs sind Hybrids, nicht so verschieden!

**Modern CPUs - "Internal Accelerators"**

- **Floating Point Unit (FPU)**: Mehrere Units, shared über Cores (nicht immer 1:1!)
- **Vectorized Instructions**: Data-parallel Operations (SIMD) → diskutiert nächste Woche
- **Cryptographic Operations**: Partial Hardware Implementations (z.B. Intel AES-NI)
- **Neural Processing Units (NPUs)**: Tensor-Style Operations (z.B. AMD AI Engines in Consumer CPUs)

**Multi-Socket Machines**

- **Interconnect** zwischen CPU Dies
- Zwei separate CPU Dies mit jeweils:
    - Cores, L1/L2 Caches, L3, Main Memory
- Modern: Mesh Interface für Inter-CPU Communication

**Summary**

- Modern Servers: Multiple CPUs, Multi-Core, Hyper-Threaded Architecture
- We (can) control Multi-Core/NUMA Execution from outside
- Hyperthreading wird intern von CPU gehandhabt
- **Efficient Execution**: CPU muss korrekt spekulieren können (Prefetching, Branch Prediction)
- **Efficient Software**: Sollte alle CPU Features nutzen – zumindest nicht dagegen arbeiten!

## 🔢 Vorlesung 5: Vectorized Execution on CPUs

**Execution in Modern CPUs - Reminder**

- CPUs haben **10-20 Cores** (multi-core)
- Jeder Core hat **sophisticated execution strategies**:
    - **Instruction Pipelining**: Stages verschiedener Instructions überlappen
    - **Superscalar Execution/Hyperthreading**: Multiple Instructions pro Cycle
    - **Out-of-Order Execution**: Dependencies checken und Instructions reordern
- **+ CPU Extensions** für vektorisierte Execution

**Vectorized Execution - Grundlagen**

- **Scalar Instruction**: Verarbeitet eine Operation (z.B. add) zur Zeit
- **Vectorized Instruction (SIMD)**: Verarbeitet eine Operation auf **mehreren Datenelementen** gleichzeitig
- **SIMD** = **Single Instruction Multiple Data**
- **Beispiel**: Addition von zwei Arrays
    - Scalar: `Z[i] = X[i] + Y[i]` für jedes i einzeln
    - SIMD: 4 (oder 8) Additionen gleichzeitig in einem Instruction

**SIMD Instruction Types**

1. **Data Movement**: Load/Store in SIMD registers
2. **Arithmetic Operations**: ADD, SUB, MUL, DIV, SQRT, MAX, MIN
3. **Bitwise Operations**: AND, OR, XOR
4. **Comparison/Shuffle**: Vergleichen, Daten zwischen Registern verschieben
5. **Miscellaneous**: Konversion, Cache Control

**Vectorization Options**

- **Choice #1: Automatic by Compiler**
    - Compiler findet vektorisierbaren Code automatisch
    - Funktioniert nur für "simple loops"
    - In der Praxis selten
- **Choice #2: Compiler Hints**
    - `restrict` Keyword: Teilt Compiler mit dass Arrays distinct sind
    - `#pragma ivdep`: Ignoriere Loop Dependencies
- **Choice #3: Explicit Vectorization**
    - CPU Intrinsics manuell nutzen
    - Volle Kontrolle, aber nicht portable
    - Beispiel: `_mm256_load_ps()`, `_mm256_add_ps()`, `_mm256_store_ps()`

**Vectorization Challenges**

**1. Dependencies**

- Code ist nur vektorisierbar wenn **independent steps** parallel ausführbar sind
- **Problem**: Read-After-Write (RAW) und Write-After-Read (WAR) Hazards

**2. Branching**

- **Problem**: Branches verhindern Vektorisierung

```cpp
for (i = 0; i < n; i++) {
    if (X[i] < 50) {
        X[i] = 2*X[i];
    }
}
```

- **Lösung: Predication**

```cpp
for (i = 0; i < n; i++) {
    X[i] = ((X[i] < 50)+1) * X[i];
}
```

- **Masking**: Vergleich erzeugt Mask → AND mit Mask → bedingte Operation ohne Branch
- **Intrinsics**: `_mm256_cmpgt_epi32()`, `_mm256_and_si256()`, `_mm256_blendv_epi8()`

**3. Loop-Carried Dependencies**

- **Problem**: Dot Product

```cpp
for (i=0; i<n; i++) {
    sum = sum + X[i] * Y[i];  // Dependency!
}
```

- **Lösung: Reduction mit Partial Sums**

```cpp
// Step 1: Compute independent partial sums
partial_sums[4] = {0,0,0,0};
for (i=0; i<n; i+=4) {
    for (j=0; j<4; j++) {
        partial_sums[j] += X[i+j] * Y[i+j];
    }
}
// Step 2: Reduce partial sums
for (j=0; j<4; j++) {
    sum += partial_sums[j];
}
```

- Inner Loop ist vektorisierbar!

**4. Non-Divisible Array Sizes**

- **Problem**: Was wenn n nicht durch SIMD-Width teilbar?
- **Lösung**: Split in "clean" part + "corner case"

```cpp
int split_point = n - (n%4);
// Vectorized part
for (i=0; i<split_point; i+=4) { ... }
// Scalar corner case (<4 iterations)
for (i=split_point; i<n; i++) { ... }
```

**SIMD in Database Operations**

- **Table Scans**: Columnar Data scannen + filtern (gut für SIMD!)
- **Joins**, **Sorting**, **Aggregation**
- **Dense Data**: SIMD sehr effektiv
- **Sparse Data**: Reshape nötig → Overhead
- **Presented in ADMS Course** (Spring Semester)

**Memory Wall Problem**

- **Peak Performance Beispiel** (Core i7-960, 2010):
    - 102 Single-Precision GFLOPs
    - 2 loads + 1 store = 12 bytes/FLOP → **über 1 TB/s** nötig!
    - Actual Memory Bandwidth: **32 GB/s**
- **Konsequenz**: Peak SIMD-Utilization nur wenn **Daten im Cache**!
- **Viele Workloads sind memory-bound** statt compute-bound
    - SAXPY (Dot Product): BW bound
    - SpMV (Sparse Matrix-Vector): BW bound
    - Convolution: Compute bound (große Filter) oder BW bound (kleine Filter)

**Example Performance: Scalar SIMD Selection**

- **Dense Input**: 8.4× Speedup
- **Sparse Input**: 2.7× Speedup
- **TPC-H Q6**: 1.4× Speedup
- **Grund**: Filter ist großer Teil der Execution Time, aber Ende-zu-Ende hängt von anderen Operations ab

**Scatter-Gather Operations**

- **Sparse SAXPY**: Indirekte Zugriffe über Index-Arrays K und M

```cpp
for (i = 0; i < n; i++) {
    X[K[i]] = a * X[K[i]] + Y[M[i]];
}
```

- **Vectorization möglich** wenn keine Collisions in K
- **Aber**: Scatter-Gather ist **viel langsamer** (kein Sequential Access!)

**Explicit SIMD Examples**

**SAXPY**

```cpp
// Scalar
for (int i = 0; i < n; i++) {
    X[i] = a*X[i] + Y[i];
}
```

```cpp
// SIMD (AVX2, 256-bit)
const __m256 scalar = _mm256_set1_ps(a);
for (int i = 0; i < n; i+=8) {
    __m256 xs = _mm256_loadu_ps(X + i);
    __m256 ys = _mm256_loadu_ps(Y + i);
    __m256 dst = _mm256_fmadd_ps(scalar, xs, ys);
    _mm256_storeu_ps(X + i, dst);
}
```

**Conditional Sum mit Masking**

```cpp
// Scalar
for (int i = 0; i < n; i++) {
    if (X[i] > 50) {
        sum = sum + X[i];
    }
}
```

```cpp
// SIMD
const __m256i condition = _mm256_set1_epi32(50);
__m256i partial_sums = _mm256_set1_epi32(0);
for (int i = 0; i < n; i+=8) {
    __m256i xs = _mm256_load_si256((__m256i*)(X + i));
    __m256i mask = _mm256_cmpgt_epi32(xs, condition);
    xs = _mm256_and_si256(xs, mask);
    partial_sums = _mm256_add_epi32(partial_sums, xs);
}
// Reduce partial_sums to single value
for (int i = 0; i < 8; i++) {
    sum += partial_sums[i];
}
```

**Useful Intrinsics für Branching**

- `_mm256_blendv_epi8(a, b, mask)`: Kombiniert zwei Vektoren basierend auf Mask
- `_mm256_blend_epi32(a, b, imm8)`: Blend mit 8-bit Integer Mask
- `_mm256_maskload_epi32(addr, mask)`: Load mit Mask
- `_mm256_maskstore_epi32(addr, mask, a)`: Store mit Mask

**Resources**

- **Intel Intrinsics Guide**: [intel.com/intrinsics-guide](http://intel.com/intrinsics-guide)
- **Cheat Sheet**: [db.in.tum.de/~finis/x86](http://db.in.tum.de/~finis/x86) intrinsics cheat sheet
- **Examples**: [en.algorithmica.org/hpc/simd/masking](http://en.algorithmica.org/hpc/simd/masking)
- **Compiler Explorer**: [godbolt.org](http://godbolt.org)

**Best Practices**

- **Use Intrinsics** wenn du genau weißt was du tust und Code non-trivial ist
- **Otherwise**: Code einfach schreiben + Compiler Hints + hoffen
- **Best Choice**: Libraries für deine Domain nutzen (BLAS, Eigen, etc.)
- **Vorsicht**: SIMD limitiert auf CPUs wenn Daten nicht im Cache oder Computational Intensity sehr niedrig

**Summary**

- SIMD auf CPUs kann Performance-Boost bringen, ist aber **challenging**
- **Challenges**: Dependencies, Branching, Loop-Carried Dependencies, Memory Bandwidth
- **Solutions**: Predication, Masking, Reduction, Tiling, Intrinsics
- Viele Probleme sind **memory-bound** bevor sie compute-bound sind
- Vectorization hat **limited benefits** wenn Working Set > Cache

## Vorlesung 6: Concurrency & Parallelism (gesehen)

### **Amdahl's Law**

- **Formel**: `Speedup = 1 / ((1-p) + p/s)`
    - `s` = parallelism factor (Anzahl Cores/Threads)
    - `p` = fraction of app parallelized
- **Key Insight**: Mehr Cores bringt nichts wenn parallel portion klein ist
- **Beispiel**: Bei 50% parallel portion → max. 2× Speedup (auch mit ∞ Cores!)
- **Bei 90% parallel portion**: 10× Speedup bei ~32 Cores, dankt flacht ab
- **Bei 95% parallel portion**: ~20× Speedup bei ~1000 Cores
- **Lösung**: Parallel portion erhöhen durch:
    - Algorithmus ändern
    - Data movement reduzieren
    - Synchronization minimieren

### **OS Concepts - Processes & Threads**

**Processes vs. Threads**

- **Processes**: Separate Address Space, separate Resources
    - Per-process: Address space, Global variables, Open files, Child processes, Alarms, Signals
- **Threads** (within Process): Shared Address Space, separate Execution State
    - Per-thread: Program counter, Registers, Stack, State
- **User Space Threads (Co-routines)**: Mapped to OS threads

**Multi-threaded Architecture - Vorteile**

- ✅ Same memory address space → einfacher Data Sharing
- ✅ Less overhead per context switch

**Multi-threaded Architecture - Nachteile**

- ❌ Single thread crash → gesamter Process (DBMS) crasht
- ❌ Multi-threaded app kann nicht über Maschinen skalieren

**Wichtig**: Multi-threaded ≠ parallel!

- Man kann auch Parallelism innerhalb eines Threads haben (SIMD, ILP)

### **OS Scheduling**

**OS kann Threads/Processes switchen bei:**

- Process exits (must)
- Thread blockiert auf I/O oder Semaphore (must)
- Thread wird erstellt
- I/O interrupt oder Clock interrupt

**Cost of Scheduling**

- **Scheduling Decision**: Software, braucht CPU time! (Zeit nicht für Processing)
- **Context Switch (Dispatch)**: Flush CPU pipeline, load register state, ggf. flush TLB + lose cache locality
- **Balance**: Scheduler complexity vs. Quality of schedule
- **Linux**: CFS (Completely Fair Scheduler) und EEVDF

### **System Calls**

- **Zweck**: Interaction mit I/O und OS Features
- **Cost**: **Orders of magnitude teurer** als Function Calls!
- **Warum teuer?**: User space → Kernel space transition (siehe Diagram)
    - Push arguments, Trap to Kernel, Check syscall#, Dispatch, Execute, Return, Pop arguments
- **Trend**: System calls werden **nicht schneller** über Zeit
    - Security patches (Spectre, Meltdown) haben Syscalls verlangsamt
    - Quelle: "An analysis of performance evolution of Linux's core operations" (SOSP'19)

### **Synchronization - Warum nötig?**

**Problem: Race Conditions**

```cpp
// Thread 1              Thread 2
while (done==0)         sum = sum + 1
    do nothing          done = 1
read(sum)
```

- Ohne Synchronization: Undefiniertes Verhalten!

**Was können wir annehmen?**

- ✅ **Cache line level atomicity** für Load/Store
- ✅ **Ordering von dependent instructions**
- ❌ Code concurrent auf CPUs kann in vielen (unexpected) Ways interleaved werden
    - Out-of-Order Execution, Compiler Reordering

### **Synchronization Mechanisms**

**Software / OS-based** (require "sleeping"):

- **Semaphores**: Counting semaphore für Resource Management
- **Mutex (Lock)**: Binary lock für Critical Sections
- → Thread blockiert und wird vom OS gescheduled wenn Condition nicht erfüllt

**Hardware-based** (require "spinning"):

- **Compare and Swap (CAS)**: Atomares Read-Modify-Write
- **Fetch and Add**: Atomares Increment
- **Atomic Logical Ops**: AND, OR, XOR
- → Thread spinnt in Loop bis Condition erfüllt

**Fences**

- Ensure dass Instruction nicht vor vorherigen Loads/Stores ausgeführt wird
- Memory ordering Garantien

### **FUTEX (Fast Userspace Mutex)**

- **Best of Both Worlds**: HW Atomics + OS Scheduling
- **Design-Beobachtung**: Most locks are not contended
- **Mutex Beispiel**:
    1. Thread versucht Lock mit Test-and-Set (HW atomics): 0 = unlocked, 1 = locked
    2. Bei Failure: Syscall → OS puts thread in waiting queue (kernel space, yield)
    3. Nach Unlock: Syscall → OS wakes up waiting thread
- **Performance**: Bis zu 100,000s ops/s
- **Kann implementieren**: Semaphores, Mutex, RW Locks, etc.

### **Reader/Writer Pattern**

**Problem**: Nicht jeder Thread muss shared state modifizieren → zahlt aber für Synchronization!

**Lösung: RW Locks**

- **Writers**: Exclusive access
- **Readers**: Concurrent access (solange kein Writer)

**Beispiel**: Database

- Viele Queries (Readers) → Account Balances berechnen
- Wenige Updates (Writers) → Money Transfers

**Problem**: Was wenn Writer sehr lange im exclusive section?

### **Copy-on-Write (CoW)**

**Ziel**: Multiple Threads/Processes auf shared data ohne Copies, ohne lange Waits für Writers

**Annahme**: One level of indirection (z.B. Array of Objects, Pages)

**Mechanismus**:

- **Readers**: Lockless reads
- **Writers**:
    1. Make copy of data
    2. Modify copy
    3. Atomically update pointer in parent structure

**Problem**: Wie weiß Reader dass Daten up-to-date sind?

- Ist Pointer-Value checken genug?
- Was wenn nach mehreren Changes Pointer wieder gleich ist wie "old"?

### **Locking Performance - Implications**

**Quelle**: "Scalable and Robust Latches for Database Systems" (28)[^28]

**Contention Handling** (exklusiver Lock):

- **Test-and-set**: Linear degradation mit #threads
- **Local Spinning**: Besser, aber immer noch degradation
- **TicketLock variants**: Beste Performance unter hoher Contention
- **OS mutex (std::mutex)**: Schlechteste Performance (Syscall Overhead!)
- **ParkingLot**: Gute Balance

**OLTP vs. OLAP**:

- **OLTP** (viele Updates): Lock-Wahl sehr wichtig!
    - Exclusive-Spinlock: Bricht bei ~20 threads ein
    - Optimistic/Hybrid-Lock: Skaliert bis 40 threads
- **OLAP** (wenige Updates): Alle Methoden ähnlich gut
    - Writes sehr selten → Contention minimal

### **Parallel Processing Patterns**

▶#### **Dataflow/Pipeline Pattern**

- **Idee**: Arbeit in Pipeline-Stages aufbrechen
- **Jede Stage**: Kann parallel oder sequential sein
- **Vorteil**: Code locality in jeder Stage → höhere Effizienz

**Data Passing**: FIFO Buffers (Circular Buffer)

- Arbeitet auf Granularität von Batches
- Genutzt in: Disk I/O, Networking, PCIe Data Transfer

**Beispiel: Blockchain Consensus Pipeline**

- Stages: Unmarshal → Hash&Verify → Decide → Hash → Sign/Auth → Marshal → Networking
- Crypto Operations: Data-parallel innerhalb Stage

**Goal**: Jede Stage so dimensionieren dass gleicher Throughput

- Pipeline-Speed = Slowest Stage
- Nützliche Parallelität variiert stark zwischen Stages!

▶#### **NUMA & Synchronization**

**Performance Degradation bei NUMA**:

- **Locking-heavy Code**: Leidet stark unter NUMA
    - Syncing ist **latency-sensitive** Operation!
- **Pipeline-structured Apps**: Weniger betroffen
    - Batch-Sending ist **bandwidth-sensitive** Operation

**Communication Latencies** (Reminder):

- Same Core (L1/L2): <5 ns
- Same CPU (L3): ~80 ns
- Different CPUs (Main Memory): ~160 ns
- **Rule of Thumb**: 1:2 Ratio

**Communication Bandwidth**:

- Same CPU: 60-90 GB/s
- Different CPUs: 20-30 GB/s
- **Rule of Thumb**: 2:1 to 3:1 Ratio

**Konsequenz**: Wenn App compute-heavy → Benefit von mehr Threads überwiegt zusätzliche Sync-Kosten

- Gilt auch für distributed data processing pipelines (z.B. ML Training mit Parameter Server)

### **Summary**

- **Amdahl's Law**: Mehr Cores ≠ automatisch Speedup → parallel portion erhöhen!
- **OS Scheduling**: Context switches sind teuer (Pipeline flush, TLB flush, Cache locality loss)
- **System Calls**: Orders of magnitude teurer als Function Calls
- **Synchronization Mechanisms**:
    - Software/OS: Semaphores, Mutex (sleeping)
    - Hardware: CAS, Fetch-and-Add (spinning)
    - FUTEX: Best of both worlds
- **Patterns**:
    - Reader/Writer Locks: Concurrent reads, exclusive writes
    - Copy-on-Write: Lockless reads für Writers mit infrequent updates
    - Dataflow/Pipeline: Break work into stages mit FIFO buffers
- **Locking Performance**: Stark abhängig von Workload (OLTP vs. OLAP) und Contention
- **NUMA**: Synchronization ist latency-sensitive → Performance degradation bei multi-socket

## Vorlesung 7: GPUs (gesehen) - Ab hier fur Quiz

[Lecture_07_GPUs.pdf](attachment:10209283-fefd-4cf6-9955-e1b2bab2d281:Lecture_07_GPUs.pdf)

- Multicore Performance stagniert → Accelerators (GPUs, TPUs, FPGAs und ASICs)
- GPGPU → Origin GPU nur fyr Grafik GP auch fyr generelle workloads
- Multi GPU mit NVLINK
- SM besteht aus Cores (FP64, FP32, INT32, Tensor)
- APIs fyr GPGPU OpenCL/CUDA
- CPU thread OS scheduled
- Kernel = A function that should be executed using parallel threads in grid

### **GPU Architecture Basics**

- **CPU vs GPU**: CPU optimiert für Latency (wenige, schnelle Cores), GPU für Throughput (viele, langsamere Cores)
- SM (Streaming Multiprocessor) mit Register, Cache und Local memory
- **SIMT (Single Instruction Multiple Threads)**: Viele Threads führen gleiche Instruktion auf unterschiedlichen Daten aus
- **Warps/Wavefronts**: Gruppen von 32 (NVIDIA) oder 64 (AMD) Threads die zusammen ausgeführt werden
- **Branch Divergence**: Performance-Problem wenn Threads in einem Warp unterschiedliche Pfade nehmen

### **GPU Memory Hierarchy**

- **Global Memory**: Großer DRAM (GB-Bereich), langsam (~100-200 cycles), von allen Threads erreichbar
- **Shared Memory**: Klein (~KB), schnell (~5-10 cycles), innerhalb eines Thread-Blocks geteilt
- **Registers**: Sehr schnell (1 cycle), pro Thread privat, begrenzte Anzahl
- **L1/L2 Cache**: Automatisch verwaltet, zwischen Shared Memory und Global Memory
- **Memory Coalescing**: Benachbarte Threads sollten benachbarte Memory Addresses zugreifen für optimale Bandwidth

### **GPU Programming Model**

- **Grid → Blocks → Threads**: Hierarchische Organisation der Parallelität
    
    ![grafik.png](attachment:ac0a208f-eea1-4017-bc2f-71be684e1a1c:grafik.png)
    
    ![grafik.png](attachment:cfeaa38f-bc2d-49c3-a1d6-dfeaad3dc884:grafik.png)
    
    - SM fuhrt block aus
    - In jedem Takt werden dann Warps diesen Blocks ausgefyhrt (kann mehr als 1 sein)
    - Vorteil von 2. ist Occupancy da weniger threads im idle weil man mehr fine grained ausfyhren kann
- **Kernel Launch**: `kernel&lt;&lt;&lt;numBlocks, threadsPerBlock&gt;&gt;&gt;(args)`
    
- **Thread Indexing**: `threadIdx`, `blockIdx`, `blockDim`, `gridDim`
    
- **Occupancy**: Verhältnis von aktiven Warps zu maximal möglichen Warps
    
- **Latency Hiding**: Viele Threads schedulen um Memory Latency zu verbergen
    

### **GPU Performance Optimization**

- **Maximize Occupancy**: Genug Threads/Blocks um alle SMs auszulasten
- **Minimize Branch Divergence**: Conditional Code vermeiden oder umstrukturieren
- **Coalesced Memory Access**: Sequential Memory Access Patterns
- **Use Shared Memory**: Für häufig verwendete Daten (z.B. Tiling in Matrix Multiplication)
- **Minimize Host-Device Transfers**: PCIe Bandwidth ist limitiert (~16 GB/s)
- **Async Operations**: Computation und Memory Transfers überlappen

![grafik.png](attachment:03cd02c4-c0bd-4692-8a0c-e0915a3335d1:grafik.png)

- zweites besser weil speicher zusammenhqngend und memreads weniger

### CUDA: WARPS AND LATENCY HIDING

![grafik.png](attachment:c29fe59a-2658-452c-b5e5-1f48001c8e26:grafik.png)

Rechnungen

- Warp schedule = 4 Cycles
- Register load data 24Cycles
- GLobal mem access = 400 cycles
- → 24/4 = 6 (heist 6 warps um register acc zu hiden)
- → 400/4 = 100 warps um mem accc zu hiden
- → Alle 8 cycles reg zugriff = 24/8 = 3 warps
- → Alle 8 cycle mem zugriff = 100/8 = 12.5

![grafik.png](attachment:86dc68a7-6236-489c-93df-230212ac3c0a:grafik.png)

### **GPU Use Cases**

- **Matrix Operations**: Dense Linear Algebra (BLAS, cuBLAS)
- **Deep Learning**: Training und Inference (Tensor Cores)
- **Graphics Rendering**: Ray Tracing, Rasterization
- **Scientific Computing**: Simulations, FFT, Monte Carlo
- **Data Analytics**: Sorting, Filtering, Aggregation (bei regulären Daten)
- **Nicht geeignet für**: Irregular Memory Access, High Branch Divergence, Small Datasets

![grafik.png](attachment:039625b7-380e-4fc0-9574-3c3ed0a770cb:grafik.png)

### **GPU Programming APIs**

- **CUDA**: NVIDIA-spezifisch, am weitesten verbreitet
- **HIP**: AMD, CUDA-ähnliche API
- **OpenCL**: Platform-agnostic, komplexer
- **SYCL**: Modern C++ Abstraction über OpenCL
- **Higher-Level**: cuDNN, TensorFlow, PyTorch (für ML)

### **Summary**

- **GPUs**: Massiv parallel, optimiert für Throughput statt Latency
- **SIMT Model**: Tausende Threads führen gleiche Operationen auf verschiedenen Daten aus
- **Memory Hierarchy**: Registers → Shared Memory → L1/L2 → Global Memory
- **Performance Keys**: Occupancy, Coalesced Access, Shared Memory nutzen, Branch Divergence vermeiden
- **Best für**: Regular, data-parallel Workloads mit hoher Arithmetic Intensity
- **Nicht gut für**: Irregular Access Patterns, hohe Branch Divergence, kleine Datasets

## Vorlesung 8: FPGAs (gesehen)

[Lecture_08_Accelerators_FPGA_TPU.pdf](attachment:066fd3a2-3aea-49fe-b943-9f0813b7caaa:Lecture_08_Accelerators_FPGA_TPU.pdf)

![grafik.png](attachment:286d0d1f-b2ce-4d51-b1e8-0913c9a084d8:grafik.png)

**CGRA = Coarse-Grained Reconfigurable Architectures**

NIC = Network Interface Cards

Single Core Performance bleibt gleich → mehr parallelismus oder mehr specialisierte hardware

### Integration von Accelaratoren

![grafik.png](attachment:c2e6dd2e-577c-438a-96da-78ee7d794605:grafik.png)

![grafik.png](attachment:3bd4d542-f531-4bde-9587-c26cbfc7a718:grafik.png)

![grafik.png](attachment:740c517f-fffc-408d-af1e-a69f4b5d6dfa:grafik.png)

ADaptive Intelligence Engines (AMD)

- Sind CRGA aber mit very long isntruction words wodurch isntruction kram komplexitqt geringer und dadurch mehr platz vor compute power → more efficient

### **FPGA Basics**

- **FPGA (Field-Programmable Gate Array)**: Rekonfigurierbare Hardware zwischen CPU (flexibel, langsam) und ASIC (schnell, unflexibel)
    - **Aufbau**: Gitter aus konfigurierbaren Logic Blocks (CLBs), Switch Boxes, I/O Blocks
- **CLB Komponenten**: LUTs (Look-Up Tables), Flip-Flops, Multiplexer, Carry Logic
- **LUT (Look-Up Table)**: Kleine Memory (z.B. 6-input → 64-bit SRAM) die beliebige Boolean-Funktion implementieren kann
- **Programmierung**: HDL (Hardware Description Languages) wie Verilog, VHDL, oder High-Level Synthesis (HLS) mit C/C++

### **FPGA vs CPU/GPU**

- **Vorteile**:
    - Custom Datapaths: Exakte Bit-Widths (z.B. 17-bit statt 32-bit)
    - Massive Parallelität: Tausende custom Operations gleichzeitig
    - Low Latency: Keine Instruction Fetch/Decode Overhead
    - Energy Efficiency: Nur benötigte Logic aktiv
- **Nachteile**:
    - Clock Speed: 100-500 MHz (vs. CPU 3-5 GHz)
    - Entwicklungsaufwand: Komplexes HDL Programming
    - Resource-limitiert: Begrenzte LUTs/DSPs/Block RAM
    - Rekonfigurationszeit: Sekunden bis Minuten

### **FPGA Architecture Details**

- **DSP Blocks**: Spezialisierte Hardware für Multiply-Accumulate (MAC) Operations
- **Block RAM (BRAM)**: On-chip Memory (KBs-MBs), schneller als External DRAM
- **I/O Blocks**: High-Speed Serial Interfaces (PCIe, Ethernet, etc.)
- **Routing**: Programmable Interconnects zwischen CLBs
- **Clock Management**: PLLs für verschiedene Clock Domains

### **FPGA Programming Models**

- **HDL (Verilog/VHDL)**:
    - Low-Level, explizite Hardware-Beschreibung
    - Volle Kontrolle, steile Lernkurve
- **High-Level Synthesis (HLS)**:
    - C/C++ Code → Hardware (z.B. Xilinx Vitis, Intel OpenCL)
    - Pragmas für Parallelisierung: `#pragma HLS PIPELINE`, `#pragma HLS UNROLL`
    - Einfacher für Software-Entwickler, weniger Kontrolle
- **OpenCL for FPGAs**: Portabel zwischen GPU/FPGA, automatisches Routing

### **FPGA Use Cases**

- **Signal Processing**: Custom Filter, FFT, Compression
- **Networking**: Packet Processing, Crypto Offload, Low-Latency Trading
- **Database Acceleration**: Scan/Filter/Join Offload
- **AI Inference**: Custom Precision Neural Networks (z.B. 4-bit Quantization)
- **Prototyping ASICs**: Hardware-Verifikation vor Tape-Out
- **Nicht geeignet für**: Control-Heavy Code, Irregular Branching, Dynamic Workloads

### **TPUs (Tensor Processing Units)**

- **ASIC** von Google für ML Training/Inference
- **Systolic Array**: 2D Grid von MAC Units für Matrix Multiplication
- **Optimiert für**: Dense Matrix Operations, niedrige Precision (BF16, INT8)
- **Memory**: High-Bandwidth Memory (HBM), on-chip SRAM für Weights
- **Performance**: 100-400 TOPS (Tera Operations per Second)
- **Vorteile**: Extrem energie-effizient für spezifische ML Workloads
- **Nachteile**: Nicht rekonfigurierbar, nur für ML nutzbar

### **Summary**

- **FPGAs**: Rekonfigurierbare Hardware, custom Datapaths, niedrige Latency
- **Architektur**: CLBs mit LUTs/Flip-Flops, DSP Blocks, Block RAM, Routing
- **Programming**: HDL (low-level) oder HLS (high-level C/C++)
- **Vorteile**: Custom Precision, massive Parallelität, Energy Efficiency
- **Nachteile**: Niedrige Clock Speed, komplexe Entwicklung, limitierte Resources
- **Use Cases**: Signal Processing, Networking, Database Acceleration, AI Inference
- **TPUs**: Specialized ASICs für ML (Systolic Arrays), extrem effizient aber unflexibel

## Vorlesung 9: Networking (gesehen)

[Lecture_09_Networking_Part1.pdf](attachment:0eaeaeda-e874-4536-a6ef-f0cf63fa5654:Lecture_09_Networking_Part1.pdf)

### **Networking Basics**

- **OSI Model**: 7 Layers (Physical, Data Link, Network, Transport, Session, Presentation, Application)
- **TCP/IP Model**: 4 Layers (Link, Network/IP, Transport, Application)
- **Protocols**: TCP (reliable), UDP (fast, unreliable), HTTP/HTTPS (Web), DNS (Name Resolution)
- **IP Addressing**: IPv4 (32-bit), IPv6 (128-bit), Subnetting, CIDR Notation
- **Routing**: Forwarding Packets zwischen Networks, Routing Tables, BGP

### Socket Interface

- Zwischen Application und Transport layer

![grafik.png](attachment:93304653-56ff-45ce-a22b-63c3fe3862c0:grafik.png)

- Empfange ist komplexer, weil asynchron und interrupts + polling
    - Entweder Blocking thread bis receive → Viele threads fur viele connections
    - Oder Non-Blocking → EIn thread kummert sich um mehrere

### CPU Bottleneck

- Perfomance stagniert und kann somit zum bottleneck werden (Weil PArallelsierung ist schwer)
- Network wird aber immer schneller

![grafik.png](attachment:9f3ecfe3-ea97-4715-b609-c0af13b994c9:grafik.png)

### How many Caches misses can we afford?

10Gbps; Ethernet Frame Size 84 bytes; 67ns zwischen packets (14.88 Mpps);

L1$ = 1 ns, L2$ = 5 ns, LLC$ = 30 - 40 ns, DRAM = 60 - 100 ns

- 84 bytes / 10GBps = 67ns
- 1s / 67 ns = 14,88 Mpps
- Allowed Cache misses → MAybe 1 DRAM Access

100Gbps

- 6,7 ns
- 148,8 Mpps
- Allowed Cache misses → Nur ein paar L1 und L2 erlaubt

### OVERHEAD: SIGNIFICANT ROLE OF OS

![grafik.png](attachment:fc635c66-2288-45cc-84fe-b2072b019be2:grafik.png)

![grafik.png](attachment:a8d9e1b5-2adc-4822-9b42-ec39f8f2a7b2:grafik.png)

→ Losung: Wir versuchen OS zu reduzieren User SPace Networking

### USer SPace Networking

![grafik.png](attachment:baa13144-5d89-4457-b0af-760f7d1e7cf0:grafik.png)

data operation direkte communication mit net stack

![grafik.png](attachment:94310a30-1f08-49c1-8058-dfd591a480ca:grafik.png)

### DPDK FrameWork

Data Plane Development Kit

- Von Intel um zu zeigen wie schnell ihre CPUs sind
- Ist der schnellste packet processing framework
- Control und Data Plane im user space
- Keine sys calls alles mit polling
- Keine treiber anpassung nptig

![grafik.png](attachment:0f2f3cce-2196-47d5-a462-45305883d6b5:grafik.png)

![grafik.png](attachment:70455a91-a41a-47f7-a1cc-3fa4fca6772a:grafik.png)

![grafik.png](attachment:7cf07787-0c9a-47f1-adb8-d83cb8bb4135:grafik.png)

### REMOTE DIRECT MEMORY ACCESS (RDMA)

- Not socket-based - has its own programming API and abstractions
- The goal: make network operations ~= local compute operations

![grafik.png](attachment:0a7fcd92-aef0-43fa-b263-e779aa9a0b04:grafik.png)

![grafik.png](attachment:099ab4e5-f365-417a-ae3d-6c75b80d1c09:grafik.png)

- Two-sided message exchange between processes. Server muss response auch quen
- Kpnnen wie server elemienieren und direkt auf speicher schreiben?

![grafik.png](attachment:9f392cda-6446-40f0-a3ce-a58487f0f0df:grafik.png)

![grafik.png](attachment:f532801d-6581-4d46-801c-979281713a94:grafik.png)

- Aber was wenn mehrere clients auf selbe speicher schreiben?

### RDMA Challenge

![grafik.png](attachment:86b84af4-5dca-405c-9092-8d1ad9e2edbd:grafik.png)

### Architectural View

- RDNA kopiert daten nur in NIC und nicht wie bei socket base die daten als copy in client side

![grafik.png](attachment:9e7dac7d-b018-420d-91cd-63d3c896e792:grafik.png)

![grafik.png](attachment:ba6b61e4-7abd-491d-be1a-20b6515bd725:grafik.png)

![grafik.png](attachment:373082c7-4748-4d4d-b022-aff77209385f:grafik.png)

![grafik.png](attachment:09dec50b-0b74-43dd-b389-f9ff22db6f9c:grafik.png)

![grafik.png](attachment:629dcccc-2557-454b-b2ba-9768e49ebdb3:grafik.png)

![grafik.png](attachment:210e56cc-26b3-4f07-8427-9c4642a85386:grafik.png)

### **Network Performance Metrics**

- **Bandwidth**: Maximale Datenrate (Gbps, MB/s)
- **Latency**: Round-Trip Time (RTT), One-Way Delay
- **Throughput**: Tatsächlich erreichte Datenrate
- **Packet Loss**: Verlorene Pakete (%), wichtig für TCP Performance
- **Jitter**: Varianz in Latency, kritisch für Real-Time Applications

### **Network Stack Optimizations**

- **TCP Tuning**: Window Size, Congestion Control (Cubic, BBR), Nagle's Algorithm
- **Zero-Copy**: Daten direkt von NIC zu Application Memory (DMA)
- **Kernel Bypass**: DPDK, RDMA - Umgeht Kernel Network Stack
- **Offloading**: TCP/UDP Checksum, Segmentation (TSO/GSO) in NIC Hardware
- **Interrupt Coalescing**: Mehrere Packets pro Interrupt verarbeiten

### **High-Performance Networking**

- **DPDK (Data Plane Development Kit)**: User-Space Packet Processing, Poll Mode Drivers
- **RDMA (Remote Direct Memory Access)**: Direkter Memory-Zugriff ohne CPU, ultra-low Latency
- **SR-IOV**: Single-Root I/O Virtualization, direkte NIC Access für VMs
- **XDP (eXpress Data Path)**: Kernel-integriertes Fast Path Packet Processing
- **SmartNICs**: Programmierbare NICs mit FPGAs/ASICs für Packet Processing

### **Network Topologies**

- **Star**: Alle Nodes verbunden zu zentralem Switch
- **Tree/Fat-Tree**: Hierarchisch, verwendet in Datacenters
- **Mesh**: Jeder Node verbunden mit jedem (hohe Redundanz)
- **Torus**: Mesh mit wrap-around Links (HPC Interconnects)
- **Dragonfly**: Hierarchisch gruppiert, niedrige Diameter (Google, Supercomputers)

### **Datacenter Networking**

- **East-West Traffic**: Server-to-Server innerhalb Datacenter (dominant in modernen DCs)
- **North-South Traffic**: Client-to-Server (extern)
- **Spine-Leaf Architecture**: Jeder Leaf Switch verbunden zu jedem Spine Switch
- **Load Balancing**: Traffic-Verteilung über mehrere Server/Paths (ECMP, Maglev)
- **Network Virtualization**: Overlay Networks (VXLAN, Geneve), Software-Defined Networking (SDN)

### **Network Measurement Tools**

- **ping**: ICMP Echo Request/Reply für Latency-Messung
- **iperf3**: Bandwidth und Throughput Testing
- **netperf**: Network Performance Benchmarking (verschiedene Patterns)
- **tcpdump/Wireshark**: Packet Capture und Analysis
- **ss/netstat**: Socket Statistics, Connection Tracking
- **ethtool**: NIC Configuration und Statistics

### **Summary**

- **Networking**: Kritischer Bottleneck in verteilten Systemen
- **Performance**: Bandwidth, Latency, Throughput, Packet Loss
- **Optimizations**: TCP Tuning, Zero-Copy, Kernel Bypass (DPDK/RDMA)
- **Datacenter**: Spine-Leaf Topology, East-West Traffic dominiert
- **High-Perf**: RDMA für ultra-low Latency, SmartNICs für Offload
- **Tools**: iperf3, ping, tcpdump, ethtool für Messung und Debugging

## Vorlesung 10: Cloud (gesehen)

[Lecture_10_Cloud_Intro.pdf](attachment:1f102b44-fbd2-4ecb-8c88-7df2306343ab:Lecture_10_Cloud_Intro.pdf)

- RoCEv2 → RDMA over ROUTABLE UDP/Ethernet packets

CapEx vs. OpEx

- CapitalExpense investment in Server infrastruktur
- Operational Expense op kosten lol

### **Cloud Computing - Grundlagen**

- **Definition**: On-Demand Zugriff auf Computing Resources über das Internet
- **Service Models**: IaaS (Infrastructure), PaaS (Platform), SaaS (Software)
- **Deployment Models**: Public Cloud, Private Cloud, Hybrid Cloud, Multi-Cloud
- **Key Characteristics**: On-Demand Self-Service, Broad Network Access, Resource Pooling, Rapid Elasticity, Measured Service

### **Cloud Providers**

- **AWS (Amazon Web Services)**: Marktführer, umfangreichstes Service-Portfolio
- **Microsoft Azure**: Stark bei Enterprise & Hybrid Cloud
- **Google Cloud Platform (GCP)**: Fokus auf ML/AI und Analytics
- **Alibaba Cloud**: Dominant in Asien

### **Virtualization**

- **Hypervisors**: Type 1 (Bare-Metal: VMware ESXi, Xen, KVM) vs. Type 2 (Hosted: VirtualBox, VMware Workstation)
- **VMs**: Vollständige OS-Isolation, höherer Overhead
- **Containers**: Shared Kernel, leichtgewichtiger (Docker, Kubernetes)
- **Hardware Virtualization**: Intel VT-x, AMD-V für CPU; SR-IOV für I/O

### **Cloud Storage**

- **Object Storage**: S3, Azure Blob - für unstrukturierte Daten, REST API
- **Block Storage**: EBS, Azure Disk - für VMs, niedrige Latency
- **File Storage**: EFS, Azure Files - shared filesystems (NFS/SMB)
- **Durability**: 11 9's (99.999999999%) durch Replikation über Availability Zones

### **Cloud Networking**

- **Virtual Private Cloud (VPC)**: Isolierte Netzwerke in der Cloud
- **Subnets**: Public (Internet-facing) vs. Private (internal)
- **Load Balancers**: Application LB (Layer 7), Network LB (Layer 4)
- **Content Delivery Networks (CDN)**: CloudFront, Azure CDN - Edge Caching
- **VPN/Direct Connect**: Sichere Verbindung On-Premise ↔ Cloud

### **Scalability & Elasticity**

- **Vertical Scaling**: Größere VM (mehr CPU/RAM) - limitiert, Downtime
- **Horizontal Scaling**: Mehr Instanzen - unbegrenzt, komplexere Architektur
- **Auto-Scaling**: Automatische Skalierung basierend auf Metriken (CPU, Requests)
- **Elasticity**: Schnelles Scale-Up/Down bei Lastspitzen

### **Cloud Pricing Models**

- **On-Demand**: Pay-per-Use, keine Commitments, teuerste Option
- **Reserved Instances**: 1-3 Jahre Commitment, 30-70% günstiger
- **Spot Instances**: Bid auf ungenutzte Kapazität, bis 90% günstiger, können unterbrochen werden
- **Savings Plans**: Flexible Commitments über Instanz-Familien hinweg

### **Cloud Performance Optimization**

- **Instance Types**: General Purpose, Compute Optimized, Memory Optimized, Storage Optimized, GPU
- **Placement Groups**: Cluster (niedrige Latency), Spread (Redundanz), Partition (große verteilte Workloads)
- **Caching**: ElastiCache (Redis/Memcached), CloudFront (CDN)
- **Database Optimization**: Read Replicas, Sharding, Managed Services (RDS, DynamoDB)

### **Serverless Computing**

- **Functions-as-a-Service (FaaS)**: AWS Lambda, Azure Functions, Google Cloud Functions
- **Event-Driven**: Code läuft nur bei Events (HTTP Request, File Upload, etc.)
- **Auto-Scaling**: Automatisch von 0 bis zu tausenden parallelen Invocations
- **Pricing**: Pay-per-Invocation und Execution Time
- **Cold Start Problem**: Initiale Latency beim ersten Request

### **Cloud Security**

- **Shared Responsibility Model**: Provider sichert Infrastruktur, Kunde sichert Daten/Applikationen
- **Identity & Access Management (IAM)**: Fine-grained Permissions, Least Privilege Principle
- **Encryption**: At Rest (EBS, S3) und In Transit (TLS/SSL)
- **Network Security**: Security Groups (Stateful Firewall), Network ACLs
- **Compliance**: ISO 27001, SOC 2, GDPR, HIPAA

### **Summary**

- **Cloud**: On-Demand Computing Resources, Pay-as-You-Go Modell
- **Service Models**: IaaS (VMs), PaaS (Managed Platforms), SaaS (Applications)
- **Virtualization**: VMs (Hypervisors) vs. Containers (Docker/K8s)
- **Storage**: Object (S3), Block (EBS), File (EFS)
- **Scalability**: Horizontal (mehr Instanzen) besser als Vertical (größere VMs)
- **Pricing**: On-Demand, Reserved, Spot Instances
- **Serverless**: FaaS (Lambda) für event-driven Workloads
- **Security**: Shared Responsibility, IAM, Encryption, Network Security

## Vorlesung 11: Virtualisierung (gesehen) - Bis hier fur Quiz

Hier ist eine **kompakte, strukturierte Zusammenfassung der PDF „Lecture 11: Virtualization“**:

---

## Überblick

Die Vorlesung erklärt die Grundlagen der **Virtualisierung** in modernen Cloud- und Datensystemen. Behandelt werden **Virtuelle Maschinen (VMs)**, **Container** und **WebAssembly (Wasm)** sowie deren technische Umsetzung, Vorteile, Nachteile und Performance-Eigenschaften.

---

## 1. Virtualisierung – Grundlagen

- Virtualisierung schafft eine **virtuelle Darstellung physischer Ressourcen** (CPU, Speicher, I/O).
- Ziel: **Ressourcenteilung**, **Isolation** (Sicherheit) und **Flexibilität**.
- Wichtig für Cloud Computing: Serverkonsolidierung, Lastverteilung, Migration, Checkpoints.

---

## 2. Virtuelle Maschinen (VMs)

### Konzepte

- **Host**: Physische Hardware
- **Guest**: Virtuelles System (OS + Anwendungen)
- **VMM/Hypervisor**: Vermittelt zwischen Hardware und Gästen
- Starke Isolation, vollständiges Betriebssystem pro VM.

### Virtualisierungsansätze

1. **Interpretation**
    - Sehr sicher, aber extrem langsam.
2. **Trap-and-Emulate**
    - Direktes Ausführen, privilegierte Instruktionen lösen Traps aus.
3. **Binäre Übersetzung**
    - Nicht-virtualisierbare Instruktionen werden dynamisch umgeschrieben.
4. **Paravirtualisierung**
    - Gast-OS wird angepasst (z. B. Xen), bessere Performance, aber aufwendig.
5. **Hardware-unterstützte Virtualisierung (heute Standard)**
    - Intel VT-x / AMD-V
    - Gast-OS läuft direkt auf der CPU, VM-Exits nur bei Bedarf.

---

## 3. Speicher- und I/O-Virtualisierung

### Speicher

- Problem: Gast-OS erwartet eigenen physischen Speicher.
- Lösung früher: **Shadow Page Tables** (hoher Overhead).
- Moderne Lösung: **Extended Page Tables (EPT)**
    - Hardware übernimmt Übersetzung
    - Weniger VM-Exits, bessere Performance.

### I/O

- Gerätevirtualisierung ist komplex.
- Ansätze:
    - Geräteemulation
    - Paravirtualisierte Treiber
    - **SR-IOV**: Ein physisches Gerät erscheint als mehrere virtuelle Geräte.

---

## 4. Performance-Auswirkungen von VMs

- Mehr Kontextwechsel
- Höherer Druck auf TLB und Speicherhierarchie
- Längere I/O-Pfade
- Geteilte Ressourcen → mögliche Konkurrenz zwischen VMs.

---

## 5. Container

### Grundidee

- **Leichtgewichtige OS-Level-Virtualisierung**
- Container teilen sich den **Kernel des Host-OS**
- Kein Hypervisor notwendig.

### Vorteile gegenüber VMs

- Sehr schneller Start
- Geringer Speicherbedarf
- Nahezu native Performance

### Nachteile

- Schwächere Isolation
- Alle Container sind vom selben Kernel abhängig.

### Docker & Linux Containers

- Linux-Features: **Namespaces** (Isolation), **cgroups** (Ressourcenlimits)
- Docker ergänzt:
    - Images & Layer
    - Dockerfile
    - Registry & Tooling

---

## 6. WebAssembly (Wasm)

- Portables, sicheres Binärformat
- Ursprünglich für Browser, heute auch Cloud & Edge
- Eigenschaften:
    - Starke Isolation
    - Sehr kleine Binaries
    - Schneller Start
    - Keine direkten Systemaufrufe
- Sehr gut geeignet für **Serverless** und **Sandboxing**.

---

## 7. Vergleich der Virtualisierungstechniken

|Eigenschaft|VM|Container|WebAssembly|
|---|---|---|---|
|Isolation|Stark|Mittel|Stark|
|Performance|Langsamer|Schnell|Nahezu nativ|
|Startzeit|Sekunden–Minuten|ms–Sekunden|ms|
|Speicherbedarf|Hoch (GB)|Mittel (MB)|Sehr gering (KB)|
|Flexibilität|Sehr hoch|Hoch|Eingeschränkt|

---

### Kurzfazit

- **VMs**: Maximale Isolation, hoher Overhead
- **Container**: Beste Balance aus Performance & Flexibilität
- **WebAssembly**: Extrem leichtgewichtig und sicher, aber eingeschränkt

Wenn du möchtest, kann ich dir auch:

- eine **Lernzettel-Version**,
- eine **1-Seiten-Zusammenfassung**, oder
- einen **Vergleich speziell für Klausurvorbereitung** erstellen.

## 📑 Exercise Session #1: Experiments & Profiling

**1. gdb - Debugger**

- Compile: `g++ main.cpp -o main && ./main`
- Start gdb: `gdb ./main`
- Run: `run`
- Backtrace: `backtrace` (zeigt wo Crash)
- Breakpoints setzen: `break main` oder `break main.cpp:42`
- Navigation: `next` (step over), `step` (step into), `continue`
- Variablen inspizieren: `print variable`

**2. Valgrind - Memory Leak Detection**

```bash
valgrind --leak-check=full ./main
```

- Zeigt Memory Leaks und ungültige Speicherzugriffe

**3. Manpages**

- `man <command>` (z.B. `man gdb`)
- Suchen: `/pattern`, nächster Treffer: `n`
- Spezifische Sektion: `man 3 printf` (C library function)
- Exit: `q`

**4. Compiler Flags**

- **Optimization Levels**:
    - `-O0`: Keine Optimierung (default)
    - `-O1, -O2, -O3`: Steigende Optimierung
    - `-Ofast`: Aggressive Optimierung (kann Standards brechen)
    - `-Os`: Für Size optimieren
    - `-g`: Debug-Info hinzufügen
- **Vectorization**:
    - `-march=native`: SIMD aktivieren
    - `-ftree-vectorize`, `-funroll-loops`: Zusätzliche Optimierungen
- **Assembly ansehen**:
    - `-save-temps`: Assembly als Zwischenschritt behalten
    - `-S -o code.s`: Nur Assembly generieren
    - `-fverbose-asm`: Lesbares Assembly (kann Binary größer machen)
- Godbolt: [https://godbolt.org/z/TvaEeGene](https://godbolt.org/z/TvaEeGene)

**5. Performance Counters (PMUs)**

- Hardware-Counter für CPU-Events (Cache Misses, Branch Mispredictions, etc.)
- Sampling-based Profiling

**6. perf & perfEvent**

- **perf**: Linux Performance Profiling Tool
- **perfEvent**: C++ Header-Only Library ([https://github.com/viktorleis/perfevent](https://github.com/viktorleis/perfevent))
    - Einfaches Drop-in für Projekte
    - Bereits in FOMO-Projekten enthalten

## 📄 Exercise Session #2: Profiling & Memory Hierarchy

**⚠️ PSA**: SSH-Key-Formular in Moodle schließt am Tag der Anmeldefrist!

**Performance Monitoring Units (PMUs)**

- **Zweck**: Hardware-Counter in modernen CPUs für Performance-Events
- **Events**: L1/dTLB hits/misses, Branch Predictions, Instructions, Cycles, etc.
- Hunderte bis tausende Events verfügbar (je nach CPU-Vendor/Modell)
- Können **mehrere Events gleichzeitig tracken**
- **Profiling Statistics**: `perf stat ./my-app`
    - Liest Counter am Anfang und Ende der Ausführung
    - Zeigt: Cycles, Instructions, IPC (Instructions per Cycle), Branch Misses, Cache Misses
- **Profiling Sampling**: Periodisches Sampling des Execution State
    - **Period**: _Wann_ samplen (z.B. alle 4.000 Cycles oder Memory Loads)
    - **Sample**: _Was_ speichern (Instruction Pointer, Memory Address, ...)
    - Kombiniert mit Binary & Debug Symbols → zeigt Hotspots im Code

**Abstractions - perf subsystem**

- PMUs sind **implementation-dependent** (Intel PEBS, AMD IBS, ARM SPE)
- **perf subsystem** (Linux) vereinheitlicht Konfiguration und Zugriff
- **Darüber**: Linux Perf, PAPI, PerfEvent, perfmon2, perf-cpp

**In-Application Profiling**

- Statt externe Tools: PMUs direkt im Code nutzen
- **Workload Setup** → Counter lesen → **Workload ausführen** → Counter erneut lesen → Teardown
- Bibliotheken: PAPI, PerfEvent, perfmon2, perf-cpp

**PerfEvent**

- [https://github.com/viktorleis/perfevent](https://github.com/viktorleis/perfevent)
- Single Header File (.hpp), keine komplizierten Dependencies
- Drop-in für einfache Projekte
- **Wird in FOMO/ADMS-Projekten bereitgestellt**

**Likwid**

- [24](24)
- Vom BMBF gefördert
- Heavy-duty "All-in-One": Energy Consumption, NUMA Topology, etc.
- Sogar Fortran-Support!

**perf-cpp**

- [25](25)
- Projekt von TU Dortmund
- Unterstützt **Triggers**: Conditions die PMU-Capture auslösen
- Mächtig für gezieltes Profiling

**Perf Overhead**

- Likwid: 5-10% Overhead (bei Matrix-Größe >768×768)
- Overhead = Runtime(without perf) / Runtime(with perf)

**Memory Hierarchy - Practical View**

- **Storage Hierarchy**:
    - **Registers**: 16×8B, 1 cycle
    - **L1 Cache**: 32KB (I+D getrennt), ~4 cycles
    - **L2 Cache**: 256KB, ~10 cycles
    - **L3/LLC**: 10s MB, ~30-60 cycles
    - **DRAM**: 16-64GB, ~100-200 cycles / 60ns
    - **Persistent Storage** (SSD/HDD): 1-2TB, μs-ms
    - **Archival Storage** (Tape): >TB, ~100s

**Warum ist das wichtig?**

- Zwei O(1)-Datenstrukturen haben **nicht** dieselbe Performance
- **Random Access** ≠ **Sequential Access**
- **Access Latency** trifft manche Datenstrukturen härter
- **Trade-off**: Space gegen Latency/Bandwidth
- **Caching-Effekte** durch Reuse maximieren
- **Prefetching** durch Locality ausnutzen

**Array vs. Vector**

- **Array**: Statisch pre-allokiert, aligned, garantiert Sequential Access
- **Vector** (std::vector): Dynamisch wachsend, keine Alignment-Garantie, potenzielle Fragmentierung
- **Ohne reserve()**: push_back() triggert Reallocations → teuer
- **Mit reserve()**: Memory upfront allokiert → keine Reallocations → schneller, weniger Fragmentierung

**Cache Behavior - Access Patterns**

- **Sequential Access**: Daten im Cache + Prefetching → schnell
- **Random Access**: Jeder Zugriff = Cache Miss → langsam
- **Messen**: `perf stat -e cache-misses ./main`

**Data Structure Properties**

- **5 Core Metrics**:
    1. Insert Time
    2. Update Time
    3. Delete Time
    4. Access Time
    5. Space ← **Severe implications on 1-4** durch Memory Hierarchy
- Für 1-4: Sequential vs. Random? Worst/Average/Best Case?

**🎯 Project 1 - Benchmarking & Memory Hierarchy**

- **Startet heute! (23.10.25)**
- **Deadline**: 20.11.2025
- **Punkte**: 15P (von 50P gesamt)
- **Learning Objectives**:
    - Hardware Memory Performance genau messen und analysieren
    - Performance verschiedener Datenstrukturen vergleichen
    - Benchmarking-Ergebnisse klar kommunizieren (visuell + schriftlich)
    - Erklären wie Memory Hierarchy DS-Performance beeinflusst

**Project Tasks**

1. **(3P) Memory System evaluieren**: Bandwidth + Latency
2. **(6P) 4 Datenstrukturen evaluieren**: Bandwidth + Latency
    - DirectAccessArray
    - BinarySearchArray
    - ChainedHashTable(bin_size=1)
    - ChainedHashTable(bin_size=16)
3. **(6P) Report**: Erklärung der Benchmarking-Setup + Ergebnisse interpretieren

**Die Datenstruktur: 64B Node**

```cpp
struct alignas(64) Node {
    uint64_t key;
    uint64_t data;
    Node *next;
    char padding[64 - 16 - sizeof(Node *)];
};
```

- 64-Byte-aligned → jedes Lookup = 1 Cache Line Read
- Macht Lookups _sehr_ memory-intensiv

**Contestants**

- **DirectAccessArray**: Dense Datasets, pre-initialized, sequential keys
- **BinarySearchArray**: Sparse Datasets, pre-initialized, sequential keys
- **ChainedHashTable**: Dynamic Size, universal, verschiedene Bin Sizes, auch random keys möglich

**Metriken**

- **Lookup Bandwidth**: Avg. Bytes/Second
- **Lookup Latency**: Avg. Cycles/Lookup

**Restrictions**

- Alle DS haben N Nodes in **ascending key order** (auch Hash!)
- Key darf **nicht öfter als 1× pro N Lookups** gesucht werden
- Alle Keys am Ende **gleich oft** gesucht

**Chained Hash Table - Bin Size**

- **bin_size=1**: Ist das noch eine Hash Table? Wie vergleicht sie sich mit Array?
- **bin_size=16**: Wie vergleicht sie sich mit bin_size=1?

**Final Output**

- Rückgabe: `{bw_1, bw_2, bw_3, bw_4, lat_1, lat_2, lat_3, lat_4}`

**Tests**

- 2 Basic Tests (je 0.5P)
- 8 Advanced Tests (je 1P)

**Report (1-2 Seiten, Font Size 11)**

- **(1P)** Explanation des Benchmarking Setups
- **(1P)** Plot: Bandwidth über Access Patterns + Dataset Sizes
- **(1P)** Plot: Latency über Access Patterns + Dataset Sizes
- **(1P)** Compare: DirectAccessArray vs. ChainedHashTable(bin_size=1)
- **(1P)** Compare: BinarySearch Random vs. Sequential Access
- **(1P)** Compare: ChainedHashTable(bin_size=1) vs. (bin_size=16)

**Wichtig**

- **FORK das Projekt** in deinen Namespace
- Report als PDF im Fork ablegen
- Details siehe Moodle Project Description

## 📄 Exercise Session #3: DDR & Memory Access Patterns

**DDR Memory - 3 wichtige Effekte**

- **Bursting**: Upfront Cost beim Zugriff auf DRAM
    - RAS (Row Address Strobe) + CAS (Column Address Strobe) müssen gesetzt werden
    - RCD (RAS to CAS Delay) + CL (CAS Latency) bevor Daten verfügbar
    - Danach: Burst von mehreren Data Outs möglich
- **Row Changes**: Bank-Wechsel hat Kosten
    - Rows müssen "aktiviert" werden (Precharge + Activation)
    - RP (Row Precharge Time) + RCD Delay
    - Swapping zwischen Rows führt zu Performance-Einbußen
- **Recharging**: DRAM-Zellen müssen konstant refreshed werden
    - Refresh stalled eine Memory Row für einige Clock Cycles
    - Access während Refresh → zusätzliche Wartezeit

**TLBs (Translation Lookaside Buffers)**

- **Zweck**: Cache für Virtual → Physical Address Translation
- **Problem**: Begrenzte TLB-Cache-Größe
    - Typisch: 1 Page (4KB) = 1 TLB Entry
    - Wenn Daten über viele Pages verstreut → TLB Thrashing → Performance-Einbruch
- **Lösung**: Memory Access Pattern optimieren
    - Data Locality erhöhen
    - Huge Pages nutzen (weniger TLB Entries nötig)
- **Motivation**: Radix Join Algorithmus (aus ADMS) wurde u.a. entwickelt um TLB Overheads zu minimieren

**Prefetching**

- **Wichtig**: Prefetcher arbeitet typisch nur **innerhalb einer Page Boundary**
    - Performance + Security Gründe
- **Page Granularity** = kritischste Optimierungsebene (nach Cache Line)
- **Pseudo Random Access**: Viel näher an Sequential als an Random
    - Random Pages, aber Sequential Access innerhalb der Page
- **Stride**: Prefetcher funktioniert auch mit Stride ≠ 1 (z.B. +10)
    - Aber: Es gibt Limits für Stride-Größe

**Row-Major vs. Column-Major**

- **Alles spielt eine Rolle**:
    - TLB Misses vermeiden
    - Prefetcher mit einfachem Pattern füttern
    - Cache Lines voll ausnutzen
- **Zusätzlich**: Constant-size Arrays vs. Dynamic Arrays
    - Constant-size: Compiler kann besser optimieren
    - Dynamic: Pointer Dereferencing → schlechter für Prefetcher

**Blocking (Tiling)**

- **Ziel**: Schlüsseltechnik aus Linear Algebra
- **Idee 1**: Column-major Inner Loop → Row-major umwandeln durch zusätzlichen Outer Loop
- **Idee 2**: Cache-Utilization erhöhen
    - Kleine Tiles von A, B, C im Cache halten
    - Bessere Reuse von Cache Lines

**Beispiel: Blocked Matrix Multiplication**

- **Naïve Version**: Triple-Loop (i, k, j)
    - Inner Loop j: Row-major für C und B
    - Problem: Keine Garantie dass alle Daten im Cache bleiben
- **Blocked Version**: 6 Loops (i0, k0, j0, i, k, j)
    - Outer Loops: Iterieren über Blocks (Tile-Größe = Bsize)
    - Inner Loops: Innerhalb der Tiles arbeiten
    - **Vorteil**: Kleine Tiles bleiben im Cache → bessere Reuse
    - Comment: "blocking keeps small tiles of A,B,C in cache → better reuse of cache lines"

**Exkurs: Strassen Matrix Multiplication**

- **Was ist es?**: Alternativer Algorithmus zur Matrix-Multiplikation
    - Statt Triple-Loop: Serie von spezifischen Operationen (unique pro Matrix-Größe)
    - O(n^2.80735) statt O(n³)
- **AI-Connection**: Kürzlich durch AI "rediscovered" für verschiedene Matrix-Größen
- **⚠️ Cautionary Tale - Theory vs. Practice**:
    - Verringert asymptotische Komplexität
    - **Aber**: Zerstört Memory Access Pattern komplett
    - → Alle Gewinne durch Cache Misses verloren!
    - Würde nur gut funktionieren wenn Random Access = Sequential Access

**Diskussion & Q&A**

- Diskussion über eigene Datenstrukturen im Projekt

## 📝 Exercise Session #4: Tiled/Blocked Matrix Multiplication (06.11.25)

**Reminders**

- **Exam Registration Deadline**: 10.11.2025 (Montag) – letzter Tag!
- Late Registrations nur mit gutem Grund über Studienbüro
- Bei Quiz-Abwesenheit: Tim Neubacher kontaktieren (mit Nachweis)
- **Kontakt**: [fomo@lists.systems.informatik.tu-darmstadt.de](mailto:fomo@lists.systems.informatik.tu-darmstadt.de) nutzen (nicht persönliche Emails!)

**Practical Notes - Pipelining**

- **Pipelining**: Analogous zu Prefetching – CPU muss wissen was als nächstes kommt
- **Branches sind der Feind**: Wie Random Access statt Sequential
- **Predication**: Sehr mächtig – vermeidet Branches → CPU weiß was ahead ist
- **Speculative Execution**: CPUs "Antwort", aber nicht gratis & sehr limitiert

**Practical Notes - Out of Order Execution**

- **Extremely Powerful**: Löst viele Probleme (teilweise)
- **Warum Random Access nicht "so schlimm" ist**: OoO kann andere Dinge tun während es auf Daten wartet
- **OoO-friendly Code schreiben**: Dependencies innerhalb von Funktionen minimieren → gibt Hyper-Threads mehr "Options"

**Making Code OoO-Friendly - Parallel Accumulators**

- **Sequential Approach**: `sum += a\\[i\\] \\* b\\[i\\]` – jede Operation abhängig von vorheriger
- **Parallel Accumulators**: Mehrere unabhängige Akkumulatoren (s0, s1, s2, s3)
    - `s0 += a\\[i+0\\] \\* b\\[i+0\\]; s1 += a\\[i+1\\] \\* b\\[i+1\\]; ...`
    - Loop increment: `i += 4` (annehmen n % 4 = 0)
    - Final: `return s0 + s1 + s2 + s3`
- **Teaser für nächste Woche**: Vectorization/SIMD

**The Other Side of the Coin**

- **CPU Features sind nicht gratis**: Pipelining, Prefetching, OoO, Transparent Caches, Speculation
- **Moderne CPUs sind extrem komplex** – schadet Performance-Potential:
    - Alle Daten müssen durch Caches (auch wenn nicht benötigt)
    - Instructions speichern (bis zu 50% von L1!)
    - Instruction Handling sehr teuer
    - Cores kommunizieren über höhere Cache-Levels
    - Schwer zu verstehen warum CPU etwas nicht tut
    - Schwer zu skalieren (#Cores, SIMD width, #Pages)
- **Accelerators** (GPUs, TPUs, FPGAs, CGRAs): Geben diese Features auf für max. Performance & Skalierbarkeit
    - → Du musst sie dann auf Application-Level selbst implementieren
- **Trade-off**: Generality ↔ Specialization

**Tiled/Blocked Matrix Multiplication**

- **Key Idea**: Main Memory Accesses minimieren durch Segmentierung in Blocks und Caching
- **Ergebnis ändert sich nicht**, Operations ändern sich nicht – **nur die Reihenfolge**
- **Block-Größe b×b**: Reduziert Main Memory Accesses um Faktor b
- **Größerer Block** = effizientere MMULT – **Limit**: Cache Size!
- **Applies across Memory Hierarchy**: Kann rekursiv angewendet werden
- **Incredibly Important**: In praktisch allen Linear Algebra Workloads (und vielen anderen) genutzt
- **Illustrative GIF**: [https://penny-xu.github.io/tmm-59dd890f48435e692c47919d0df4a5e6.gif](https://penny-xu.github.io/tmm-59dd890f48435e692c47919d0df4a5e6.gif)

**Tips für Project 1**

- **pthread mit Stop Token** ist effizienter als `chrono::now()`
    - Atomic Operation (Flag checken) vs. ständig OS nach Zeit fragen
    - "Wake me up when we've arrived" vs. "Are we there yet? Are we there yet?..."
- **16 KB Array**: 256-long Loop mit 64B Node
    - Memory Fetch = tens to hundreds of cycles
    - Warm-up Effects, Testing Time, Thread Spin-up – **alles wird wichtig sein**

**Tips für Project 1**

- **pthread mit Stop Token** ist effizienter als `chrono::now()`
    - Atomic Operation (Flag checken) vs. ständig OS nach Zeit fragen
    - "Wake me up when we've arrived" vs. "Are we there yet? Are we there yet?..."
- **16 KB Array**: 256-long Loop mit 64B Node
    - Memory Fetch = tens to hundreds of cycles
    - Warm-up Effects, Testing Time, Thread Spin-up – **alles wird wichtig sein**

## 📝 Exercise Session #4: Tiled Matrix Multiplication & Project Tips (06.11.25)

**Reminders**

- **⚠️ Exam Registration Deadline**: 10.11.2025 (Montag) – letzter Tag!
- Late Registrations nur mit gutem Grund über Studienbüro
- Bei Quiz-Abwesenheit: Tim Neubacher kontaktieren (mit gutem Grund + Nachweis)
- **Kontakt**: [fomo@lists.systems.informatik.tu-darmstadt.de](mailto:fomo@lists.systems.informatik.tu-darmstadt.de) nutzen (keine persönlichen Emails!)

**Practical Notes - Pipelining**

- **Pipelining**: Analog zu Prefetching – CPU muss wissen was als nächstes kommt
- **Branches = der Feind**: Ähnlich wie Random Access statt Sequential
    - CPU Pipeline Flush bei Misprediction
- **Predication**: Sehr mächtig – vermeidet Branches → CPU weiß was kommt
- **Speculative Execution**: CPUs "Antwort", aber nicht gratis & sehr limitiert

**Practical Notes - Out of Order Execution**

- **Extremely Powerful**: Löst viele Probleme (teilweise)
- **Warum Random Access nicht "so schlimm" ist**: OoO kann andere Dinge tun während es auf Daten wartet
- **OoO-friendly Code schreiben**: Dependencies innerhalb von Funktionen minimieren
    - Gibt Hyper-Threads mehr "Options" was sie parallel ausführen können

**Making Code OoO-Friendly - Parallel Accumulators**

- **Sequential Approach** (schlecht für OoO):
    
    ```cpp
    double sum = 0.0;
    for (size_t i = 0; i < n; ++i) {
        sum += a[i] * b[i];  // jede Operation abhängig von vorheriger
    }
    return sum;
    ```
    
- **Parallel Accumulators** (gut für OoO):
    
    ```cpp
    double s0 = 0.0, s1 = 0.0, s2 = 0.0, s3 = 0.0;
    // assume n % 4 = 0 this week :)
    for (size_t i = 0; i < n; i += 4) {
        s0 += a[i + 0] * b[i + 0];  // unabhängig
        s1 += a[i + 1] * b[i + 1];  // unabhängig
        s2 += a[i + 2] * b[i + 2];  // unabhängig
        s3 += a[i + 3] * b[i + 3];  // unabhängig
    }
    return s0 + s1 + s2 + s3;
    ```
    
- **Vorteil**: 4 unabhängige Akkumulatoren → CPU kann alle parallel berechnen
    
- **Teaser für nächste Woche**: Vectorization/SIMD
    

**The Other Side of the Coin**

- **CPU Features sind nicht gratis**: Pipelining, Prefetching, OoO, Transparent Caches, Speculation
- **Moderne CPUs sind extrem komplex** – schadet Performance-Potential:
    - Alle Daten müssen durch Caches (auch wenn nicht benötigt)
    - Instructions speichern (bis zu 50% von L1!)
    - Instruction Handling sehr teuer
    - Cores kommunizieren über höhere Cache-Levels
    - Schwer zu verstehen warum CPU etwas nicht tut
    - Schwer zu skalieren (#Cores, SIMD width, #Pages)
- **Accelerators** (GPUs, TPUs, FPGAs, CGRAs): Geben diese Features auf für max. Performance & Skalierbarkeit
    - → Du musst sie dann auf Application-Level selbst implementieren
- **Trade-off**: **Generality ↔ Specialization**

**Tiled/Blocked Matrix Multiplication**

- **Key Idea**: Main Memory Accesses minimieren durch Segmentierung in Blocks und Caching
- **Was ändert sich?**
    - Ergebnis: **Gleich** ✓
    - Operations: **Gleich** ✓
    - Reihenfolge: **Anders** ← Das ist der Trick!
- **Block-Größe b×b**: Reduziert Main Memory Accesses um **Faktor b**
- **Größerer Block** = effizientere MMULT
    - **Limit**: Cache Size! (Block muss in Cache passen)
- **Applies across Memory Hierarchy**: Kann rekursiv angewendet werden
    - L1-optimierte Tiles → L2-optimierte Tiles → L3-optimierte Tiles
- **Incredibly Important**: In praktisch allen Linear Algebra Workloads (und vielen anderen) genutzt
- **Illustrative GIF**: [Tiled Matrix Multiplication Visualization](https://penny-xu.github.io/tmm-59dd890f48435e692c47919d0df4a5e6.gif)

**Naïve Matrix Multiplication**

```cpp
// C = A × B
for (int i = 0; i < n; i++) {
    for (int k = 0; k < n; k++) {
        for (int j = 0; j < n; j++) {
            C[i][j] += A[i][k] * B[k][j];
        }
    }
}
```

- **Problem**: Keine Garantie dass A, B, C im Cache bleiben
- Bei großen Matrizen: Viele Cache Misses → langsam

**Tiled Matrix Multiplication**

```cpp
// Outer loops: iterate over blocks
for (int i0 = 0; i0 < n; i0 += BLOCK_SIZE) {
    for (int k0 = 0; k0 < n; k0 += BLOCK_SIZE) {
        for (int j0 = 0; j0 < n; j0 += BLOCK_SIZE) {
            // Inner loops: work within block
            for (int i = i0; i < i0 + BLOCK_SIZE; i++) {
                for (int k = k0; k < k0 + BLOCK_SIZE; k++) {
                    for (int j = j0; j < j0 + BLOCK_SIZE; j++) {
                        C[i][j] += A[i][k] * B[k][j];
                    }
                }
            }
        }
    }
}
```

- **Vorteil**: Kleine Tiles von A, B, C bleiben im Cache → bessere Reuse
- **Beispiel**: (8×8) Matrix mit Block Size 4
    - Naïv: Jedes Element mehrfach aus Memory laden
    - Tiled: Block einmal laden, viele Operationen darauf

**Tips für Project 1**

- **pthread mit Stop Token** ist effizienter als `chrono::now()`
    - **Stop Token**: Atomic Operation (Flag checken) – sehr schnell
    - **chrono::now()**: Ständig OS nach Zeit fragen + vergleichen – langsam
    - **Analogie**:
        - Stop Token: "Wake me up when we've arrived" ✓
        - chrono::now(): "Are we there yet? Are we there yet? Are we there yet?..." ✗
- **16 KB Array**: 256-long Loop mit 64B Node
    - Memory Fetch = tens to hundreds of cycles
    - **Alles wird wichtig sein**:
        - Warm-up Effects
        - Testing Time
        - Thread Spin-up
        - Measurement Overhead
    - Bei so kleinen Workloads zählt jeder Cycle!

## 🔧 Exercise Session #5: Performance Measurement & Throughput vs Latency

**Präzises Performance Measurement**

**Problem: Naive Measurement**

```cpp
do {
    for (size_t i = 0; i < N; ++i) {
        c[i] = a[i] + b[i];
    }
    ++repeats;
    t1 = seconds();  // ← Teuer!
} while (t1 - t0 < 1.0);
```

- **Problem**: `seconds()` ist ein **Syscall-Wrapper** → sehr teuer!
- Bei kleinen Workloads: Du misst hauptsächlich den **Overhead des Messens** statt der eigentlichen Arbeit

**Lösung: Advanced Measurement mit pthreads**

```cpp
std::jthread worker([&](std::stop_token stoken) {
    e.startCounters();
    while (!stoken.stop_requested()) {  // ← Nur atomic read!
        for (size_t i = 0; i < N; ++i)
            c[i] = a[i] + b[i];
        ++repeats;
    }
    e.stopCounters();
});
std::this_thread::sleep_for(std::chrono::seconds(2));
```

- **Vorteil**:
    - **Worker Thread**: Macht die eigentliche Arbeit, checkt nur atomic flag
    - **Main Thread**: Checked Zeit, stoppt Worker nach Threshold
    - `stop_token.stop_requested()` = **atomic load + AND** → viel günstiger als Syscall!
    - Zeit-Check **nicht mehr im kritischen Loop** → präzisere Messung

**Throughput vs. Latency Measurement**

**Aus Project Subtask 1**

**Latency Loop (mit Dependencies)**

```cpp
// Pointer chasing durch Linked List
Node *current = &linked_list[0];
for (size_t i = 0; i < size; i++) {
    current = current->next;  // ← Dependency!
}
doNotOptimizeAway(current);
```

- **Dependencies zwischen Loop-Iterationen** → Out-of-Order Execution **nicht möglich**
- Nächste Iteration muss warten bis vorherige fertig
- → Misst **Latency** (Zeit pro Operation)

**Throughput Loop (ohne Dependencies)**

```cpp
// Array Access ohne Dependencies
volatile uint64_t res{0};
for (size_t i = 0; i < size; i++) {
    res = array[i].data;  // ← Keine Dependency zwischen Iterationen
}
```

- **Keine Dependencies zwischen Loop-Iterationen** → Out-of-Order Execution **möglich**
- CPU kann nächste Iteration starten ohne auf vorherige zu warten
- → Misst **Throughput** (Operationen pro Zeiteinheit)

**Reminder: Out-of-Order (OoO) Execution**

- **Idee**: CPU führt Instructions basierend auf **Data Availability** aus, nicht nach Program Order
    
- **Beispiel**:
    
    ```
    (1) r1 ← r2 / r3
    (2) r4 ← r1 + r5  (abhängig von (1))
    (3) r6 ← r7 * r8  (unabhängig!)
    ```
    
    - → (3) kann **parallel** zu (1)+(2) oder sogar **vor** (1)+(2) ausgeführt werden

**Visualisierung**

```
Latency Measurement:
Loop progress
    ↑
    |  Iter 1  Iter 2  Iter 3  Iter 4
    |    /       /       /       /
    |   /       /       /       /     ← Dependency, must wait
    |  /       /       /       /
    |__________________________________→ Time
       ︸────︷
       Want to measure this
```

```
Throughput Measurement:
Loop progress
    ↑
    |  Iter 1 Iter 2 Iter 3 Iter 4
    |    ╱╱╱╱╱╱╱
    |   ╱╱╱╱╱╱╱    ← No dependency, parallel execution
    |  ╱╱╱╱╱╱╱
    |__________________________________→ Time
       ︸──︷
       Would measure this (if not for OoO parallelism)
```

**Warum ist das wichtig?**

- **Latency**: Zeit die eine einzelne Operation braucht
    - Wichtig für interaktive Anwendungen, Echtzeit-Systeme
    - Beispiel: Pointer Chasing in Linked List, Tree Traversal
- **Throughput**: Wie viele Operationen pro Zeiteinheit
    - Wichtig für Batch-Processing, Data Analytics
    - Beispiel: Array Scans, SIMD Operations
- **In Project 1**: Beide messen um Datenstrukturen vollständig zu charakterisieren!

**Key Takeaway**

- **Dependencies = Latency-bound**
- **No Dependencies = Throughput-bound** (wenn OoO Execution möglich)
- Moderne CPUs sind sehr gut darin, unabhängige Instructions parallel auszuführen
- Aber: Bei Pointer Chasing oder anderen Dependencies → müssen warten

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

**Trade-off:**
- **Mehr Spezialisierung → mehr Effizienz**
- **Mehr Flexibilität → weniger Effizienz**

---

### 4. Integration von Accelerators (sehr wichtig!)
#### 1. In-Data-Path
- Accelerator arbeitet **während Daten fließen**
- Kaum Datenkopien
- Beispiel:
    - SmartNICs
    - Computational Storage
- **Schwierige Integration**

#### 2. On-the-Side
- CPU besitzt Daten
- Accelerator bekommt Kopien
- Einfach zu integrieren
- **Hoher Data-Movement-Overhead**
- Beispiel:
    - GPUs, TPUs

#### 3. Co-Processor
- Accelerator arbeitet direkt auf CPU-Daten
- Sehr niedrige Latenz
- System stark spezialisiert
- Beispiel:
    - NPUs, Vector Units in CPUs

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
# Vorlesung 9: Networking

### 1. Überblick & Lernziele

Die Vorlesung behandelt:
- Klassisches **Socket-basiertes Networking**
- Vor- und Nachteile von **OS-basierter Netzwerkanbindung**
- **User-Space Networking** und **DPDK**
- **Remote Direct Memory Access (RDMA)**

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

Vorteil: Modularität  
Nachteil: **Overhead durch viele Schichten**

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

**Aber:** hoher Overhead durch Kernel-Beteiligung

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

**Viele Kopien + viele Kontextwechsel**

---

### 5. Das Kernproblem: CPU-Bottleneck
#### Trends:
- Netzwerkbandbreite:
    - Heute: **100–200 Gbps**
- CPU-Frequenz:
    - Seit Jahren ~3 GHz
- Kleinste Ethernet-Frames:
    - **~150 Mio. Pakete/Sekunde bei 100 Gbps**

**OS + CPU können pro Paket kaum noch Arbeit leisten**

**Faustzahl:**
- DRAM-Zugriff: 60–100 ns
- Zeit zwischen Paketen bei 100 Gbps: **~6.7 ns**

**Schon ein Cache Miss ist zu teuer**

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

Bei 10 Gbps: ~15 Mio. System Calls / Sekunde  
Bei 100 Gbps: praktisch **nicht skalierbar**

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

DPDK baut den Linux-Netzwerkstack praktisch **neu in User Space**

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
**RDMA (Remote Direct Memory Access)**

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

Wichtig:
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

Enormer Performance-Gewinn

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

**RNIC = Netzwerk + Endhost**

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

Besonders stark bei **kleinen Nachrichten**

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

Sehr leistungsfähig, aber **komplex & fragil**

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

**Klausur-Merksatz:**
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

👉**Prüfungsargument:**
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