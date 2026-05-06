---
title: Normalformen der Prädikatenlogik
aliases:
  - Pränexe Normalform
  - Prenex Normal Form
  - Skolemisierung
  - Skolem Normal Form
  - Herbrand-Universum
  - Herbrand
  - Herbrandnormalform
tags:
  - automaten
  - logik
description: "Normalformen der Prädikatenlogik — Pränexe Normalform, Skolemisierung (Eliminierung von Existenzquantoren), Herbrand-Universum und Satz von Herbrand."
draft: false
---

Die **Normalformen der Prädikatenlogik** transformieren [[Prädikatenlogik|PL1-Formeln]] in standardisierte Formen, die als Eingabe für automatische Beweisverfahren wie den [[Resolutionskalkül]] dienen.

## Pränexe Normalform (PNF)

Eine Formel ist in **pränexer Normalform**, wenn alle Quantoren **vorne** stehen:

$$Q_1 x_1\, Q_2 x_2\, \ldots Q_n x_n\, \varphi_0$$

wobei $Q_i \in \{\forall, \exists\}$ und $\varphi_0$ **quantorenfrei** ist (die **Matrix**).

### Umwandlung in PNF

1. **Implikationen/Bikonditionale** eliminieren
2. **Negationen** nach innen schieben (De Morgan, $\neg\forall x\,\varphi \equiv \exists x\,\neg\varphi$, $\neg\exists x\,\varphi \equiv \forall x\,\neg\varphi$)
3. **Variablen umbenennen**, um Namenskonflikte zu vermeiden
4. **Quantoren** nach vorne ziehen

> [!NOTE]
> Die Umformung in PNF erhält die logische **Äquivalenz** — die Formel hat dieselben Modelle.

## Skolemisierung

Die **Skolemisierung** eliminiert alle **Existenzquantoren**, indem sie durch **Skolem-Funktionen** ersetzt werden:

### Verfahren

Für eine PNF-Formel $\forall x_1 \ldots \forall x_k\, \exists y\, \varphi$:
- Ersetze $y$ durch $f(x_1, \ldots, x_k)$, wobei $f$ ein **neues** Funktionssymbol ist
- Die Argumente von $f$ sind genau die **vorangehenden Allquantor-Variablen**

| Formel | Skolemisiert |
|---|---|
| $\exists x\, P(x)$ | $P(c)$ (Skolem-**Konstante**) |
| $\forall x\, \exists y\, R(x,y)$ | $\forall x\, R(x, f(x))$ |
| $\forall x\, \forall y\, \exists z\, S(x,y,z)$ | $\forall x\, \forall y\, S(x, y, g(x,y))$ |

> [!IMPORTANT]
> Die Skolemisierung erhält **nicht** die logische Äquivalenz, sondern nur die **Erfüllbarkeitsäquivalenz**: $\varphi$ ist erfüllbar $\Longleftrightarrow$ $\varphi_S$ (skolemisiert) ist erfüllbar.

### Skolemnormalform

Eine Formel in **Skolemnormalform** ist:
$$\forall x_1 \ldots \forall x_n\, \varphi_0$$
wobei $\varphi_0$ quantorenfrei und in KNF ist. Dies ist die Standardeingabe für den Resolutionskalkül.

## Herbrand-Universum

Das **Herbrand-Universum** $D(\sigma)$ einer Signatur $\sigma$ ist die Menge aller **variablenfreien Terme** (Grundterme), die aus den Funktions- und Konstantensymbolen von $\sigma$ gebildet werden können:

1. Alle Konstantensymbole $c_i \in D(\sigma)$
2. Gibt es keine Konstante, füge ein neues Symbol $a$ hinzu
3. Wenn $t_1, \ldots, t_n \in D(\sigma)$ und $f$ ein $n$-stelliges Funktionssymbol: $f(t_1, \ldots, t_n) \in D(\sigma)$

**Beispiel**: $\sigma = \{c, f^1\}$ → $D(\sigma) = \{c, f(c), f(f(c)), f(f(f(c))), \ldots\}$

### Herbrand-Struktur

Eine **Herbrand-Struktur** $\mathfrak{H}$ hat:
- Trägermenge $= D(\sigma)$ (die Grundterme selbst)
- Jeder Term wird **als er selbst** interpretiert: $c^{\mathfrak{H}} = c$, $f^{\mathfrak{H}}(t_1,\ldots,t_n) = f(t_1,\ldots,t_n)$
- Nur die **Relationen** müssen interpretiert werden

## Satz von Herbrand

> Eine Formelmenge $\Phi$ in Skolemnormalform ist **unerfüllbar** $\Longleftrightarrow$ eine **endliche** Menge von Grundinstanzen von $\Phi$ ist (aussagenlogisch) unerfüllbar.

### Bedeutung

Der Satz reduziert die **prädikatenlogische** Unerfüllbarkeit auf **aussagenlogische** Unerfüllbarkeit:

1. Erzeuge systematisch Grundinstanzen (Substitution aller Variablen durch Grundterme)
2. Prüfe die Grundinstanzen auf aussagenlogische Unerfüllbarkeit

> [!NOTE]
> Der Satz von Herbrand liefert ein **Semi-Entscheidungsverfahren** für Unerfüllbarkeit: Wenn die Formel unerfüllbar ist, wird dies nach endlich vielen Schritten erkannt. Wenn sie erfüllbar ist, terminiert das Verfahren möglicherweise nicht.

## Pipeline: Formel → Resolution

$$\text{PL1-Formel} \xrightarrow{\text{PNF}} \text{Pränex} \xrightarrow{\text{Skolem}} \text{Skolemnormalform} \xrightarrow{\text{KNF}} \text{Klauselmenge} \xrightarrow{\text{Resolution}} \square\,?$$

## Related Concepts

- [[Prädikatenlogik]]: Grundlage der Normalformen
- [[Resolutionskalkül]]: Verwendet Skolemnormalform als Eingabe
- [[Aussagenlogik]]: Herbrand reduziert PL1 auf AL
