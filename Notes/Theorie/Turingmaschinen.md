---
title: Turingmaschinen
aliases:
  - TM
  - Turing Machine
  - Turingmaschine
  - Church-Turing-These
tags:
  - automaten
  - logik
description: "Turingmaschinen — universelles Berechnungsmodell mit unbeschränktem Band, Church-Turing-These und Varianten (Mehrband-TM, NTM)."
draft: false
---

Eine **Turingmaschine** (TM) ist das mächtigste Automatenmodell und dient als formale Definition von **Berechenbarkeit**. Sie erkennt die [[Formale Sprachen|rekursiv aufzählbaren Sprachen]] (Typ 0).

## Formale Definition

Eine TM ist ein 7-Tupel $M = (Q, \Sigma, \Gamma, \delta, q_0, q_{acc}, q_{rej})$:

| Komponente | Bedeutung |
|---|---|
| $Q$ | Endliche Zustandsmenge |
| $\Sigma$ | Eingabealphabet (ohne Blank $\sqcup$) |
| $\Gamma \supseteq \Sigma \cup \{\sqcup\}$ | Bandalphabet (mit Blank-Symbol $\sqcup$) |
| $\delta: Q \times \Gamma \to Q \times \Gamma \times \{L, R\}$ | Übergangsfunktion |
| $q_0 \in Q$ | Startzustand |
| $q_{acc} \in Q$ | Akzeptierender Endzustand |
| $q_{rej} \in Q$ | Verwerfender Endzustand ($q_{acc} \neq q_{rej}$) |

Ein Schritt $\delta(q, a) = (q', b, D)$: Im Zustand $q$, lese $a$ → schreibe $b$, gehe in Zustand $q'$, bewege Kopf in Richtung $D \in \{L, R\}$.

## Berechnung und Akzeptanz

Die TM startet mit der Eingabe $w$ auf dem Band und dem Kopf auf dem ersten Symbol. Sie **hält**, wenn $q_{acc}$ oder $q_{rej}$ erreicht wird.

| Ergebnis | Bedingung |
|---|---|
| **Akzeptiert** $w$ | TM erreicht $q_{acc}$ |
| **Verwirft** $w$ | TM erreicht $q_{rej}$ |
| **Hält nicht** | TM läuft unendlich weiter (möglich!) |

> [!WARNING]
> Im Gegensatz zu DFA/NFA/PDA kann eine TM auf manchen Eingaben **nie halten**. Dies ist ein fundamentaler Unterschied.

## Sprachklassen

| Klasse | Definition |
|---|---|
| **Entscheidbar** (rekursiv) | $\exists$ TM, die $L$ erkennt und auf **jeder** Eingabe hält |
| **Erkennbar** (rekursiv aufzählbar) | $\exists$ TM, die $w \in L$ akzeptiert (bei $w \notin L$ evtl. nicht hält) |
| **Nicht erkennbar** | Keine TM erkennt $L$ |

$$\text{entscheidbar} \subsetneq \text{erkennbar} \subsetneq \mathcal{P}(\Sigma^*)$$

## Varianten

Alle folgenden Varianten sind **äquivalent** zur Standard-TM:

| Variante | Unterschied |
|---|---|
| **Mehrband-TM** | $k$ Bänder mit unabhängigen Köpfen |
| **Nichtdeterministische TM** (NTM) | $\delta$ liefert Menge von Möglichkeiten |
| **Beidseitig unendliches Band** | Band in beide Richtungen unbegrenzt |
| **Mehrspurige TM** | Ein Band, aber mehrere Spuren pro Zelle |

> [!NOTE]
> Die Äquivalenz gilt bezüglich der **erkennbaren Sprachen**. Bezüglich Laufzeit können Varianten effizienter sein (z. B. Mehrband simuliert $k$ Bänder auf einem Band mit quadratischem Overhead).

## Church-Turing-These

> Der intuitive Begriff "berechenbar" stimmt mit der formalen Klasse der Turing-berechenbaren Funktionen überein.

Die Church-Turing-These ist **keine bewiesene mathematische Aussage**, sondern eine allgemein akzeptierte Hypothese. Alle bekannten Berechnungsmodelle (Lambda-Kalkül, While-Programme, RAM-Maschinen, …) sind äquivalent zur Turingmaschine.

## Universelle Turingmaschine

Eine **universelle TM** $U$ erhält als Eingabe die Kodierung $\langle M, w \rangle$ einer TM $M$ und einer Eingabe $w$ und simuliert $M$ auf $w$:

$$U(\langle M, w \rangle) = M(w)$$

Dies zeigt, dass ein einzelner Algorithmus alle anderen simulieren kann — das theoretische Fundament des **Universalrechners**.

## Related Concepts

- [[Entscheidbarkeit und Berechenbarkeit]]: Halteproblem und Reduktionen
- [[Kellerautomaten]]: Schwächeres Modell (Stack statt unbeschränktes Band)
- [[Formale Sprachen]]: TMs erkennen Typ-0-Sprachen
