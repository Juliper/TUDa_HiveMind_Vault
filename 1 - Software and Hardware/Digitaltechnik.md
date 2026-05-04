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

## Zusammenfassung

Digitaltechnik legt die mathematischen und technischen Grundlagen digitaler Systeme. Die ersten Vorlesungen decken die Informationsdarstellung ab (Zahlensysteme, Kodierung vorzeichenbehafteter Zahlen) und die algebraischen Werkzeuge zur Beschreibung und Minimierung von Schaltfunktionen (Boolesche Algebra, Normalformen, KV-Diagramme). Darauf aufbauend werden Schaltungen klassifiziert (Schaltnetz vs. Schaltwerk), Gatter und ihre Symbole eingeführt, Entwurfstechniken wie Bubble Pushing und zweistufige Logik behandelt, sowie wichtige Bausteine (Volladdierer, Multiplexer, Decoder) erarbeitet. Das Zeitverhalten ($t_{pd}$, $t_{cd}$, Glitches, Kritischer Pfad) schließt den Bogen von der abstrakten Boole'schen Funktion zum physikalischen Schaltkreis.

## Übungsaufgaben

<!-- Links zu Altklausuren und Übungsblättern hier einfügen -->
