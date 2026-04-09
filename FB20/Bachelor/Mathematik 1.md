---
title: Mathematik 1
aliases:
  - "Mathe 1"
tags:
  - fb20
  - bachelor
  - pflichtmodul
  - semester-1
description: Grundlagen der Mathematik für Informatiker — Logik, Mengenlehre, algebraische Strukturen, Lineare Algebra und Analysis (Konvergenz).
cp: 9
pruefungsform: Klausur
modultyp: Pflichtmodul
wahlbereich: 
dozent: Robert Haller-Dintelmann
studiengang: Bachelor Informatik
semester: 1
status: vollständig
---
# Mathematik 1

## Überblick

> Mathematik 1 legt die formalen Grundlagen für das Informatikstudium. Die Vorlesung führt in die mathematische Sprache (Logik, Mengen, Beweise) ein, behandelt algebraische Strukturen (Gruppen, Ringe, Körper) mit Anwendung in der Kryptographie, deckt die Lineare Algebra vollständig ab und beginnt die Analysis mit Konvergenz von Folgen.
>
> **Vorkenntnisse:** Schulwissen Mathematik (Gymnasium). Keine Programmierkenntnisse nötig.

## Kerninhalte

- **Grundbegriffe:** Aussagen & Logik (inkl. logische Vollständigkeit/NOR), Mengen & Mengenoperationen, Supremum/Infimum, Relationen (Ordnung, Äquivalenz), Abbildungen (injektiv/surjektiv/bijektiv, Bilder/Urbilder), Beweismethoden, Intervalle in ℝ
- **Algebraische Strukturen:** Modulare Arithmetik, lineare Kongruenzgleichungen, Euklidischer Algorithmus, RSA-Verschlüsselung, Gruppen (direktes Produkt, Kern, Injektivität), Ringe & Körper, komplexe Zahlen (Polarform, $n$-te Einheitswurzeln), Körperhomomorphismen
- **Lineare Algebra:** Vektorräume, Normen & Skalarprodukt, ONB & Orthogonalprojektion, Basen & Dimension, lineare Abbildungen (Kern/Bild, Faktorraum), Matrizen & Basiswechsel, LGS (Gauß), Determinanten, Eigenwerttheorie, orthogonale Matrizen, Geometrie (Kreuzprodukt, Hesse-Normalform)
- **Universelle Algebra:** Signaturen, Σ-Algebren, Homomorphismen, Terminduktion *(kurzer Ausblick)*
- **Analysis I:** Reelle Zahlen & Vollständigkeitsaxiom, Betrag & Dreiecksungleichung, Folgen & Konvergenz (ε-n₀-Technik), Konvergenzkriterien, Häufungswerte & Teilfolgen, Sandwich-Theorem, Grenzwerte rationaler Folgen, Landau-Notation, rekursive Folgen

## Zusammenfassung

### 1. Grundbegriffe

#### Aussagen & Logik
Eine **Aussage** ist ein Satz, der wahr (w) oder falsch (f) ist. Eine **Aussageform** $E(x)$ wird durch Einsetzen einer konkreten Belegung zur Aussage.

Verknüpfungen: $A \wedge B$ (und), $A \vee B$ (oder), $\neg A$ (nicht), $A \Rightarrow B$ (wenn…dann), $A \Leftrightarrow B$ (genau dann wenn).

**Wichtig:** $A \Rightarrow B$ ist auch wahr, wenn $A$ falsch ist ("aus Falschem folgt Beliebiges").

Quantoren: $\forall x \in M: E(x)$ (Allquantor), $\exists x \in M: E(x)$ (Existenzquantor).

**Logische Vollständigkeit:** Eine Menge von Junktoren heißt *funktional vollständig*, wenn sich jede boolesche Funktion damit ausdrücken lässt. $\{\neg, \wedge\}$ und $\{\neg, \vee\}$ sind vollständig. Der **NOR-Operator** $A \downarrow B := \neg(A \vee B)$ ist alleine vollständig: $\neg A = A \downarrow A$ und $A \vee B = (A \downarrow B) \downarrow (A \downarrow B)$.

#### Mengen
Operationen auf Mengen $M, N$ in Grundmenge $G$:
- $M \cup N$ (Vereinigung), $M \cap N$ (Schnitt), $M^c$ (Komplement), $M \setminus N$ (Differenz), $M \times N$ (kartesisches Produkt)

**Beziehungen:** $M \subseteq N$ gilt, wenn jedes Element von $M$ in $N$ enthalten ist.
**Wichtig:** Es gilt $M = N$, wenn $M \subseteq N \land N \subseteq M$

