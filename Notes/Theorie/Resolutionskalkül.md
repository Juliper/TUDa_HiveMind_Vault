---
title: Resolutionskalkül
aliases:
  - Resolution
  - Resolutionsverfahren
  - Resolution Procedure
  - Resolvente
  - Unifikation
tags:
  - automaten
  - logik
description: "Resolutionskalkül — Widerlegungsverfahren für Aussagenlogik (AL) und Prädikatenlogik (PL1) mit Klauselform, Resolutionsregel und Unifikation."
draft: false
---

Der **Resolutionskalkül** ist ein **Widerlegungsverfahren**: Um zu zeigen, dass eine Formel allgemeingültig ist ($\models \varphi$), zeigt man, dass $\neg\varphi$ **unerfüllbar** ist.

## Grundprinzip

$$\Phi \models \psi \quad\Longleftrightarrow\quad \Phi \cup \{\neg\psi\} \text{ ist unerfüllbar}$$

Unerfüllbarkeit wird durch systematische Ableitung der **leeren Klausel** $\square$ nachgewiesen.

## Aussagenlogische Resolution

### Klauselform

Eine **Klausel** ist eine Disjunktion von Literalen: $C = \{l_1, l_2, \ldots, l_k\}$

Eine Formelmenge in [[Aussagenlogik|KNF]] wird als **Klauselmenge** dargestellt:

$$\varphi = (p \vee \neg q) \wedge (q \vee r) \quad\longrightarrow\quad \{\{p, \neg q\},\; \{q, r\}\}$$

### Resolutionsregel

Aus zwei Klauseln mit **komplementären Literalen** wird eine neue Klausel (Resolvente) abgeleitet:

$$\frac{C_1 = \{l\} \cup C_1' \qquad C_2 = \{\neg l\} \cup C_2'}{C_1' \cup C_2'} \quad \text{(Resolvente)}$$

> [!IMPORTANT]
> Pro Resolutionsschritt wird **genau ein** komplementäres Literal aufgelöst.

### Algorithmus

1. Negiere die zu beweisende Formel
2. Überführe in KNF / Klauselmenge
3. Wende Resolutionsregel wiederholt an
4. Falls $\square$ (leere Klausel) abgeleitet → **unerfüllbar** (Beweis erfolgreich)
5. Falls keine neuen Resolventen möglich → **erfüllbar**

### Korrektheit und Vollständigkeit

| Eigenschaft | Aussage |
|---|---|
| **Korrekt** (sound) | Wenn $\square$ ableitbar, dann tatsächlich unerfüllbar |
| **Vollständig** (complete) | Wenn unerfüllbar, dann ist $\square$ ableitbar |

## Prädikatenlogische Resolution

Für die [[Prädikatenlogik]] muss die Resolution um **Unifikation** erweitert werden.

### Vorbereitung

1. **Pränexe Normalform**: Alle Quantoren nach vorne
2. **Skolemisierung**: $\exists$-Quantoren durch Skolem-Funktionen ersetzen (siehe [[Normalformen der Prädikatenlogik]])
3. **Klauselform**: KNF des quantorenfreien Teils bilden
4. **Variablen standardisieren**: Verschiedene Klauseln verwenden verschiedene Variablen

### Unifikation

Ein **Unifikator** $\sigma$ für zwei Terme/Atome $s, t$ ist eine Substitution mit $s\sigma = t\sigma$.

Der **allgemeinste Unifikator** (mgu, most general unifier) ist der Unifikator, aus dem alle anderen durch weitere Substitution hervorgehen.

**Unifikationsalgorithmus**:
1. Finde die erste Unterschiedsstelle (disagreement pair) $(s_i, t_i)$
2. Wenn einer eine Variable $x$ ist und $x$ nicht in dem anderen Term vorkommt (**Occurs-Check**): Substituiere $x \mapsto t_i$
3. Wiederhole bis Gleichheit oder Fehler

> [!WARNING]
> Der **Occurs-Check** ist essenziell: $x$ und $f(x)$ sind **nicht** unifizierbar, da $x \mapsto f(x)$ zu einem unendlichen Term führen würde.

### Prädikatenlogische Resolutionsregel

$$\frac{\{P(\vec{s})\} \cup C_1 \qquad \{\neg P(\vec{t})\} \cup C_2}{(C_1 \cup C_2)\sigma} \quad \text{wobei } \sigma = \text{mgu}(P(\vec{s}), P(\vec{t}))$$

### Korrektheit und Vollständigkeit (PL1)

| Eigenschaft | Aussage |
|---|---|
| **Korrekt** | Wenn $\square$ ableitbar, dann unerfüllbar |
| **Vollständig** | Wenn unerfüllbar, dann ist $\square$ ableitbar (Satz von Robinson) |

> [!NOTE]
> Da die Prädikatenlogik **unentscheidbar** ist, kann das Resolutionsverfahren bei erfüllbaren Formelmengen **nicht terminieren** (kein Entscheidungsverfahren, nur Semi-Entscheidungsverfahren).

## Beispiel (AL)

Zeige: $\{p \to q,\; q \to r\} \models p \to r$

1. Negation: $p \to q,\; q \to r,\; \neg(p \to r) \equiv p \to q,\; q \to r,\; p,\; \neg r$
2. Klauseln: $\{\neg p, q\},\; \{\neg q, r\},\; \{p\},\; \{\neg r\}$
3. Resolution:
   - $\{\neg p, q\}$ und $\{\neg q, r\}$ → $\{\neg p, r\}$
   - $\{\neg p, r\}$ und $\{\neg r\}$ → $\{\neg p\}$
   - $\{\neg p\}$ und $\{p\}$ → $\square$

## Related Concepts

- [[Aussagenlogik]]: KNF als Eingabeformat für aussagenlogische Resolution
- [[Prädikatenlogik]]: Erweiterung mit Unifikation für PL1-Resolution
- [[Normalformen der Prädikatenlogik]]: Skolemisierung als Vorbereitung
- [[Sequenzenkalkül]]: Alternatives Beweisverfahren
