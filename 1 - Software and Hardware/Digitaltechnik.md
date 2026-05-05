---
title: DT
aliases:
  - Digitaltechnik
tags:
  - 5CP
  - fb20
  - bachelor
  - pflichtmodul
  - semester-1
description: ""
draft: false
---
# Syllabus

| Moodle       | —                      |
| ------------ | ---------------------- |
| Dozent       | —                      |
| Vorlesung    | —                      |
| Übung        | —                      |
| Prüfungsform | Klausur                |
# Vorlesungen

## Lecture 1 - Einführung & Zahlensysteme
* TODO - Schichtenmodell (Hierachie, Modularität, Regularität)
- [[Zahlensysteme]]: Stellenwertsystem; Binär, Oktal, Dezimal, Hexadezimal; Basis-Umrechnung (Integer & Fraktion); Binär↔Hex Shortcut
- TODO - Größenfaktoren nach IEC

## Lecture 2 - Kodierung & Schaltalgebra
- [[Zweierkomplement]]: Vorzeichen-Betrag, Einerkomplement, Zweierkomplement; BCD; Gray Code
- [[Boolesche Algebra]]: Einführung in Schaltvariablen und Grundoperationen (AND, OR, NOT)

## Lecture 3 - Boolesche Algebra & Normalformen
- [[Boolesche Algebra]]: vollständige Gesetze (Kommutativ, Assoziativ, Distributiv, Absorption, De Morgan); Dualitätsprinzip
- [[Normalformen]]: Minterm, Maxterm, DNF, KNF; Ableitung aus Wahrheitstabelle
- [[Karnaugh-Veitch-Diagramme]]: Aufbau, Gray-Code-Anordnung, Minimierungsregeln, Don't-Cares