**Satz (De Morgan):** $(A \cup B)^c = A^c \cap B^c$ und $(A \cap B)^c = A^c \cup B^c$

**Potenzmenge:** $\mathcal{P}(M) = \{N : N \subseteq M\}$, es gilt $|\mathcal{P}(M)| = 2^{|M|}$.

**Supremum und Infimum:** Für $M \subseteq \mathbb{R}$ ist $\sup M$ die *kleinste obere Schranke*, $\inf M$ die *größte untere Schranke*. $\max M$ (bzw. $\min M$) existiert nur, wenn das Supremum (Infimum) in $M$ liegt.

Für zwei nichtleere Mengen $C, D$: $\sup(C \cup D) = \max(\sup C, \sup D)$ und $\inf(C \cup D) = \min(\inf C, \inf D)$.

#### Relationen
Eine **Relation** $R \subseteq X \times X$ heißt:
- *reflexiv* ($xRx$), *symmetrisch* ($xRy \Rightarrow yRx$), *antisymmetrisch*, *transitiv*
- **Äquivalenzrelation**: reflexiv + symmetrisch + transitiv → erzeugt Äquivalenzklassen $\tilde{a} = \{x : x \sim a\}$
- **Ordnungsrelation**: reflexiv + antisymmetrisch + transitiv → partiell/total geordnete Menge

#### Abbildungen
$f: A \to B$ heißt:
- **injektiv**: $f(x) = f(y) \Rightarrow x = y$
- **surjektiv**: $f(A) = B$
- **bijektiv**: injektiv und surjektiv → Umkehrabbildung $f^{-1}$ existiert
![[pasted-image-20231024165003.png|800]]
**Bilder und Urbilder:**
- Bild: $f(S) = \{f(x) : x \in S\}$; Urbild: $f^{-1}(T) = \{x \in A : f(x) \in T\}$
- Allgemein: $f^{-1}(f(S)) \supseteq S$ und $f(f^{-1}(T)) \subseteq T$
- $f$ injektiv $\Leftrightarrow$ $f^{-1}(f(S)) = S$ für alle $S \subseteq A$
- $f$ surjektiv $\Leftrightarrow$ $f(f^{-1}(T)) = T$ für alle $T \subseteq B$

#### Intervalle
Eine Teilmenge $I \subseteq \mathbb{R}$ heißt **Intervall**, falls für alle $x, z \in I$ mit $x \leq z$ gilt: $x \leq y \leq z \Rightarrow y \in I$.

In $\mathbb{R}$ gibt es genau die folgenden Typen (mit $a, b \in \mathbb{R}$):
$$[a,b],\quad [a,b),\quad (a,b],\quad (a,b),\quad [a,\infty),\quad (a,\infty),\quad (-\infty,b],\quad (-\infty,b)$$

**Satz:** Der Schnitt zweier Intervalle ist wieder ein Intervall.

#### Beweisprinzipien
| Methode | Vorgehen |
|---|---|
| Direkter Beweis | $A$ annehmen → $B$ folgern |
| Kontraposition | $\neg B$ annehmen → $\neg A$ zeigen |
| Widerspruch | $A \wedge \neg B$ annehmen → Widerspruch herleiten |
| Vollständige Induktion | Induktionsanfang + Induktionsschritt ($E(n) \Rightarrow E(n+1)$) |

---

### 2. Algebraische Strukturen: Gruppen, Ringe, Körper

#### Modulare Arithmetik
**Division mit Rest:** Zu $a \in \mathbb{Z}$, $b \in \mathbb{N}^*$ gibt es eindeutige $q \in \mathbb{Z}$, $r \in \{0,\ldots,b-1\}$ mit $a = q \cdot b + r$. Schreibweise: $r = a \bmod b$.

Rechenregel: $(a + b) \bmod n = ((a \bmod n) + (b \bmod n)) \bmod n$ (analog für Multiplikation und Potenz).

**Lineare Kongruenzgleichungen:** Die Gleichung $mx \equiv k \pmod{n}$ besitzt eine Lösung $x \in \mathbb{Z}$ genau dann, wenn $\gcd(m,n) \mid k$. Die Anzahl der Lösungen modulo $n$ ist dann genau $\gcd(m,n)$. Lösung via erweitertem Euklid.

**Teilbarkeit durch 11:** Eine ganze Zahl ist durch 11 teilbar $\Leftrightarrow$ ihre alternierende Quersumme (Ziffern von rechts abwechselnd addiert/subtrahiert) durch 11 teilbar ist.

