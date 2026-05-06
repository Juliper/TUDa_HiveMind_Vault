---
title: Prädikatenlogik
aliases:
  - First-Order Logic
  - PL1
  - Prädikatenlogik erster Stufe
  - FO
  - Quantoren
  - Struktur
tags:
  - automaten
  - logik
description: "Prädikatenlogik erster Stufe (PL1/FO) — Syntax (Terme, Formeln, Quantoren), Semantik (Strukturen, Interpretationen, Variablenbelegungen) und Modellbegriff."
draft: false
---

Die **Prädikatenlogik erster Stufe** (PL1, First-Order Logic, FO) erweitert die [[Aussagenlogik]] um **Quantoren** ($\forall$, $\exists$), **Variablen**, **Funktionen** und **Relationen**. Sie ermöglicht Aussagen über Objekte und deren Eigenschaften.

## Signatur

Eine **Signatur** $\sigma = (R_1^{a_1}, \ldots, R_k^{a_k}, f_1^{b_1}, \ldots, f_m^{b_m}, c_1, \ldots, c_l)$ legt fest:

| Symbole | Bedeutung |
|---|---|
| **Relationssymbole** $R_i$ | Mit Stelligkeit $a_i$ (z. B. $<$ ist 2-stellig) |
| **Funktionssymbole** $f_j$ | Mit Stelligkeit $b_j$ (z. B. $+$ ist 2-stellig) |
| **Konstantensymbole** $c_k$ | Nullstellige Funktionen (z. B. $0$) |

## Syntax

### Terme

Terme werden induktiv definiert:
1. Jede **Variable** $x, y, z, \ldots$ ist ein Term
2. Jede **Konstante** $c$ ist ein Term
3. Ist $f$ ein $n$-stelliges Funktionssymbol und sind $t_1, \ldots, t_n$ Terme, so ist $f(t_1, \ldots, t_n)$ ein Term

### Formeln

| Formeltyp | Notation | Beschreibung |
|---|---|---|
| **Atomare Formel** | $R(t_1, \ldots, t_n)$ | Relation angewandt auf Terme |
| **Gleichheit** | $t_1 = t_2$ | Gleichheit von Termen |
| **Negation** | $\neg\varphi$ | |
| **Junktoren** | $\varphi \wedge \psi$, $\varphi \vee \psi$, $\varphi \to \psi$ | Wie in AL |
| **Universalquantor** | $\forall x\, \varphi$ | "Für alle $x$ gilt $\varphi$" |
| **Existenzquantor** | $\exists x\, \varphi$ | "Es gibt ein $x$, für das $\varphi$ gilt" |

### Freie und gebundene Variablen

| Begriff | Definition |
|---|---|
| **Gebunden** | $x$ steht im Wirkungsbereich eines Quantors $\forall x$ oder $\exists x$ |
| **Frei** | $x$ ist nicht gebunden |
| **Satz** (geschlossene Formel) | Formel ohne freie Variablen |

> [!IMPORTANT]
> Nur **Sätze** haben einen Wahrheitswert unabhängig von einer Variablenbelegung. Formeln mit freien Variablen benötigen eine Belegung.

## Semantik

### Struktur (Interpretation)

Eine **$\sigma$-Struktur** $\mathfrak{A} = (A, \cdot^{\mathfrak{A}})$ besteht aus:

| Komponente | Bedeutung |
|---|---|
| $A$ | **Trägermenge** (Universum, nichtleer) |
| $R_i^{\mathfrak{A}} \subseteq A^{a_i}$ | Interpretation der Relation $R_i$ |
| $f_j^{\mathfrak{A}}: A^{b_j} \to A$ | Interpretation der Funktion $f_j$ |
| $c_k^{\mathfrak{A}} \in A$ | Interpretation der Konstante $c_k$ |

### Variablenbelegung

Eine **Belegung** $\beta: \text{Var} \to A$ weist jeder Variablen ein Element der Trägermenge zu.

$\beta[x \mapsto a]$ ist die Belegung, die wie $\beta$ ist, außer dass $x$ auf $a$ abgebildet wird.

### Auswertung

Die **Termauswertung** $\text{val}_{\mathfrak{A},\beta}(t)$ berechnet den Wert eines Terms:
- $\text{val}_{\mathfrak{A},\beta}(x) = \beta(x)$
- $\text{val}_{\mathfrak{A},\beta}(c) = c^{\mathfrak{A}}$
- $\text{val}_{\mathfrak{A},\beta}(f(t_1,\ldots,t_n)) = f^{\mathfrak{A}}(\text{val}_{\mathfrak{A},\beta}(t_1),\ldots,\text{val}_{\mathfrak{A},\beta}(t_n))$

### Erfüllungsrelation

$\mathfrak{A}, \beta \models \varphi$ ("$\mathfrak{A}$ erfüllt $\varphi$ unter $\beta$"):

| Formel | Erfüllt gdw. |
|---|---|
| $R(t_1,\ldots,t_n)$ | $(\text{val}(t_1),\ldots,\text{val}(t_n)) \in R^{\mathfrak{A}}$ |
| $t_1 = t_2$ | $\text{val}(t_1) = \text{val}(t_2)$ |
| $\neg\varphi$ | $\mathfrak{A}, \beta \not\models \varphi$ |
| $\varphi \wedge \psi$ | $\mathfrak{A}, \beta \models \varphi$ und $\mathfrak{A}, \beta \models \psi$ |
| $\forall x\, \varphi$ | Für **alle** $a \in A$: $\mathfrak{A}, \beta[x \mapsto a] \models \varphi$ |
| $\exists x\, \varphi$ | Es existiert $a \in A$: $\mathfrak{A}, \beta[x \mapsto a] \models \varphi$ |

## Modellbegriff

| Begriff | Definition |
|---|---|
| **Modell** | $\mathfrak{A} \models \varphi$ gdw. für alle $\beta$: $\mathfrak{A}, \beta \models \varphi$ |
| **Erfüllbar** | $\exists$ Struktur $\mathfrak{A}$: $\mathfrak{A} \models \varphi$ |
| **Allgemeingültig** | Jede Struktur ist Modell |
| **Folgerung** | $\Phi \models \psi$: Jedes Modell von $\Phi$ ist Modell von $\psi$ |

## Entscheidbarkeit

> [!WARNING]
> Im Gegensatz zur [[Aussagenlogik]] ist die Prädikatenlogik **unentscheidbar**: Es gibt keinen Algorithmus, der für jede PL1-Formel entscheidet, ob sie allgemeingültig ist. Die Allgemeingültigkeit ist aber **semi-entscheidbar** (aufzählbar).

## Kompaktheitssatz (PL1)

> Eine (möglicherweise unendliche) Formelmenge $\Phi$ ist erfüllbar $\Longleftrightarrow$ jede endliche Teilmenge von $\Phi$ ist erfüllbar.

## Related Concepts

- [[Aussagenlogik]]: PL1 als Erweiterung der AL
- [[Normalformen der Prädikatenlogik]]: Pränexe NF, Skolemisierung, Herbrand
- [[Resolutionskalkül]]: Resolution mit Unifikation für PL1
- [[Sequenzenkalkül]]: Beweisverfahren mit Quantorenregeln
- [[Entscheidbarkeit und Berechenbarkeit]]: Unentscheidbarkeit der PL1
