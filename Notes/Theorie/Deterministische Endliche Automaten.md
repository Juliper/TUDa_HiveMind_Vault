---
title: Deterministische Endliche Automaten
aliases:
  - DFA
  - Deterministischer Endlicher Automat
  - Deterministic Finite Automaton
tags:
  - automaten
  - logik
description: "DFA — formale Definition als 5-Tupel, erweiterte Übergangsfunktion, akzeptierte Sprache, Produktkonstruktion und Minimalautomaten."
draft: false
---

Ein **Deterministischer Endlicher Automat** (DFA) ist das einfachste Berechnungsmodell für [[Formale Sprachen|reguläre Sprachen]]. In jedem Zustand ist bei gegebener Eingabe der nächste Zustand **eindeutig** bestimmt.

## Formale Definition

Ein DFA ist ein 5-Tupel $A = (Q, \Sigma, \delta, q_0, F)$:

| Komponente | Bedeutung |
|---|---|
| $Q$ | Endliche Zustandsmenge |
| $\Sigma$ | Eingabealphabet |
| $\delta: Q \times \Sigma \to Q$ | Übergangsfunktion (total) |
| $q_0 \in Q$ | Startzustand |
| $F \subseteq Q$ | Menge der akzeptierenden (End-)Zustände |

> [!IMPORTANT]
> Die Übergangsfunktion $\delta$ ist **total**: Für jedes Paar $(q, a)$ gibt es genau einen Folgezustand. Fehlende Übergänge führen implizit in einen **Fangzustand** (trap state), der nicht akzeptiert.

## Erweiterte Übergangsfunktion

Die Funktion $\hat{\delta}: Q \times \Sigma^* \to Q$ verarbeitet ganze Wörter:

$$\hat{\delta}(q, \varepsilon) = q \qquad \hat{\delta}(q, wa) = \delta(\hat{\delta}(q, w), a)$$

## Akzeptierte Sprache

$$L(A) = \{w \in \Sigma^* \mid \hat{\delta}(q_0, w) \in F\}$$

Ein Wort $w$ wird akzeptiert, wenn der DFA nach Lesen aller Symbole in einem Endzustand steht.

## Darstellung

DFAs werden typisch als **Zustandsdiagramme** dargestellt:
- Zustände als Kreise (Doppelkreis = Endzustand)
- Kanten beschriftet mit Eingabesymbolen
- Startpfeil auf $q_0$

## Produktkonstruktion

Für DFAs $A_1 = (Q_1, \Sigma, \delta_1, q_{0,1}, F_1)$ und $A_2 = (Q_2, \Sigma, \delta_2, q_{0,2}, F_2)$ konstruiert man den **Produktautomaten** $A = (Q_1 \times Q_2, \Sigma, \delta, (q_{0,1}, q_{0,2}), F)$ mit:

$$\delta((p, q), a) = (\delta_1(p, a),\; \delta_2(q, a))$$

| Ziel | Endzustände $F$ |
|---|---|
| $L(A_1) \cap L(A_2)$ | $F_1 \times F_2$ |
| $L(A_1) \cup L(A_2)$ | $(F_1 \times Q_2) \cup (Q_1 \times F_2)$ |
| $L(A_1) \setminus L(A_2)$ | $F_1 \times (Q_2 \setminus F_2)$ |

## Komplementautomat

Durch Vertauschen von End- und Nicht-Endzuständen erkennt ein DFA die Komplementsprache:

$$A' = (Q, \Sigma, \delta, q_0, Q \setminus F) \quad \Longrightarrow \quad L(A') = \overline{L(A)}$$

> [!WARNING]
> Diese Konstruktion funktioniert nur für DFAs (totale Übergangsfunktion), **nicht** direkt für NFAs.

## Minimalautomat

Zu jeder regulären Sprache $L$ existiert ein **eindeutiger minimaler DFA** (bis auf Isomorphie). Äquivalente Zustände ($p \sim q$ gdw. $\forall w: \hat{\delta}(p,w) \in F \Leftrightarrow \hat{\delta}(q,w) \in F$) werden verschmolzen.

## Related Concepts

- [[Nichtdeterministische Endliche Automaten]]: NFA-Variante mit Potenzmengenkonstruktion zur DFA-Konversion
- [[Reguläre Ausdrücke]]: Äquivalente Beschreibung regulärer Sprachen (Satz von Kleene)
- [[Formale Sprachen]]: DFAs erkennen genau die regulären Sprachen (Typ 3)
- [[Pumping-Lemma]]: Technik zum Nachweis der Nicht-Regularität