#### Euklidischer Algorithmus
$\gcd(a, b) = \gcd(b, a \bmod b)$

```
Euklid(a, b):
  IF b = 0 THEN return a
  ELSE return Euklid(b, a mod b)
```

**Erweiterter Euklid:** Liefert zusätzlich $k, \ell \in \mathbb{Z}$ mit $d = \gcd(a,b) = ka + \ell b$.

#### Kleiner Satz von Fermat
Für jede Primzahl $p$ und $a \in \mathbb{N}$: $a^p \equiv a \pmod{p}$.

Korollar: Ist $p \nmid a$, so gilt $a^{p-1} \equiv 1 \pmod{p}$.

#### RSA-Verschlüsselung
Alice wählt zwei große Primzahlen $p, q$, berechnet $n = pq$ und $N = (p-1)(q-1)$. Wählt $e$ mit $\gcd(e, N) = 1$ und bestimmt $x$ mit $ex \equiv 1 \pmod{N}$. Public Key: $(n, e)$, Private Key: $(n, x)$.

Verschlüsseln: $M' = M^e \bmod n$. Entschlüsseln: $M'' = (M')^x \bmod n = M$.

#### Gruppen
Eine **Gruppe** $(G, *)$ erfüllt: Assoziativität, neutrales Element, inverses Element. Gilt zusätzlich Kommutativität, heißt sie **abelsch**.

Beispiele: $(\mathbb{Z}, +)$, $(\mathbb{Q} \setminus \{0\}, \cdot)$, Permutationsgruppen, $(\mathbb{Z}_n, +)$.

**Untergruppenkriterium:** $U \subseteq G$ ist Untergruppe $\Leftrightarrow$ $U \neq \emptyset$ und $\forall a, b \in U: a * b^{-1} \in U$.

**Direktes Produkt:** Für Gruppen $(G_1, *_1)$ und $(G_2, *_2)$ ist $G_1 \times G_2$ mit komponentenweiser Verknüpfung $(g_1, g_2) * (h_1, h_2) = (g_1 *_1 h_1,\ g_2 *_2 h_2)$ wieder eine Gruppe.

**Gruppenhomomorphismus:** $f: G \to H$ mit $f(g_1 * g_2) = f(g_1) \diamond f(g_2)$. Bijektiver Homomorphismus = Isomorphismus.

**Kern und Injektivität:** $\ker(f) = \{g \in G : f(g) = n_H\}$ ist eine Untergruppe von $G$.
$$f \text{ injektiv} \Leftrightarrow \ker(f) = \{n_G\}$$

#### Ringe und Körper
Ein **Ring** $(R, +, \cdot)$ ist eine abelsche Gruppe bzgl. $+$ mit assoziativer Multiplikation und Distributivgesetzen.

**Rechenregeln in Ringen:** Für alle $a, b \in R$: $0 \cdot a = 0$, $(-a) \cdot b = -(ab)$, $(-a)(-b) = ab$.

Ein **Körper** ist ein kommutativer Ring, in dem jedes Element $\neq 0$ ein multiplikatives Inverses hat. Beispiele: $\mathbb{Q}, \mathbb{R}, \mathbb{C}, \mathbb{Z}_p$ (für Primzahl $p$).

**Körperhomomorphismus:** Ein Ringhomomorphismus $f: K \to L$ zwischen Körpern ist entweder $f \equiv 0$ oder injektiv (Körper haben nur triviale Ideale).

#### Komplexe Zahlen
$\mathbb{C} = \{a + bi : a, b \in \mathbb{R}\}$ mit $i^2 = -1$.

- **Betrag:** $|z| = \sqrt{a^2 + b^2}$; **Konjugat:** $\bar{z} = a - bi$, es gilt $z \cdot \bar{z} = |z|^2$
- **Polardarstellung:** $z = r \cdot e^{i\varphi}$ mit $r = |z|$, $\varphi = \arg(z)$
- **Multiplikation in Polarform:** $z_1 z_2 = r_1 r_2 \cdot e^{i(\varphi_1 + \varphi_2)}$
- **Quadratwurzeln in $\mathbb{C}$:** $\sqrt{z}$ existiert immer; berechnet via $r' = \sqrt{r}$, $\varphi' = \varphi/2$
- **Gleichungen in $\mathbb{C}$ lösen:** pq-Formel auch mit komplexen Termen unter der Wurzel anwendbar

