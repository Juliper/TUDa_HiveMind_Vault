---
title: Kellerautomaten
aliases:
  - PDA
  - Pushdown Automaton
  - Kellerautomat
  - Pushdown Automata
tags:
  - automaten
  - logik
description: "Kellerautomaten (PDA) — Erweiterung endlicher Automaten um einen Stack, Akzeptanz durch Endzustand oder leeren Keller, Äquivalenz zu kontextfreien Grammatiken."
draft: false
---

Ein **Kellerautomat** (Pushdown Automaton, PDA) erweitert einen [[Nichtdeterministische Endliche Automaten|NFA]] um einen **Stack** (Kellerspeicher) und erkennt damit genau die [[Kontextfreie Grammatiken|kontextfreien Sprachen]].

## Formale Definition

Ein PDA ist ein 7-Tupel $P = (Q, \Sigma, \Gamma, \delta, q_0, Z_0, F)$:

| Komponente | Bedeutung |
|---|---|
| $Q$ | Endliche Zustandsmenge |
| $\Sigma$ | Eingabealphabet |
| $\Gamma$ | **Kelleralphabet** (Stack-Symbole) |
| $\delta: Q \times (\Sigma \cup \{\varepsilon\}) \times \Gamma \to \mathcal{P}(Q \times \Gamma^*)$ | Übergangsfunktion |
| $q_0 \in Q$ | Startzustand |
| $Z_0 \in \Gamma$ | **Initialsymbol** des Kellers |
| $F \subseteq Q$ | Endzustände |

Ein Übergang $(q', \gamma) \in \delta(q, a, Z)$ bedeutet: Im Zustand $q$, bei Eingabe $a$ (oder $\varepsilon$), mit $Z$ oben auf dem Stack → gehe nach $q'$, ersetze $Z$ durch $\gamma$ (Push/Pop/Replace).

## Konfiguration und Berechnung

Eine **Konfiguration** ist ein Tripel $(q, w, \alpha)$:
- $q$ = aktueller Zustand
- $w$ = noch zu lesende Eingabe
- $\alpha \in \Gamma^*$ = Kellerinhalt (oberstes Symbol links)

Ein Berechnungsschritt: $(q, aw, Z\beta) \vdash (q', w, \gamma\beta)$ falls $(q', \gamma) \in \delta(q, a, Z)$.

## Akzeptanzmodi

| Modus | Bedingung |
|---|---|
| **Endzustand** | $(q_0, w, Z_0) \vdash^* (q_f, \varepsilon, \alpha)$ mit $q_f \in F$ |
| **Leerer Keller** | $(q_0, w, Z_0) \vdash^* (q, \varepsilon, \varepsilon)$ für beliebiges $q$ |

> [!IMPORTANT]
> Beide Akzeptanzmodi sind **äquivalent**: Jeder PDA mit Endzustand-Akzeptanz kann in einen mit Leerer-Keller-Akzeptanz umgewandelt werden und umgekehrt.

## Äquivalenz CFG ↔ PDA

$$\text{Kontextfreie Grammatiken} \equiv \text{PDA}$$

| Richtung | Verfahren |
|---|---|
| CFG → PDA | Für jede Regel $A \to \alpha$: Ersetze $A$ auf dem Stack durch $\alpha$; matche Terminale mit Eingabe |
| PDA → CFG | Konstruiere Variablen $[q, A, p]$ für „vom Zustand $q$ mit $A$ oben auf dem Stack zum Zustand $p$ mit gelesenem $A$" |

## Deterministische Kellerautomaten (DPDA)

Ein **DPDA** hat in jeder Konfiguration höchstens **einen** möglichen Übergang. Die von DPDAs erkannten Sprachen bilden eine **echte Teilklasse** der kontextfreien Sprachen:

$$\text{DPDA-Sprachen} \subsetneq \text{CFL}$$

Beispiel: $\{ww^R \mid w \in \{a,b\}^*\}$ ist kontextfrei, aber nicht DPDA-erkennbar (ohne Markierung der Mitte).

## Related Concepts

- [[Kontextfreie Grammatiken]]: Äquivalenter Formalismus (CFG ↔ PDA)
- [[Nichtdeterministische Endliche Automaten]]: PDA = NFA + Stack
- [[Formale Sprachen]]: PDAs erkennen Typ-2-Sprachen
- [[Turingmaschinen]]: Mächtigeres Modell mit unbeschränktem Speicher
