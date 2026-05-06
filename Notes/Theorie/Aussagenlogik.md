---
title: Aussagenlogik
aliases:
  - Propositional Logic
  - AL
  - Aussagenlogische Formel
  - Wahrheitstafel
  - Erfüllbarkeit
  - Tautologie
tags:
  - automaten
  - logik
description: "Aussagenlogik (AL) — Syntax, Semantik, Belegungen, Wahrheitstafeln, Erfüllbarkeit, Allgemeingültigkeit und Normalformen (KNF/DNF)."
draft: false
---

Die **Aussagenlogik** (AL, Propositional Logic) ist die Grundlage der formalen Logik. Sie untersucht die Wahrheitswerte zusammengesetzter Aussagen, die durch logische Verknüpfungen (Junktoren) gebildet werden.

## Syntax

### Aussagenlogische Formeln

Formeln werden induktiv aufgebaut über einer Menge von **Aussagenvariablen** $\mathcal{V} = \{p_0, p_1, p_2, \ldots\}$:

| Formeltyp | Notation |
|---|---|
| **Atomare Formel** | $p_i \in \mathcal{V}$ |
| **Negation** | $\neg \varphi$ |
| **Konjunktion** | $\varphi \wedge \psi$ |
| **Disjunktion** | $\varphi \vee \psi$ |
| **Implikation** | $\varphi \to \psi$ |
| **Bikonditional** | $\varphi \leftrightarrow \psi$ |
| **Konstanten** | $\top$ (wahr), $\bot$ (falsch) |

**Bindungsstärke** (absteigend): $\neg > \wedge > \vee > \to > \leftrightarrow$

## Semantik

### Belegung (Interpretation)

Eine **Belegung** $\mathcal{I}: \mathcal{V} \to \{0, 1\}$ weist jeder Aussagenvariablen einen Wahrheitswert zu. Die Auswertung einer Formel $\varphi$ unter $\mathcal{I}$ wird induktiv definiert:

| Formel | $\text{val}_\mathcal{I}(\cdot)$ |
|---|---|
| $p_i$ | $\mathcal{I}(p_i)$ |
| $\neg \varphi$ | $1 - \text{val}_\mathcal{I}(\varphi)$ |
| $\varphi \wedge \psi$ | $\min(\text{val}_\mathcal{I}(\varphi), \text{val}_\mathcal{I}(\psi))$ |
| $\varphi \vee \psi$ | $\max(\text{val}_\mathcal{I}(\varphi), \text{val}_\mathcal{I}(\psi))$ |
| $\varphi \to \psi$ | $0$ nur wenn $\text{val}_\mathcal{I}(\varphi) = 1$ und $\text{val}_\mathcal{I}(\psi) = 0$ |
| $\varphi \leftrightarrow \psi$ | $1$ gdw. $\text{val}_\mathcal{I}(\varphi) = \text{val}_\mathcal{I}(\psi)$ |

### Wahrheitstafel

Systematische Auflistung aller $2^n$ Belegungen für $n$ Variablen mit resultierendem Wahrheitswert der Formel.

## Semantische Grundbegriffe

| Begriff | Definition | Notation |
|---|---|---|
| **Erfüllbar** | $\exists$ Belegung $\mathcal{I}$: $\text{val}_\mathcal{I}(\varphi) = 1$ | |
| **Unerfüllbar** | Keine Belegung erfüllt $\varphi$ | |
| **Allgemeingültig** (Tautologie) | Jede Belegung erfüllt $\varphi$ | $\models \varphi$ |
| **Folgerung** | Jedes Modell von $\Phi$ ist Modell von $\psi$ | $\Phi \models \psi$ |
| **Äquivalenz** | $\varphi \models \psi$ und $\psi \models \varphi$ | $\varphi \equiv \psi$ |

> [!IMPORTANT]
> **Zusammenhang**: $\varphi$ ist allgemeingültig $\Leftrightarrow$ $\neg\varphi$ ist unerfüllbar. Und $\Phi \models \psi$ $\Leftrightarrow$ $\Phi \cup \{\neg\psi\}$ ist unerfüllbar.

## Wichtige Äquivalenzen

| Name | Äquivalenz |
|---|---|
| De Morgan | $\neg(\varphi \wedge \psi) \equiv \neg\varphi \vee \neg\psi$; $\neg(\varphi \vee \psi) \equiv \neg\varphi \wedge \neg\psi$ |
| Implikation | $\varphi \to \psi \equiv \neg\varphi \vee \psi$ |
| Kontraposition | $\varphi \to \psi \equiv \neg\psi \to \neg\varphi$ |
| Doppelte Negation | $\neg\neg\varphi \equiv \varphi$ |
| Distributivität | $\varphi \wedge (\psi \vee \chi) \equiv (\varphi \wedge \psi) \vee (\varphi \wedge \chi)$ |
| Absorption | $\varphi \wedge (\varphi \vee \psi) \equiv \varphi$ |

## Normalformen

### Konjunktive Normalform (KNF / CNF)

Konjunktion von **Klauseln** (Disjunktionen von Literalen):

$$\varphi_{KNF} = \bigwedge_{i} \left(\bigvee_{j} l_{ij}\right)$$

### Disjunktive Normalform (DNF)

Disjunktion von **Konjunktionstermen** (Konjunktionen von Literalen):

$$\varphi_{DNF} = \bigvee_{i} \left(\bigwedge_{j} l_{ij}\right)$$

> [!NOTE]
> Jede Formel kann in eine äquivalente KNF und DNF umgewandelt werden. Die Umwandlung kann jedoch zu **exponentiellem Wachstum** führen.

### Umwandlung in KNF

1. Implikationen/Bikonditionale eliminieren
2. Negationen nach innen schieben (De Morgan, doppelte Negation)
3. Distributivgesetz anwenden ($\vee$ über $\wedge$ verteilen)

## Kompaktheitssatz

> Eine (möglicherweise unendliche) Formelmenge $\Phi$ ist erfüllbar $\Longleftrightarrow$ jede **endliche** Teilmenge von $\Phi$ ist erfüllbar.

Der Kompaktheitssatz ist ein zentrales Werkzeug der mathematischen Logik.

## Entscheidbarkeit

Die Aussagenlogik ist **entscheidbar**: Erfüllbarkeit, Allgemeingültigkeit und Folgerung können algorithmisch entschieden werden (z. B. per Wahrheitstafel). Allerdings ist SAT (Erfüllbarkeitsproblem) **NP-vollständig**.

## Related Concepts

- [[Resolutionskalkül]]: Beweisverfahren für Unerfüllbarkeit in KNF
- [[Sequenzenkalkül]]: Formales Beweissystem für Allgemeingültigkeit
- [[Prädikatenlogik]]: Erweiterung um Quantoren und Strukturen
- [[Normalformen]]: DNF/KNF in der Digitaltechnik