**$n$-te Einheitswurzeln:** Die Lösungen von $z^n = 1$ sind
$$\omega_k = e^{2\pi i k/n}, \quad k = 0, 1, \ldots, n-1$$
Sie liegen gleichmäßig verteilt auf dem Einheitskreis $|z| = 1$.

---

### 3. Lineare Algebra

#### Vektorräume
Ein **Vektorraum** $(V, +, \cdot)$ über einem Körper $K$ erfüllt 8 Axiome (Kommutativität, Assoziativität, neutrales/inverses Element der Addition, Distributivgesetze, Skalarmultiplikation).

Wichtige Beispiele: $\mathbb{R}^n$, Polynomraum $\mathbb{R}[x]$ (Monome $1, x, x^2, \ldots$ bilden eine Basis), stetige Funktionen $C([a,b])$.

**Vektorraumaxiome prüfen:** Alle 8 Axiome systematisch überprüfen. Häufige Fallen: kein neutrales Element, Addition nicht abgeschlossen, Skalarmultiplikation verletzt Distributivgesetz.

#### Normen und Skalarprodukt
Auf $\mathbb{R}^n$:
- **$\ell^1$-Norm:** $\|v\|_1 = \sum_{i=1}^n |v_i|$
- **Euklidische Norm:** $\|v\|_2 = \sqrt{\sum_{i=1}^n v_i^2}$
- **Maximumsnorm:** $\|v\|_\infty = \max_i |v_i|$

Ein **Skalarprodukt** $\langle \cdot, \cdot \rangle: V \times V \to \mathbb{R}$ erfüllt: Symmetrie, Linearität im ersten Argument, positive Definitheit ($\langle v,v\rangle \geq 0$, Gleichheit $\Leftrightarrow v=0$). Induzierte Norm: $\|v\| = \sqrt{\langle v,v\rangle}$.

**Parallelogrammidentität:** $\|v + w\|^2 + \|v - w\|^2 = 2(\|v\|^2 + \|w\|^2)$

#### Orthogonalität und ONB
- $u, v$ **orthogonal**: $\langle u, v\rangle = 0$
- **Orthonormalbasis (ONB)**: Basis mit $\langle v_i, v_j\rangle = \delta_{ij}$
- **Orthogonalprojektion** von $v$ auf $u$: $\displaystyle\text{proj}_u v = \frac{\langle v, u\rangle}{\langle u, u\rangle}\, u$

#### Basis und Dimension
- Vektoren $v_1, \ldots, v_n$ heißen **linear unabhängig**, wenn $\alpha_1 v_1 + \cdots + \alpha_n v_n = 0 \Rightarrow \alpha_i = 0$.
- Eine **Basis** ist ein linear unabhängiges Erzeugendensystem.
- Die **Dimension** $\dim(V)$ ist die Anzahl der Basisvektoren (eindeutig bestimmt).

**Dimensionsformel:** $\dim(U_1 + U_2) = \dim(U_1) + \dim(U_2) - \dim(U_1 \cap U_2)$.

#### Lineare Abbildungen & Matrizen
$f: V \to W$ linear $\Leftrightarrow$ $f(u + v) = f(u) + f(v)$ und $f(\alpha v) = \alpha f(v)$.

Jede lineare Abbildung zwischen endlichdimensionalen Räumen ist durch eine **Matrix** darstellbar. Matrixmultiplikation entspricht Verkettung von Abbildungen.

**Rang-Nullitäts-Satz:** $\dim(\ker f) + \dim(\operatorname{Im} f) = \dim(V)$.

**Kern und Bild bestimmen:** Kern = Lösungsraum von $Ax = 0$ (via Gauß); Bild = Spann der Spalten von $A$ (Basis durch Gauß ermitteln, Pivotspalten auswählen).

**Faktorraum / Quotientenabbildung:** Zu $f: V \to W$ linear mit $U = \ker(f)$ ist die kanonische Abbildung $\bar{f}: V/U \to W$, $\bar{f}(v + U) = f(v)$, injektiv.

#### Geometrie: Ebenen und Kreuzprodukt
**Ebene in Parameterform:** $E = \{p + s \cdot u + t \cdot v : s, t \in \mathbb{R}\}$ mit Aufpunkt $p$, Richtungsvektoren $u, v$.

**Kreuzprodukt** in $\mathbb{R}^3$:
$$u \times v = \begin{pmatrix} u_2 v_3 - u_3 v_2 \\ u_3 v_1 - u_1 v_3 \\ u_1 v_2 - u_2 v_1 \end{pmatrix}$$
Eigenschaften: $u \times v = -(v \times u)$; $u \times v \perp u$ und $u \times v \perp v$; $\|u \times v\| = \|u\|\|v\|\sin\theta$.

