---
title: Pumping-Lemma
aliases:
  - Pumping Lemma
  - Pumplemma
  - Pumping-Lemma für reguläre Sprachen
  - Pumping-Lemma für kontextfreie Sprachen
tags:
  - automaten
  - logik
description: "Pumping-Lemma für reguläre und kontextfreie Sprachen — notwendige Bedingung für Sprachzugehörigkeit, verwendet zum Nachweis der Nicht-Regularität bzw. Nicht-Kontextfreiheit."
draft: false
---

Das **Pumping-Lemma** ist ein Werkzeug, um zu beweisen, dass eine [[Formale Sprachen|Sprache]] **nicht** zu einer bestimmten Sprachklasse gehört. Es formuliert eine **notwendige** (aber nicht hinreichende) Bedingung.

## Pumping-Lemma für reguläre Sprachen

> **Satz**: Sei $L$ eine reguläre Sprache. Dann existiert eine Zahl $n \geq 1$ (Pumping-Länge), sodass für jedes Wort $w \in L$ mit $|w| \geq n$ eine Zerlegung $w = xyz$ existiert mit:
> 1. $|y| \geq 1$ (der Pumping-Teil ist nicht leer)
> 2. $|xy| \leq n$
> 3. $\forall k \geq 0: xy^kz \in L$ (Aufpumpen und Abpumpen ergibt wieder Wörter in $L$)

### Beweisintuition

Ein DFA mit $n$ Zuständen muss bei einem Wort der Länge $\geq n$ mindestens einen Zustand **wiederholt** besuchen (Schubfachprinzip). Die Schleife zwischen dem ersten Wiederholungszustand kann beliebig oft durchlaufen werden.

### Beweisschema (Nicht-Regularität)

Um zu zeigen, dass $L$ **nicht regulär** ist:
1. Angenommen, $L$ wäre regulär mit Pumping-Länge $n$
2. Wähle ein **geschicktes** Wort $w \in L$ mit $|w| \geq n$
3. Zeige, dass **für jede** Zerlegung $w = xyz$ mit $|y| \geq 1$, $|xy| \leq n$
4. ein $k$ existiert, sodass $xy^kz \notin L$ → Widerspruch

> [!WARNING]
> Die Wortwahl in Schritt 2 ist entscheidend. Man muss ein Wort finden, bei dem **jede** zulässige Zerlegung zum Widerspruch führt.

### Klassisches Beispiel

$L = \{a^n b^n \mid n \geq 0\}$ ist **nicht regulär**:
- Wähle $w = a^n b^n$
- Wegen $|xy| \leq n$ besteht $y$ nur aus $a$'s: $y = a^j$ mit $j \geq 1$
- $xy^0z = a^{n-j}b^n \notin L$, da $n - j \neq n$ → Widerspruch

## Pumping-Lemma für kontextfreie Sprachen

> **Satz**: Sei $L$ eine kontextfreie Sprache. Dann existiert $n \geq 1$, sodass für jedes $w \in L$ mit $|w| \geq n$ eine Zerlegung $w = uvxyz$ existiert mit:
> 1. $|vy| \geq 1$ (mindestens ein Pumping-Teil ist nicht leer)
> 2. $|vxy| \leq n$
> 3. $\forall k \geq 0: uv^kxy^kz \in L$

### Beweisintuition

In einem hinreichend großen Ableitungsbaum einer [[Kontextfreie Grammatiken|CFG]] muss sich eine Variable **wiederholen**. Die Teilbäume der Wiederholung können beliebig oft eingesetzt werden.

### Klassisches Beispiel

$L = \{a^n b^n c^n \mid n \geq 0\}$ ist **nicht kontextfrei**:
- Wähle $w = a^n b^n c^n$
- Da $|vxy| \leq n$, kann $vxy$ höchstens **zwei** der drei Symbole enthalten
- Aufpumpen verändert die Anzahl von höchstens zwei Symbolen → Gleichgewicht gestört → Widerspruch

## Vergleich

| Eigenschaft | Regulär | Kontextfrei |
|---|---|---|
| Zerlegung | $w = xyz$ (3 Teile) | $w = uvxyz$ (5 Teile) |
| Pumping-Teile | $y$ | $v$ und $y$ (synchron) |
| Längenbedingung | $|xy| \leq n$ | $|vxy| \leq n$ |
| Widerlegt | Regularität | Kontextfreiheit |

## Related Concepts

- [[Deterministische Endliche Automaten]]: Pumping-Lemma basiert auf dem Schubfachprinzip für DFA-Zustände
- [[Kontextfreie Grammatiken]]: CFL-Pumping basiert auf Wiederholungen im Ableitungsbaum
- [[Formale Sprachen]]: Hierarchie der Sprachklassen
