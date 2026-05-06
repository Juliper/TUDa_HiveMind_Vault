---
title: Nichtdeterministische Endliche Automaten
aliases:
  - NFA
  - Nichtdeterministischer Endlicher Automat
  - Nondeterministic Finite Automaton
  - ε-NFA
  - Potenzmengenkonstruktion
  - Subset Construction
tags:
  - automaten
  - logik
description: "NFA und ε-NFA — nichtdeterministische Automaten mit Potenzmengenkonstruktion (Subset Construction) zur Äquivalenz mit DFA."
draft: false
---

Ein **Nichtdeterministischer Endlicher Automat** (NFA) erweitert den [[Deterministische Endliche Automaten|DFA]] um Nichtdeterminismus: In einem Zustand können bei gleicher Eingabe **mehrere** Folgezustände möglich sein.

## Formale Definition

Ein NFA ist ein 5-Tupel $A = (Q, \Sigma, \Delta, q_0, F)$:

| Komponente | Bedeutung |
|---|---|
| $Q$ | Endliche Zustandsmenge |
| $\Sigma$ | Eingabealphabet |
| $\Delta \subseteq Q \times \Sigma \times Q$ | Übergangsrelation (oder $\delta: Q \times \Sigma \to \mathcal{P}(Q)$) |
| $q_0 \in Q$ | Startzustand |
| $F \subseteq Q$ | Endzustände |

> [!NOTE]
> Im Gegensatz zum DFA kann $\delta(q, a)$ eine **Menge** von Zuständen sein (auch die leere Menge).

## $\varepsilon$-NFA

Ein $\varepsilon$-NFA erlaubt zusätzlich **spontane Übergänge** ohne Eingabe:

$$\delta: Q \times (\Sigma \cup \{\varepsilon\}) \to \mathcal{P}(Q)$$

Die **$\varepsilon$-Hülle** (epsilon closure) eines Zustands $q$ ist die Menge aller Zustände, die von $q$ durch beliebig viele $\varepsilon$-Übergänge erreichbar sind:

$$\text{ECLOSE}(q) = \{p \in Q \mid q \xrightarrow{\varepsilon^*} p\}$$

## Akzeptanz

Ein NFA akzeptiert ein Wort $w$, wenn **mindestens ein** Berechnungspfad in einem Endzustand endet:

$$L(A) = \{w \in \Sigma^* \mid \hat{\delta}(q_0, w) \cap F \neq \emptyset\}$$

Dabei ist $\hat{\delta}(q_0, w)$ die Menge aller nach Lesen von $w$ erreichbaren Zustände.

## Potenzmengenkonstruktion (Subset Construction)

Jeder NFA $A = (Q, \Sigma, \delta, q_0, F)$ kann in einen äquivalenten DFA umgewandelt werden:

$$A' = (\mathcal{P}(Q), \Sigma, \delta', \{q_0\}, F')$$

| Komponente | Definition |
|---|---|
| Zustände | $\mathcal{P}(Q)$ — jede Teilmenge von $Q$ ist ein DFA-Zustand |
| $\delta'(S, a)$ | $\bigcup_{q \in S} \delta(q, a)$ |
| Startzustand | $\{q_0\}$ (bei $\varepsilon$-NFA: $\text{ECLOSE}(q_0)$) |
| Endzustände | $F' = \{S \subseteq Q \mid S \cap F \neq \emptyset\}$ |

> [!IMPORTANT]
> Die Potenzmengenkonstruktion kann im schlimmsten Fall zu **exponentiell vielen** Zuständen führen ($2^{|Q|}$). In der Praxis sind meist nur wenige der $2^{|Q|}$ Teilmengen erreichbar.

## NFA vs. DFA

| Eigenschaft | DFA | NFA |
|---|---|---|
| Übergangsfunktion | Total, deterministisch | Relational, nichtdeterministisch |
| Zustandsanzahl | Kann exponentiell größer sein | Oft kompakter |
| Akzeptanz | Eindeutiger Pfad | Existenz eines akzeptierenden Pfads |
| Sprachklasse | Reguläre Sprachen | Reguläre Sprachen (**gleich mächtig**) |
| Komplementbildung | Trivial (Endzustände tauschen) | Erfordert erst Determinisierung |

## Äquivalenz

$$\text{DFA} \equiv \text{NFA} \equiv \varepsilon\text{-NFA}$$

Alle drei Modelle erkennen **exakt** die Klasse der regulären Sprachen. Die Konversionsrichtungen:
- NFA → DFA: Potenzmengenkonstruktion
- $\varepsilon$-NFA → NFA: $\varepsilon$-Elimination (Hüllenbildung)
- DFA → NFA: Trivial (jeder DFA ist ein spezieller NFA)

## Related Concepts

- [[Deterministische Endliche Automaten]]: Deterministisches Gegenstück
- [[Reguläre Ausdrücke]]: NFA-Konstruktion aus regulären Ausdrücken (Thompson's Construction)
- [[Formale Sprachen]]: NFAs erkennen reguläre Sprachen (Typ 3)