**Hesse-Normalform:** $E: \langle n_0, x\rangle = d$ mit $\|n_0\| = 1$ (Einheitsnormalenvektor).

**Abstand Punkt–Ebene:** $d(q, E) = |\langle n_0, q\rangle - d|$

#### Lineare Gleichungssysteme
$Ax = b$ mit $A \in \mathbb{R}^{m \times n}$.

**Gauß-Algorithmus:** Durch elementare Zeilenumformungen auf Zeilenstufenform bringen. Lösbar $\Leftrightarrow$ $\operatorname{rg}(A) = \operatorname{rg}(A|b)$. Lösungsraum hat Dimension $n - \operatorname{rg}(A)$.

#### Matrizen: Rechnen und Inverse
**Matrizenprodukt** $AB$ definiert $\Leftrightarrow$ Spaltenzahl von $A$ = Zeilenzahl von $B$. Im Allgemeinen $AB \neq BA$.

**Potenzen:** $A^k \cdot A^m = A^{k+m}$; $(\lambda A)^m = \lambda^m A^m$; aber $(AB)^2 \neq A^2 B^2$ im Allgemeinen.

**Inverse einer $2 \times 2$-Matrix:**
$$A = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \implies A^{-1} = \frac{1}{ad - bc}\begin{pmatrix} d & -b \\ -c & a \end{pmatrix}$$
existiert genau wenn $\det(A) = ad - bc \neq 0$.

**Inverse allgemein:** Gauß auf $(A \mid I)$ anwenden → ergibt $(I \mid A^{-1})$.

#### Abbildungsmatrix und Basiswechsel
Zu $f: V \to W$ mit Basen $\mathcal{B} = (b_1,\ldots,b_n)$ von $V$ und $\mathcal{C} = (c_1,\ldots,c_m)$ von $W$:
- $j$-te Spalte von $M_\mathcal{C}^\mathcal{B}(f)$ = Koordinaten von $f(b_j)$ bzgl. $\mathcal{C}$