## Lecture 4 - Kombinatorische Logik
- [[Kombinatorische Logik]]: Schaltungsmodell (Eingänge, Ausgänge, funktionales/zeitliches Verhalten); Verbindungsknoten vs. Schaltungselemente; Schaltnetz (azyklisch, kein Gedächtnis) vs. Schaltwerk (mit Rückkopplung); Operatorrangfolge (NOT > AND > XOR > OR); Begriffe: Literal, Implikant, Primimplikant
- [[Kombinatorische Logik#Volladdierer (Full Adder)|Volladdierer]]: $S = A \oplus B \oplus C_{in}$, $C_{out} = AB + AC_{in} + BC_{in}$; Einführung Bubble Pushing

## Lecture 5 - Logikgatter & Multiplexer
- [[Logikgatter]]: Gattertypen (AND, OR, NOT, NAND, NOR, XOR, XNOR); XOR als Paritätsfunktion; Bubble Pushing vollständig (Bubbles vorwärts/rückwärts schieben, AND↔OR-Tausch via De Morgan, Bubbles löschen sich paarweise); zweistufige AND-OR-Logik aus DNF; schematische Konventionen
- [[Multiplexer]]: MUX2 und MUX4 (Wahrheitstabelle, Gleichung, Gatterrealisierung); MUX als Look-Up Table (LUT) / ROM-Prinzip; Dekodierer ($n$ Eingänge → $2^n$ One-Hot-Ausgänge = alle Minterme)

## Lecture 6 - 7-Segment-Anzeige & Zeitverhalten
- **7-Segment-Anzeige** (Entwurfsbeispiel): 4-Bit-Hex-Eingang → Segmente a–g; Wahrheitstabelle mit kompakter $\sum m + \sum d$ Notation (Don't-Cares für Zustände 10–15); KV-Minimierung pro Segment; minimierte Ausdrücke; KNF-Minimierung mit Maxterms auf KV-Karte; Hinweis auf Quine-McCluskey als algorithmische Alternative
- [[Zeitverhalten]]: Propagation Delay $t_{pd}$ (Maximum, letzter Ausgang stabil), Contamination Delay $t_{cd}$ (Minimum, erster Ausgang beginnt zu wechseln); Glitches/Hazards durch Pfade unterschiedlicher Länge; Kritischer Pfad bestimmt $t_{pd}$

## Lecture 7 — Arithmetische Grundschaltungen
- [[Arithmetische Schaltungen]]: Shifter (logisch, Rotation, arithmetisch; Barrel Shifter; Multiplikation durch Shifts); Halbaddierer ($S = A \oplus B$, $C = AB$); Volladdierer aus 2 Halbaddierern + OR
- [[Arithmetische Schaltungen#Ripple-Carry-Adder (RCA)|RCA]]: Carry-Kette, kritischer Pfad $O(n)$; [[Arithmetische Schaltungen#Conditional Sum Adder (CSA)|CSA]]: Vorausberechnung beider Carry-Fälle + MUX
- [[Arithmetische Schaltungen#Carry Lookahead Adder (CLA)|CLA]]: Generate/Propagate-Signale ($G_i = A_i B_i$, $P_i = A_i + B_i$), blockweise Carry-Berechnung; Parallel Prefix Adder $O(\log n)$
- [[Arithmetische Schaltungen#Subtrahierer (Subtractor)|Subtrahierer]]: $A - B = A + \overline{B} + 1$; Vergleicher ($<$ via Subtraktion, $=$ via XNOR-Baum); [[Arithmetische Schaltungen#Multiplizierer (Multiplier)|Multiplizierer]]: Partialprodukte, $O(n^2)$ Fläche

## Lecture 8 — Sequentielle Schaltungen & Pipelining
- [[Speicherelemente]]: SR-Latch, D-Latch (transparent/latched), D-Flip-Flop (flankengesteuert), Register ($n$ parallele DFFs)
- [[Speicherelemente#Synchrone Entwurfsdisziplin|Synchrone Entwurfsdisziplin]]: Rückkopplungen durch Register aufbrechen; alle Register gleicher Takt; jeder zyklische Pfad enthält Register
- [[Speicherelemente#Zeitverhalten von Flip-Flops|DFF-Timing]]: $t_{setup}$, $t_{hold}$, $t_a$ (Aperture); $t_{ccq}$, $t_{pcq}$ (Clock-to-Q); dynamische Entwurfsdisziplin: Setup-Bedingung ($f_{CLK} \leq \frac{1}{t_{pcq}+t_{pd}+t_{setup}}$), Hold-Bedingung ($t_{ccq}+t_{cd} \geq t_{hold}$)
- [[Speicherelemente#Taktverschiebung (Clock Skew)|Clock Skew]]; [[Speicherelemente#Metastabilität|Metastabilität]] und Synchronizer (2-stufiges Schieberegister)
- [[Pipelining]]: räumliche vs. zeitliche Parallelität; Datensatz, Latenz, Durchsatz; Pipeline-Register erhöhen $f_{CLK}$ auf Kosten der Latenz; ausbalancierte Stufen

## Lecture 9 — Endliche Zustandsautomaten (FSM)
- [[Endliche Zustandsautomaten]]: Definition (Eingänge, Ausgänge, Zustand, CLK, Reset); Zustandsdiagramm als gerichteter Graph; Anwendungen (Ampelsteuerung, Zahlenschloss, Mustererkennung, Steuerwerk)
- [[Endliche Zustandsautomaten#Moore vs. Mealy|Moore vs. Mealy]]: Ausgaben im Zustand vs. an Kanten; Moore = statische Ausgaben, mehr Zustände; Mealy = schnellere Reaktion (1 Takt früher), weniger Zustände
- [[Endliche Zustandsautomaten#Zustandskodierung|Zustandskodierung]]: Binär, One-Hot, Ausgabekodierung; kodierte Tabellen → KV-Minimierung → Schaltplan (Gatter + Register)
- [[Endliche Zustandsautomaten#Entwurfsverfahren (Design Flow)|FSM-Entwurfsverfahren]]: Spezifikation → Diagramm → Tabellen → Gleichungen → Schaltung
- [[Endliche Zustandsautomaten#Zerlegen von Zustandsautomaten (FSM Decomposition)|FSM-Dekomposition]]: komplexe FSMs in kommunizierende Teil-FSMs aufteilen

## Lecture 10 — CMOS-Technologie & SystemVerilog Einführung
- [[CMOS]]: NMOS/PMOS als spannungsgesteuerte Schalter; komplementäre CMOS-Logik (Pull-up PMOS + Pull-down NMOS); Entwurfsregeln (Seriell = AND, Parallel = OR, Pull-up = duales Netz)
- [[CMOS#Grundgatter|CMOS-Grundgatter]]: NOT (2T), NAND ($2n$T), NOR ($2n$T); NAND/NOR als native CMOS-Gatter; AND/OR benötigen Inverter
- [[CMOS#Komplexe Gatter (AOI / OAI)|Komplexe Gatter]]: AOI (AND-OR-Invert), OAI (OR-AND-Invert); [[CMOS#Transmission Gate (TG)|Transmission Gate]]; [[CMOS#Pseudo-NMOS|Pseudo-NMOS]] (statischer Stromverbrauch); [[CMOS#Tristate-Ausgang|Tristate-Buffer]] ($0$, $1$, $Z$)
- [[Verilog]]: HDL-Einführung; SystemVerilog-Syntax (Case-Sensitivity, Bezeichner, Kommentare); Modulstruktur; `assign` für kombinatorische Logik; bitweise und Reduktionsoperatoren; ternärer Operator (MUX); Konkatenation; numerische Literale; Operatorpräzedenz
- [[Verilog#Strukturelle Beschreibung|Strukturelle Beschreibung]]: Modulinstanziierung; Portzuweisung nach Position und nach Namen

## Lecture 11 — SystemVerilog für sequentielle Logik
- [[Verilog#Sequentielle Logik (`always`-Blöcke)|`always`-Blöcke]]: Ereignissteuerung (`@posedge`, `@*`, `@(a,b)`); Blocking (`=`) vs. Non-Blocking (`<=`) Zuweisungen; Deltazyklus-Semantik
- [[Verilog#Spezialisierte `always`-Blöcke|Spezialisierte Blöcke]]: `always_comb`, `always_ff`, `always_latch` — Synthese-Tools erkennen Designer-Absicht
- [[Verilog#Modellierung von Speicherelementen|Speicherelemente in SV]]: D-Latch, DFF, rücksetzbare FFs (synchron/asynchron), FF mit Enable; allgemeine Zuweisungsregeln
- [[Verilog#Parametrisierte Module|Parametrisierte Module]]: `#(parameter ...)`, `localparam`; [[Verilog#`generate`-Anweisung|`generate`]]: iterative Instanziierung (z. B. Schieberegister-Kette)
- [[Verilog#Testumgebungen (Testbenches)|Testbenches]]: `initial`-Block, `$dumpfile`/`$dumpvars`, `$display`, `$finish`, `assert`; einfacher vs. selbstprüfender Testrahmen; Takterzeugung

## Lecture 12 — Sequentielle Grundelemente & Speicherfelder
- [[Halbleiterspeicher#Schieberegister mit parallelem Laden|Schieberegister]]: paralleles Laden ($Load=1$) vs. serielles Schieben ($Load=0$); Seriell-Parallel- und Parallel-Seriell-Wandler
- [[Halbleiterspeicher]]: Speicherfeld als 2D-Bit-Array; $N$ Adressbits, $M$ Datenbits → Tiefe $2^N$, Breite $M$; Größenberechnung
- [[Halbleiterspeicher#Wordline und Bitline|Wordlines & Bitlines]]: Decoder → One-Hot-Wordline; Bitline für Lesen/Schreiben; Bitzelle (Store/Load-Operationen)

## Lecture 13 — Speicher, Logikfelder & FPGA
- [[Halbleiterspeicher#Logik via Speicher|Logik via Speicher]]: ROM als Wahrheitstabelle; LUT (Lookup Table) als $2^k \times 1$-Bit-Speicher für $k$-stellige Boolesche Funktionen
- [[Halbleiterspeicher#SystemVerilog-Modellierung|SV RAM/ROM]]: `always_ff` für synchrones Schreiben, `assign` für asynchrones Lesen; ROM via `always_comb case`
- [[Programmierbare Logik#PLA (Programmable Logic Array)|PLA]]: programmierbare AND- + OR-Ebene (DNF); [[Programmierbare Logik#PAL (Programmable Array Logic)|PAL]]: programmierbare AND- + feste OR-Ebene
- [[Programmierbare Logik#FPGA (Field Programmable Gate Array)|FPGA]]: Architektur (Logic Cells mit LUT + FF, I/O Blocks, Switch Matrix, Function Blocks); Konfigurationsspeicher (SRAM/Flash); ASIC vs. Prozessor vs. FPGA (Performanz vs. Flexibilität); FPGA-Hersteller (Xilinx, Intel/Altera, Microsemi, Lattice)

## Lecture 14 — Klausurvorbereitung & Ausblick
- Wiederholung des Gesamtstoffs; Klausurorganisation und -ablauf
- Ausblick auf weiterführende Veranstaltungen: Rechnerorganisation, Architekturentwurf, Compilerbau, Embedded Systems, Kryptographische Protokolle

# Klausurvorbereitung

> [!IMPORTANT] Prüfungsrelevant
> - Basis-Umrechnung (Dezimal ↔ Binär ↔ Hex) — in beide Richtungen, auch für Nachkommastellen
> - Zweierkomplement: Negation, Wertebereich, Addition ohne Sonderbehandlung
> - De Morgan anwenden und Boolean-Ausdrücke vereinfachen
> - DNF und KNF aus Wahrheitstabellen ableiten
> - KV-Diagramme für bis zu 4 Variablen; Gray-Code-Reihenfolge; maximale Gruppen bilden
> - Schaltnetz vs. Schaltwerk unterscheiden (Azyklizität als Kriterium)
> - Volladdierer: Gleichungen für S und $C_{out}$ kennen und herleiten
> - Bubble Pushing: Bubbles verschieben, AND↔OR tauschen, Bubbles kürzen
> - MUX als Funktion und als LUT verstehen; Decoder-Ausgänge als Minterme
> - $t_{pd}$ und $t_{cd}$ berechnen (längster / kürzester Pfad); Glitch-Ursachen erklären
> - Addierer: RCA-Prinzip, CLA mit Generate/Propagate herleiten; Subtrahierer über Zweierkomplement
> - Shifter-Typen unterscheiden; Barrel Shifter als MUX-Kaskade
> - SR-Latch, D-Latch, DFF: Funktionsweise und Unterschiede (pegelgesteuert vs. flankengesteuert)
> - $t_{setup}$, $t_{hold}$, $t_{ccq}$, $t_{pcq}$: Setup- und Hold-Bedingung aufstellen und prüfen; Hold-Verletzung beheben
> - Pipelining: Durchsatz vs. Latenz abwägen; $f_{CLK}$ mit Pipeline-Stufen berechnen
> - FSM-Entwurf: Zustandsdiagramm → Tabellen → kodierte Tabellen → KV-Minimierung → Schaltung
> - Moore vs. Mealy: Unterschiede erkennen, Automaten ineinander umwandeln
> - CMOS: Pull-up/Pull-down-Netzwerke entwerfen (Seriell = AND, Parallel = OR, duales Netz); NAND/NOR als native Gatter; Transistoranzahl bestimmen
> - Komplexe Gatter (AOI/OAI): Pull-down-Funktion → Pull-up als duales Netz ableiten
> - Transmission Gate, Pseudo-NMOS, Tristate: Funktionsweise und Einsatzgebiete
> - SystemVerilog: `assign` für kombinatorische Logik; `always_ff`/`always_comb` korrekt einsetzen; Blocking vs. Non-Blocking verstehen
> - Speicherelemente in SV modellieren: D-Latch, DFF, rücksetzbares FF, FF mit Enable
> - Speicherfelder: Tiefe/Breite/Größe berechnen; Wordline/Bitline-Prinzip; LUT als Funktionsspeicher
> - PLA vs. PAL vs. ROM: Unterschied in programmierbaren Ebenen erkennen
> - FPGA-Architektur: LC (LUT + FF), IOB, Switch Matrix, Function Blocks benennen und erklären

## Zusammenfassung

Digitaltechnik legt die mathematischen und technischen Grundlagen digitaler Systeme. Die ersten Vorlesungen decken die Informationsdarstellung ab (Zahlensysteme, Kodierung vorzeichenbehafteter Zahlen) und die algebraischen Werkzeuge zur Beschreibung und Minimierung von Schaltfunktionen (Boolesche Algebra, Normalformen, KV-Diagramme). Darauf aufbauend werden Schaltungen klassifiziert (Schaltnetz vs. Schaltwerk), Gatter und ihre Symbole eingeführt, Entwurfstechniken wie Bubble Pushing und zweistufige Logik behandelt, sowie wichtige Bausteine (Volladdierer, Multiplexer, Decoder) erarbeitet. Das Zeitverhalten ($t_{pd}$, $t_{cd}$, Glitches, Kritischer Pfad) schließt den Bogen von der abstrakten Boole'schen Funktion zum physikalischen Schaltkreis. VL07 vertieft arithmetische Schaltungen (Addierer-Hierarchie von RCA über CSA bis CLA, Subtrahierer, Vergleicher, Multiplizierer). VL08 führt Speicherelemente ein (Latches, Flip-Flops, Register), etabliert die synchrone Entwurfsdisziplin mit Timing-Constraints ($t_{setup}$, $t_{hold}$, $t_{pcq}$, $t_{ccq}$) und behandelt Pipelining als Mittel zur Durchsatzsteigerung. VL09 widmet sich Endlichen Zustandsautomaten (FSMs): Moore- und Mealy-Varianten, vollständiger Entwurfsablauf von der Spezifikation über Zustandsdiagramme und -tabellen bis zur minimierten Gatterschaltung, und FSM-Dekomposition. VL10 behandelt die CMOS-Technologie als physikalische Grundlage digitaler Gatter (Pull-up/Pull-down-Netzwerke, komplexe Gatter, Transmission Gate, Pseudo-NMOS, Tristate) und führt SystemVerilog als Hardwarebeschreibungssprache ein (Modulstruktur, `assign`, Operatoren, strukturelle Instanziierung). VL11 vertieft SystemVerilog für sequentielle Logik (`always`-Blöcke, Blocking vs. Non-Blocking, `always_ff`/`always_comb`/`always_latch`, Modellierung von Latches und Flip-Flops, parametrisierte Module, `generate`, Testbenches). VL12 behandelt sequentielle Grundelemente (Schieberegister mit parallelem Laden) und Speicherfelder (2D-Bit-Arrays, Wordlines, Bitlines, Bitzellen). VL13 zeigt, wie Speicher als Logik eingesetzt werden (ROM, LUT), führt programmierbare Logikbausteine ein (PLA, PAL) und behandelt die FPGA-Architektur (Logic Cells, I/O Blocks, Switch Matrix, Function Blocks, Konfigurationsspeicher). VL14 schließt mit Klausurvorbereitung und Ausblick auf weiterführende Veranstaltungen.

## Übungsaufgaben

<!-- Links zu Altklausuren und Übungsblättern hier einfügen -->
