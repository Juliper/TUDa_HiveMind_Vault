---
title: Reguläre Ausdrücke
aliases:
  - Regular Expressions
  - Regex
  - Satz von Kleene
  - Kleene's Theorem
tags:
  - automaten
  - logik
description: "Reguläre Ausdrücke — Syntax, Semantik und Satz von Kleene (Äquivalenz zu endlichen Automaten)."
draft: false
---

**Reguläre Ausdrücke** (Regular Expressions) sind eine algebraische Notation zur Beschreibung [[Formale Sprachen|regulärer Sprachen]]. Sie sind äquivalent zu [[Deterministische Endliche Automaten|DFAs]] und [[Nichtdeterministische Endliche Automaten|NFAs]].

## Syntax

Reguläre Ausdrücke über einem Alphabet $\Sigma$ werden induktiv definiert:

| Ausdruck | Beschriebene Sprache $L(r)$ |
|---|---|
| $\emptyset$ | $\emptyset$ (leere Sprache) |
| $\varepsilon$ | $\{\varepsilon\}$ (nur das leere Wort) |
| $a$ (für $a \in \Sigma$) | $\{a\}$ (einzelnes Symbol) |
| $r_1 + r_2$ (Union) | $L(r_1) \cup L(r_2)$ |
| $r_1 \cdot r_2$ (Konkatenation) | $L(r_1) \cdot L(r_2)$ |
| $r^*$ (Kleene-Stern) | $L(r)^*$ |

**Operatorpriorität**: $*$ bindet stärker als $\cdot$, und $\cdot$ stärker als $+$.

## Beispiele

| Ausdruck | Sprache |
|---|---|
| $(a+b)^*$ | Alle Wörter über $\{a,b\}$ |
| $a^*b^*$ | Beliebig viele $a$, gefolgt von beliebig vielen $b$ |
| $(a+b)^*abb$ | Alle Wörter über $\{a,b\}$, die auf $abb$ enden |
| $(aa)^*$ | Wörter aus gerader Anzahl von $a$ |
| $\Sigma^* a \Sigma^*$ | Wörter, die mindestens ein $a$ enthalten |

## Satz von Kleene

$$\text{Reguläre Ausdrücke} \equiv \text{DFA} \equiv \text{NFA}$$

Für jede Sprache $L \subseteq \Sigma^*$ sind äquivalent:
1. $L$ wird von einem DFA erkannt
2. $L$ wird von einem NFA erkannt
3. $L$ wird von einem regulären Ausdruck beschrieben

### Konversionsrichtungen

| Von → Nach | Verfahren |
|---|---|
| Regex → NFA | **Thompson's Construction**: Induktiver Aufbau mit $\varepsilon$-Übergängen |
| NFA → DFA | [[Nichtdeterministische Endliche Automaten\|Potenzmengenkonstruktion]] |
| DFA → Regex | **Zustandselimination**: Schrittweises Entfernen von Zuständen mit Regex-Beschriftung |

## Algebraische Gesetze

| Gesetz | Regel |
|---|---|
| Kommutativität | $r + s = s + r$ |
| Assoziativität | $(r + s) + t = r + (s + t)$; $(r \cdot s) \cdot t = r \cdot (s \cdot t)$ |
| Neutrales Element | $r + \emptyset = r$; $r \cdot \varepsilon = \varepsilon \cdot r = r$ |
| Annihilation | $r \cdot \emptyset = \emptyset$ |
| Idempotenz | $r + r = r$ |
| Stern-Gesetze | $\varepsilon + r \cdot r^* = r^*$; $(\varepsilon + r)^* = r^*$; $(r^*)^* = r^*$ |

## Related Concepts

- [[Deterministische Endliche Automaten]]: Äquivalentes Berechnungsmodell
- [[Nichtdeterministische Endliche Automaten]]: Thompson's Construction erzeugt NFA aus Regex
- [[Formale Sprachen]]: Reguläre Ausdrücke beschreiben Typ-3-Sprachen
- [[Pumping-Lemma]]: Nachweis, dass eine Sprache nicht durch Regex beschreibbar ist