**Basiswechsel:** Sei $\mathcal{B}'$ eine weitere Basis von $V$, $T$ die Basiswechselmatrix (Spalten = Koordinaten von $\mathcal{B}$-Vektoren bzgl. $\mathcal{B}'$). Dann: $M_\mathcal{C}^{\mathcal{B}'}(f) = M_\mathcal{C}^\mathcal{B}(f) \cdot T^{-1}$.

#### Determinanten
$\det(A)$ für $A \in \mathbb{R}^{n \times n}$: Entwicklung nach Zeile/Spalte (Laplacescher Entwicklungssatz).

Wichtige Eigenschaften:
- $\det(AB) = \det(A)\det(B)$; $\det(A^T) = \det(A)$
- $\det(A^2) = \det(A)^2$; $\det(A^{-1}) = 1/\det(A)$
- $\det(kA) = k^n \det(A)$ für $A \in \mathbb{R}^{n \times n}$
- $A$ invertierbar $\Leftrightarrow$ $\det(A) \neq 0$
- $\det(A) = 0 \Leftrightarrow$ Zeilen oder Spalten linear abhängig

#### Eigenwerttheorie
$\lambda \in K$ heißt **Eigenwert** von $A$, wenn $Av = \lambda v$ für ein $v \neq 0$ (**Eigenvektor**).

Bestimmung: $\det(A - \lambda I) = 0$ (charakteristisches Polynom). Eigenraum zu $\lambda$: $\ker(A - \lambda I)$.

**Weitere Eigenschaften:**
- $\lambda$ EW von $A$ invertierbar $\Rightarrow$ $\lambda^{-1}$ ist EW von $A^{-1}$ (mit demselben EV)
- $\lambda$ EW von $A$ $\Rightarrow$ $\lambda^k$ ist EW von $A^k$
- $AB$ und $BA$ haben dieselben Eigenwerte (für quadratische $A, B$)
- Eigenwerte reeller Matrizen treten — falls komplex — in **konjugierten Paaren** auf: $\lambda$ EW $\Rightarrow$ $\bar{\lambda}$ EW

**Symmetrische Matrizen** über $\mathbb{R}$ haben nur reelle Eigenwerte und sind diagonalisierbar.

**Definitheit:**
- **positiv definit**: alle Eigenwerte $> 0$ (äquivalent: alle Hauptminoren $> 0$)
- **negativ definit**: alle Eigenwerte $< 0$
- **indefinit**: sowohl positive als auch negative Eigenwerte

#### Orthogonale Matrizen
$A \in \mathbb{R}^{n \times n}$ heißt **orthogonal**, wenn $A^T A = I$ (äquivalent: $A^{-1} = A^T$).

Charakterisierungen: Spalten bilden ONB; Zeilen bilden ONB; $A$ erhält das Skalarprodukt: $\langle Ax, Ay\rangle = \langle x, y\rangle$; $\det(A) = \pm 1$.

---

### 4. Analysis I: Konvergenz

#### Reelle Zahlen
$\mathbb{R}$ ist der kleinste angeordnete Körper, der $\mathbb{Z}$ enthält und das **Vollständigkeitsaxiom** erfüllt:

> Jede nichtleere, nach oben beschränkte Teilmenge besitzt ein Supremum.

$\mathbb{Q}$ erfüllt dieses Axiom nicht (z.B. hat $\{x \in \mathbb{Q} : x^2 < 2\}$ kein Supremum in $\mathbb{Q}$).

#### Betrag und Dreiecksungleichung
Für $a, b \in \mathbb{R}$:
- $|a \cdot b| = |a| \cdot |b|$
- $|a + b| \leq |a| + |b|$ (**Dreiecksungleichung**)
- $\big||a| - |b|\big| \leq |a - b|$ (folgt durch Anwenden der Dreiecksungleichung auf $|(a-b)+b|$)

**Betragsungleichungen lösen:** Fallunterscheidung nach Vorzeichen des Ausdrucks im Betrag.  
Beispiel: $|2x-3| > 5$ → Fall 1: $2x-3 > 5 \Rightarrow x > 4$; Fall 2: $2x-3 < -5 \Rightarrow x < -1$. Lösungsmenge: $(-\infty,-1) \cup (4,\infty)$.

#### Folgen und Konvergenz
Eine Folge $(a_n)$ **konvergiert** gegen $a \in \mathbb{K}$, wenn:
$$\forall \varepsilon > 0\ \exists n_0 \in \mathbb{N}\ \forall n \geq n_0: |a_n - a| < \varepsilon$$

**Negation (Divergenz gegen $a$):** $\exists \varepsilon > 0\ \forall n_0 \in \mathbb{N}\ \exists n \geq n_0: |a_n - a| \geq \varepsilon$

Schreibweise: $\lim_{n \to \infty} a_n = a$.

**Grenzwertsätze:** Für $a_n \to a$, $b_n \to b$:
- $a_n \pm b_n \to a \pm b$; $a_n \cdot b_n \to a \cdot b$; $a_n/b_n \to a/b$ (falls $b \neq 0$)
- $\lambda a_n \to \lambda a$; $(a_n)^k \to a^k$

**Konvergent + Divergent = Divergent:** Ist $(a_n)$ konvergent und $(b_n)$ divergent, so ist $(a_n + b_n)$ divergent.

**Sandwich-Theorem:** $a_n \leq c_n \leq b_n$ und $a_n, b_n \to a$ $\Rightarrow$ $c_n \to a$.

Beispielanwendungen:
- $\displaystyle\lim_{n\to\infty} \frac{(-1)^n}{n} = 0$, da $-\frac{1}{n} \leq \frac{(-1)^n}{n} \leq \frac{1}{n} \to 0$
- $\displaystyle\lim_{n\to\infty} \frac{n!}{n^n} = 0$, da $0 \leq \frac{n!}{n^n} = \frac{1}{n} \cdot \frac{2}{n} \cdots \frac{n}{n} \leq \frac{1}{n}$

Wichtige Grenzwerte: $\lim q^n = 0$ für $|q| < 1$; $\lim \sqrt[n]{c} = 1$; $e = \lim (1 + \frac{1}{n})^n$; $\lim \frac{1}{n} = 0$.

**Grenzwerte rationaler Folgen:** Zähler und Nenner durch die höchste auftretende Potenz dividieren, dann Grenzwertsätze:
$$\lim_{n\to\infty} \frac{n^4}{(3n^2+2n)^2} = \lim_{n\to\infty} \frac{1}{9 + \frac{12}{n} + \frac{4}{n^2}} = \frac{1}{9}$$

#### Konvergenzkriterien und Folgeneigenschaften
- **Monotone Konvergenz:** Jede monotone und beschränkte reelle Folge konvergiert.
- **Cauchy-Kriterium:** $(a_n)$ konvergiert $\Leftrightarrow$ $\forall \varepsilon > 0\ \exists n_0: |a_n - a_m| < \varepsilon$ für alle $n, m \geq n_0$.
- **Bolzano-Weierstraß:** Jede beschränkte Folge in $\mathbb{R}$ besitzt eine konvergente Teilfolge.

**Klassifikation von Folgen** (beschränkt/nicht beschränkt, monoton/nicht monoton, konvergent/divergent):

| beschränkt | monoton | konvergent | möglich? |
|---|---|---|---|
| ja | ja | ja | ja, z.B. $(1/n)$ |
| ja | ja | nein | **nein** (Satz: beschränkt+monoton → konvergent) |
| ja | nein | ja | ja, z.B. $((-1)^n/n)$ |
| ja | nein | nein | ja, z.B. $((-1)^n)$ |
| nein | ja | ja | **nein** (unbeschränkt → nicht konvergent) |
| nein | ja | nein | ja, z.B. $(\sqrt{n})$ |
| nein | nein | ja | **nein** |
| nein | nein | nein | ja, z.B. $((-1)^n \sqrt{n})$ |

#### Häufungswerte und Teilfolgen
$\alpha \in \mathbb{R}$ heißt **Häufungswert** von $(a_n)$, wenn es eine Teilfolge $(a_{n_k})$ gibt mit $a_{n_k} \to \alpha$.

- Jede Teilfolge einer konvergenten Folge konvergiert gegen denselben Grenzwert.
- Eine konvergente Folge hat **genau einen** Häufungswert (den Grenzwert).
- Hat eine Folge zwei verschiedene Häufungswerte, ist sie divergent.

Beispiel: $a_n = (-1)^n + \frac{1}{n}$ hat Häufungswerte $1$ und $-1$ (via Teilfolgen $a_{2k}$ und $a_{2k+1}$) und divergiert.

#### ε-$n_0$-Beweistechnik
1. $\varepsilon > 0$ beliebig vorgeben
2. $n_0$ in Abhängigkeit von $\varepsilon$ wählen (oft $n_0 = \lceil f(1/\varepsilon) \rceil$)
3. Für alle $n \geq n_0$ zeigen: $|a_n - a| < \varepsilon$

**Nützliche Tricks:**
- **Konjugat erweitern:** $\sqrt{n+1} - \sqrt{n} = \frac{1}{\sqrt{n+1}+\sqrt{n}} \leq \frac{1}{2\sqrt{n}}$, daher $n_0 = \lceil 1/(4\varepsilon^2)\rceil$
- **Abschätzen:** komplizierten Term durch einfacheren nach oben abschätzen
- **Divergenz zeigen:** festes $\varepsilon$ wählen, für beliebiges $n_0$ ein $n \geq n_0$ finden mit $|a_n - a| \geq \varepsilon$

#### Asymptotik und Landau-Notation
$f(n) \in O(g(n))$: $f$ wächst höchstens so schnell wie $g$, d.h. $(f/g)$ ist beschränkt.

Zeigen via Grenzwert: $b_n \in O(a_n) \Leftrightarrow (b_n/a_n)$ konvergiert (gegen einen endlichen Wert).

#### Rekursive Folgen
Konvergenz einer rekursiv definierten Folge zeigen:
1. Monotonie zeigen (Induktion oder Rechnung)
2. Beschränktheit zeigen
3. Grenzwert aus Rekursionsformel: $a = \lim a_{n+1} = \lim a_n$ einsetzen → Fixpunktgleichung lösen

**Babylonisches Wurzelziehen:** Für $x > 0$, $a_0 > 0$ konvergiert
$$a_{n+1} = \frac{1}{2}\!\left(a_n + \frac{x}{a_n}\right)$$
gegen $\sqrt{x}$. Die Folge ist ab $n \geq 1$ monoton fallend und durch $\sqrt{x}$ nach unten beschränkt.

---

### 5. Universelle Algebra *(Ausblick)*

Eine **Signatur** $\Sigma = (S, F, \text{ar})$ beschreibt Sorten, Funktionssymbole und ihre Stelligkeit. Eine **Σ-Algebra** interpretiert diese Symbole auf konkreten Mengen.

**Terminduktion:** Analogon der vollständigen Induktion für termerzeugte Algebren — wichtig für Korrektheitsnachweise über Datentypen in der Informatik.

---

## Prüfungsvorbereitung

**Häufige Klausurthemen:**

*Logik & Mengen:*
- NOR-Vollständigkeit begründen (alle Junktoren aus NOR konstruieren)
- Sup, Inf, Max, Min an konkreten Mengen bestimmen
- Bilder und Urbilder berechnen; Injektivität/Surjektivität nachweisen

*Algebraische Strukturen:*
- Beweise per vollständiger Induktion (inkl. Binomische Formel, $\sum_{k=0}^n \binom{n}{k} = 2^n$)
- ggT berechnen (Euklid-Schema), erweiterten Euklid anwenden
- Lineare Kongruenzgleichung $mx \equiv k \pmod{n}$ auf Lösbarkeit prüfen und lösen
- Gruppenaxiome prüfen; Untergruppe nachweisen; Kern bestimmen
- Direktes Produkt zweier Gruppen beschreiben und Eigenschaften zeigen
- Komplexe Zahlen: Betrag, Konjugat, Polarform, Einheitswurzeln berechnen
- Gleichungen in $\mathbb{C}$ lösen (pq-Formel mit Arithmetik in $\mathbb{C}$)

*Lineare Algebra:*
- Vektorraumaxiome für eine konkrete Struktur nachprüfen
- Normen $\|\cdot\|_1$, $\|\cdot\|_2$, $\|\cdot\|_\infty$ berechnen; Skalarprodukt-Axiome prüfen
- ONB angeben; Orthogonalprojektion berechnen
- Gauß-Algorithmus, LGS lösen, Lösungsraum vollständig angeben (Dimension + Basis)
- Kern und Bild einer linearen Abbildung bestimmen (Basis angeben)
- Abbildungsmatrix bzgl. verschiedener Basen berechnen; Basiswechsel durchführen
- Determinante berechnen (Laplace-Entwicklung nach Zeile oder Spalte)
- Determinanteneigenschaften ausnutzen: $\det(kA) = k^n\det(A)$, $\det(A^2) = \det(A)^2$
- Eigenwerte und Eigenvektoren bestimmen; Diagonalisierbarkeit prüfen
- Definitheit über Eigenwerte oder Hauptminoren bestimmen
- Orthogonale Matrizen erkennen; $A^{-1} = A^T$ anwenden
- Eigenwerte von $A^{-1}$, $A^k$; Zusammenhang EW von $AB$ und $BA$; konjugierte EW-Paare

*Analysis:*
- $\varepsilon$-$n_0$-Beweis für Konvergenz (direkt aus Definition)
- Divergenz zeigen (Negation der Konvergenz-Definition)
- Dreiecksungleichung beweisen und anwenden: $|a+b| \leq |a|+|b|$, $\big||a|-|b|\big| \leq |a-b|$
- Betragsungleichungen lösen via Fallunterscheidung; Lösungsmenge als Intervall angeben
- Folgen klassifizieren: beschränkt/monoton/konvergent; unmögliche Kombinationen kennen
- Grenzwerte rationaler Folgen via Kürzen durch höchste Potenz
- Sandwich-Theorem anwenden (geeignete obere und untere Schranken finden)
- Häufungswerte bestimmen; Teilfolgen-Argument
- Konvergenz rekursiver Folgen zeigen (Monotonie + Beschränktheit + Fixpunktgleichung)
- Landau-Notation: $f \in O(g)$ via Konvergenz von $f/g$ zeigen

**Wichtige Formeln:**
- Binomialformel: $(a+b)^n = \sum_{k=0}^n \binom{n}{k} a^{n-k} b^k$
- Summe Binomialkoeffizienten: $\sum_{k=0}^n \binom{n}{k} = 2^n$
- Geometrische Reihe: $\sum_{k=0}^n q^k = \frac{1-q^{n+1}}{1-q}$ für $q \neq 1$
- Kleiner Fermat: $a^{p-1} \equiv 1 \pmod{p}$ für Primzahl $p$ mit $p \nmid a$
- $2\times 2$-Inverse: $\begin{pmatrix}a&b\\c&d\end{pmatrix}^{-1} = \frac{1}{ad-bc}\begin{pmatrix}d&-b\\-c&a\end{pmatrix}$
- Kreuzprodukt: $u \times v = (u_2v_3-u_3v_2,\ u_3v_1-u_1v_3,\ u_1v_2-u_2v_1)^T$
- Dreiecksungleichung: $|a+b| \leq |a|+|b|$; $\big||a|-|b|\big| \leq |a-b|$
- Babylonisches Wurzelziehen: $a_{n+1} = \frac{1}{2}(a_n + x/a_n) \xrightarrow{n\to\infty} \sqrt{x}$

## Altklausuren
