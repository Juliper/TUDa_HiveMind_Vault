---
title: CER
aliases:
  - Computational Engineering und Robotik
tags:
  - fb20
  - bachelor
  - wahlpflichtmodul
  - semester-4
  - 5CP
description: ""
draft: false
---
# Skalarprodukt

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c1a9e6f6-a591-4543-9c8a-3342d698a66b/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2f3e96c-94d5-4723-919e-5dd5f45b1452/Untitled.png)

# Norm

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/95b44adf-16de-4245-a6c5-a6e17ab017cd/Untitled.png)

# Matrizen

Sind lineare Funktionen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/359a404f-da85-4553-b0d0-e5d08b080448/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e90f26e3-e07e-4e36-9892-8d30fa94b5c8/Untitled.png)

# Differentialgleichungen

- Die höchste vorkommende Ableitungsordnung heißt Ordnung der DGL
- ist die DGL nach der höchsten Ableitung aufgelöst, heißt sie explizit
- jede(s) DGL(-System) höherer Ordnung kann auf ein DGL-System 1. Ordnung transformiert werden
- Eine DGL, die nicht explizit von 𝑡 abhängt, heißt autonom
- jede(s) nichtautonome DGL(-System) der Dimension n kann in ein autonomes DGL- System der Dimension (n + 1) transformiert werden

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a8529c46-5fde-4963-acb0-82c0a6485cea/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ef04fc38-a018-4eac-9acc-9093158d811e/Untitled.png)

# Rotationsmatrizen

Hier sind die Spalten der Rotationsmatrix immer die Koordianten Achsen des Koordinaten Systems bzgl. a. Kann teilweise einfach abgelesen werden.

## Determinante


# Determinante

$$ \begin{pmatrix} a_{11} & a_{12} & a_{13}\\ a_{21} & a_{22} & a_{23}\\ a_{31} & a_{32} & a_{33} \end{pmatrix} $$

### **Laplacescher Entwicklungssatz**

Wenn man nach Zeile i entwickelt:

$$ det(A) = \sum^n_{j=1} a_{ij} *(-1)^{i+j} * det(A_{ij}) $$

Wenn man nach Spalte i entwickelt:

$$ det(A) = \sum^n_{i=1} a_{ij} *(-1)^{i+j} * det(A_{ij}) $$

Wenn 2x2 Matrix:

$$ det(A) = a_{11} * a_{22} - a_{12} * a_{21} $$

Wenn 3x3 Matrix:

$$ det(A) = a_{11} \cdot a_{22} \cdot a_{33} + a_{12} \cdot a_{23} \cdot a_{31} + a_{13} \cdot a_{21} \cdot a_{32} - a_{31} \cdot a_{22} \cdot a_{13} - a_{11} \cdot a_{32} \cdot a_{23} - a_{33} \cdot a_{21} \cdot a_{12} $$

# Eigenkram

# LGS

# Rotationsmatrix

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e94624b6-ec17-42c5-920e-7309ffb1bec2/Untitled.png)

# DGL

### Inhomogene lineare Anfangswertprobleme

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d52cee2b-de31-4363-808e-b1fa0937c6d1/Untitled.png)

1. homogene Lösung bestimmen
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/232bfbfb-f460-459a-b4a7-e4921b50f1d4/Untitled.png)
    
2. partikuläre Lösung bestimmen und in gegebene einsetzen einsetzen
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/490af5c0-54f5-42d7-bb1d-eef5a989d657/Untitled.png)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b9282d34-e17d-4020-8c5d-bb64a2beac7f/Untitled.png)
    
3. homogene und partikuläre Lösung addieren für allgemeine Lösung
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c92bb3e9-82b0-4c69-8c9f-f0e73a033112/Untitled.png)


Klaussurvorbereitung

# Grundlagen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de92c62b-0dad-43cf-a029-e7010012affb/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/395325a5-2b60-42a1-b830-bdfcbd496af8/Untitled.png)

## Rotationsmatrixen

$$ R_x(\theta)=\left(\begin{array}{ccc}1 & 0 & 0 \\0 & \cos \theta & -\sin \theta \\0 & \sin \theta & \cos \theta\end{array}\right), \quad R_y(\theta)=\left(\begin{array}{ccc}\cos \theta & 0 & \sin \theta \\0 & 1 & 0 \\-\sin \theta & 0 & \cos \theta\end{array}\right) \quad \text { und } \quad R_z(\theta)=\left(\begin{array}{ccc}\cos \theta & -\sin \theta & 0 \\\sin \theta & \cos \theta & 0 \\0 & 0 & 1\end{array}\right) $$

## DGL

- Ordnung := höchste Ableitung
- autonom := DGL hängt nicht explizit von t ab
    - Bei Richtungsfelder t unabhängig
- linear := $x'(t) = A(t)x(t)+B(t)u(t)$
- homogen := $x'(t)=A(t)x(t)$

### Eigenwerte

### pq

Jacobi matrix

inverse

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e92a2255-3578-4ab0-a096-6cd3cfccb42e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36271d5b-b64f-4612-a42d-c32303cf0d62/Untitled.png)

# Statische Modellierung - Kinematik

### Transformationen und Rotationen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e05da9a-4828-44a7-a92b-149ab5c4d886/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a483b7e-9d87-4771-9686-88a9e0003beb/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54f9f560-1d3a-4791-b6b8-c4fbcbb7b843/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fec7500-9821-4301-92a7-88aa8e900e37/Untitled.png)

Zudem gilt:

$$ ^aT_b^{-1} = \left( \begin{array}{rr} ^aR_b & ^ar_b\\ 0 & 1\end{array}\right)^{-1} = \left( \begin{array}{rr} ^aR_b^T & -^aR_b^{T}\cdot^ar_b\\ 0 & 1\end{array}\right) $$

$$ ^aT_b^{-1} = ^bT_a $$

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/75da2104-77a9-49f8-8be4-6875cc7b2a00/Untitled.png)

Homogene Transformationsmatritzen sind assoziativ aber nicht kommutativ

### Vorwärtskinematikmodell

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1b7c10a1-dd48-46b5-a73f-f167493aa945/Untitled.png)

- $^0R_6$ Spalten sind Einheitsvektoren von $S_6$ (Rotation)
- $^0r_6$ Position des Endeffektors in $S_0$ (Translation)

Zudem gilt:

$$ \hat{p_1}={ }^a T_O{ }^O \hat{p} $$

ändert das Bezugssystem von $S_0$ zu $S_a$ und Punkt bleibt fest

$$ \hat{p_2}={ }^O T_a{ }^O \hat{p} $$

verschiebt Punkt in $S_O$

### Denavit Hartenberg Konvention

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bc06a42c-3d2f-4743-a872-75279335afc1/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/932a3d8c-0fed-46a8-9b88-5cf14b12d688/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/adaa3caa-c331-4ab2-85ec-8792e9ef0db9/Untitled.png)

# Lösung nicht linearer Gleichungsmodelle

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9e0ea926-7c43-4342-b5c5-2c8d28c85e7b/Untitled.png)

### Fixpunktiteration

## Übliche Fixpunktgleichungen für f(x)

- $x^{(k+1)} = g_1(x^{(k)}) = f(x^{}(k)) + x^{(k)}$
- $x^{(k+1)} = g_2(x^{(k)}) = A * f(x^{}(k)) + x^{(k)}$ (Relaxiertes Verfahren)

## Konvergenzbedingung

- Alle Eigenwerte müssen im Einheitskreis liegen
    - $|\frac{\partial g}{\partial x}\left(x_s\right)| < 1$
- Im eindimesionalen Fällen bedeutet das für eine Funktion f(x) mit FPI Ansatz g(x) = f(x) + x :
    - $|g'(x_s)| < 1$

## Relaxationsmatrix / Relaxations-Koeffizient

$$ A=-\left[\frac{\partial f}{\partial x}\left(x_s\right)\right]^{-1} $$

## Eigenschaften

- Gute globale Konvergenz
- Konvergiert linear

### Newton-Verfahren

## Iterationsvorschrift

$$ x^{(k+1)} = x^{(k)} - \frac{f(x^{(k)})}{f'(x^{(k)})} $$

oder

$$ x^{(k+1)} = x^{(k)} + \Delta x^{(k)} ~~~~~~~~ \Delta x^{(k)} = J_F(x^{(k)})^{-1} \cdot -F(x^{(k)}) $$

F(x) ist hierbei die Funktion deren Nullstelle wir ermitteln

## Eigenschaften

- Schlechte globale Konvergenz und gute lokale Konvergenz bei gutem Startwert
- Konvergiert quadratisch

### Vorwärtsdifferenzen Quotienten

# Dynamische Modelle

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0c8ec368-036c-4499-ad11-998dc1480ef5/Untitled.png)

### Gedämpfte schwingende Feder

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/46f2d09c-fe1d-4d8b-a7ea-e5d767760751/Untitled.png)

### Pendel

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de4a7b5b-5741-4d70-9900-f13339e3aac5/Untitled.png)

$$ M_{reib} = -d \phi' $$

$$ M_{tan} = l \cdot F_{tang} $$

$$ I = ml^2 (Trågheitsmoment) $$

## Metronom

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ed673e88-7421-4056-b183-5979e76d75f7/Untitled.png)

### Tangentialkräfte

$$ sin \phi = \frac{F_{tan}}{F_g} $$

### Radialfeder Drehmoment

$\phi_0$ ist hierbei die Ruhelage (bein uns wäre es 0)

### Trägheitsmomente der Massen

$$ I = m \cdot l^2 ~~~~~~ (\text{Trägheitsmoment}) $$

### Drehmomente

$$ M_k = k(\phi - \phi_0)~~~~~~ (\text{Radialfeder}) $$

$$ M_{tan} = F_{tan} \cdot l ~~~~~~ (\text{Tangentialkräfte}) $$

$$ M_I = \phi'' \cdot (I_1 + I_2)~~~~~~ (\text{Trägheitsmoment}) $$

Für das Momentengleichgewicht müss die Summe aller Drehmomente gleich 0 sein. Hierbei ist auf das Vorzeichen zu achten. Drehmomente die zur Ruhelage hin zeigen sind negativ.

$$ \sum^N_{i = 1} M_i = F_{tan,1} \cdot l_1 - F_{tan,2} \cdot l_2 - M_k - \phi'' \cdot (I_1 + I_2) = 0 $$

### ODE

$$ \frac{F_{tan,1} \cdot l_1 - F_{tan,2} \cdot l_2 - M_k}{I_1 + I_2} $$

## Rolle Feder System

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3d2d4d54-10e2-4164-8e8e-274a97ba71f3/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0ab3af7c-cd6b-4a8d-9eeb-a8941d50b6be/Untitled.png)

## Richtungsfelder

Für

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a513691f-ae1b-4169-a81f-5e8837747165/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5d000e15-fd06-47c3-9b89-6533d446d7ed/Untitled.png)

und Anfangswertproblem die max geschwindigkeit bestimmen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c67aa092-6f4f-4e45-8626-38d8b2842173/Untitled.png)

# Simulation von ODEs

- Für nicht lineare ODEs numerische Verfahren

## Einschrittverfahren

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b3c8857-fd15-41d7-864b-4594f584adaa/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d49784d1-934b-4fd6-89e0-3645bf190e68/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5ed5aae6-612b-4cec-bd8a-3b73e8e580bb/Untitled.png)

## Explizites Euler-Verfahren 1. Ordnung

$$ x_{t + 1} = x_t + h \cdot x'(x_t) $$

Unterschätzt Lösung

## Implizites Euler-Verfahren 1. Ordnung

$$ x_{t + 1} = x_t + h \cdot x'(x_{t+1}) $$

Überschätzt

für jeden Verfahrensschritt eine nichtlineare Gleichung gelöst werden

## Symplektische Eulerverfahren 1. Ordnung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1e4f800a-4c6a-44eb-bbda-83c6131ec2f9/Untitled.png)

## Heun-Verfahren 2. Ordnung

$$ x_{t+1}^p = x_t + h \cdot x'(x_t)\\x_{t+1} = x_t + \frac{h}{2}(x'(x_t) + x'(x_{t+1}^p)) $$

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/af5e58b1-0537-4a25-a735-6be4e938aa3d/Untitled.png)

## Klassisches 4-stufiges Runge-Kutta-Verfahren 4. Ordnung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2ec7bb11-7236-4402-b539-8dc318ab7099/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ea4ffb9-d266-4056-ae05-ed9ef87a0b57/Untitled.png)

## Approximationsfehler

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/64e00378-f65d-4ba4-95a1-07100d4001d4/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f382aac3-8bd9-4bc9-aece-a71d7f0124a4/Untitled.png)

## Schrittweitensteuerung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fcc2a56-70be-4423-9c19-64abdb453b2f/Untitled.png)

Lokaler Fehler in abhänigkeit von hk und hk/2

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/47799d0c-ade1-4f01-b9b8-07300abb76f3/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7f7f2740-d107-4a5a-b74d-87b2e9ec3ba5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c209f0f-8079-488d-a635-6de71d99b3c7/Untitled.png)

## Zeitcharakteristika

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/53a63d23-0f69-48ad-92c8-ec637f483b53/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/83522e6c-26fd-46ef-9fd5-f867f2e2dc52/Untitled.png)

## Steifheit

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fe0b7dcb-2e38-4a02-8a5a-f4faf4aa0511/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a5f7216-064c-4eb4-9c0a-91c264cca724/Untitled.png)

## Was tun bei Unstetigkeit

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3da47668-861a-4a04-b5be-1e5475f8c2e6/Untitled.png)

# Gleichgewichtslösung und stationäre Zustände

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06a6c176-1b88-48e8-a01e-3e24b6e1abc4/Untitled.png)

### Wann existiert eine Gleichgewichtslösung?

Bei einem linearen DGL und quadratischen A

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/54200560-f8dc-492b-abeb-80a36dd391a0/Untitled.png)

muss A invertierbar sein, das bedeutet A muss regulär sein (det(A) ≠ 0)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0aef7808-68a3-43c8-941a-0b969e60797e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f978831d-5a2b-469e-a71a-d641ee896777/Untitled.png)

## Linearisierung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b109e7b2-e2c6-474a-8092-a01b212ac38d/Untitled.png)

Fällt ein Arbeitspunkt mit einer Sprung- oder Knickstelle zusammen, so kann man um ihn nicht linearisieren (und auch nicht in der „engeren“ Umgebung).

## Stabilität von linearen ODEs

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c6be661-180d-466a-8b76-f79df918fc45/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e096dc1e-90ba-4c70-a193-d1574ec709a6/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04fcf851-c23b-4d8d-84da-52a7c6e800cf/Untitled.png)

# Steuerung und Regelung

Steuerung (open loop) := nur abhängig von der Zeit

Regelung (closed loop) := abhängig vom aktuellen Zustand

Wenn ein System, welches durch eine lineare Differentialgleichung beschrieben wird, instabil ist, können wir es mit einer Regelung stabilisieren

### Schaltfunktionen

Einfach Funktionen die bei bestimmten Events gleich 0 sind

### PD-Regler

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77385ba4-a87c-457f-a831-b4a24efb5c5e/Untitled.png)

kritisch gedämpft

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/081f1723-7d99-418e-99b6-29f8c4e4600d/Untitled.png)

# Partielle Differentialgleichungen

# Computerarithmetik und Messfehler

### Messfehler Regeln

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9da051e5-e54a-4df4-9445-25a1d85088de/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/44e853b6-d415-491b-9cc0-996797788c6f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/87905d51-cb41-4747-b8da-cf13a55de0ea/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/225b48fe-0617-4003-b3a4-8780ee2f8676/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1d0497ee-6e98-4df0-b433-a10997d3e06b/Untitled.png)

### Konditionszahlen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/452b2a3e-34fc-4dc0-89a8-9f087a361230/Untitled.png)

### Arithmetik Auswrtung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eaafcc02-47f7-4d14-900d-85b684850cb7/Untitled.png)

# Systemidentification

### White-Box (fixierte Struktur)

Die Klasse der Funktionen wird anhand von Domänenwissen (z.B. “Naturgesetze” in der Physik für ODEs) festgelegt

### Black-Box

Anstatt diese komplizierten Effekte zu modellieren, kann man auch mit Modellen 𝒇𝜃 arbeiten, welche sehr viele verschiedene Funktionen darstellen können

### Zwei möglich Ansätze

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cf727b83-a529-41e0-8d4c-33d4887317df/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a0c2d08a-7392-48dd-82c4-3854472b6424/Untitled.png)

### Linear Least Squares Regression

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7e03f56c-b111-451c-8e99-5c1ae3ff2da5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/733a0474-9252-41cc-8a35-285700ea69d8/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2ce16be5-ae7f-4544-8a3b-7a782ffc6a97/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1ae2f817-1420-4554-8867-057b67389da7/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e0ffa44-5e81-4498-b26c-dddd733e5963/Untitled.png)

### Summe der Absolutbeträge

1. Gütefunktion L aufstellen
2. Und alle Werte einsetzten (hier vx,0)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79ffcba0-badd-436d-8eb2-fe8438ca6117/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bb452f08-aaeb-498e-be8e-2dc844b1b833/Untitled.png)

# Verifikation und Validierung

### Verifikation

Formaler (meist mathematischer) Nachweis der Korrektheit, dass ein Modell eine vorgegebene Spezifikation (z.B. maximale Rechenzeit/Fehler, durchschnittlicher Fehler) erf¨ullt → meist unm ¨oglich vollst¨andig beweisbar wegen zu großer Komplexit¨at oder fehlendem Zugang zum “wahren” Modell

### Validierung

Plausibilitätsüberprüfung, dass ein Modell einer vorgegebenen Spezifikation entspricht

# Selbsttestfrage und Quizes

## Kapitel 0

### Was versteht man unter den Begriffen System, Modell und Simulation?

- Simulation ist der Prozess des entwerfens eines Modell für ein wahres System und virtuelle experimente mit dem Model
- Eins System ist eine Einheit die durch Zustandsvariablen beschrieben werden kann

### Für welche Zwecke kann man Simulationen einsetzen?

- billiger, schneller, oft besser, kann Sachen die im labor nicht gehen
- Bekanntes Scenario Verstehen und Nachvollziehen, Oprimieren
- Unbekanntes Scenario vorhersagen

### Was muss sichergestellt werden, damit virtuelle Experimente mit

Simulationen reale Experimente ersetzen können?

- Simulierte Systemverhalten muss mit dem Verhalten des realen Systems ausreichend gut übereinstimmt (Validierung)

### Was sind die grundlegenden Schritte des Computational Engineering?

- Problemspezifizierung := Zweck der Simulation
- Modellierrung := Abstraktion, möglich genau, relevante Merkmale
- Implemetierung := Auswahl Berechnungsverfahren, Programmierung, Visulaisierung
- Validierung := Tests, Korrektheitsnachweis (Verifikation) ist in der Regel unmöglich

### Wie können Modelle klassifiziert werden?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b23cabd1-37f7-4a2b-af63-35060c12f000/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6df2f332-f071-4fd9-a707-013d50cbd290/Untitled.png)

### Was versteht man unter „The Scientific Method“?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18664eed-7d66-4528-8203-02980904422e/Untitled.png)

### Warum braucht auch die Künstliche Intelligenz Simulationen?

Die Fähigkeit, die Auswirkungen unterschiedlicher physischer Handlungen vorhersagen zu können, ist wesentlich für KI, insbesondere bei Robotern!

## Kapitel 1

### Wie lautet eine allgemeine Notation für die in Systemmodellen auftretenden Größen?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d60d8831-ca97-44a5-b727-8a35736744ef/Untitled.png)

### Welche grundlegenden Fähigkeiten sind charakteristisch für Roboter?

- Physical interaction abilities
- Sensing abilities
- Planning abilities (onboard computers)

### Wie sind Roboterarme und -beine typischerweise aufgebaut?

- 6 bis 7 Gelenke (3 Hüfte, 1 Knie, 2 Fußgelenk)
- Drehgelenke, Schubgelenke

### Wie wird die räumliche Anordnung eines Objektes beschrieben?

- Koordinatensystem (Rechtssystem)

### Wie können Position und Orientierung von Roboterarmen und -beinen mit (expliziten) Gleichungsmodellen beschrieben werden?

- Vorwärtskinematikmodell

### Was versteht man unter dem Vorwärtskinematikmodell eines Roboters?

- Produkt der lokalen Transformationsmatrizen ($^0T_1 \cdot ^1T_2 \cdot ...$)

## Kapitel 2

### Wie ist das Fixpunktverfahren aufgebaut?

Das Fixpunktverfahren ist eine numerische Methode zur Annäherung von Lösungen von Gleichungen f(x)=0 durch die Suche nach einem Fixpunkt der Funktion g(x), derart dass g(x)=x. Das bedeutet, dass der Punkt x ein Fixpunkt von g ist, wenn er auf sich selbst abgebildet wird.

### Wie kann eine Relaxationsmatrix einer Fixpunktiteration zur Konvergenz verhelfen?

Alle Eigenwerte der Jacobi-Matrix der Iterationsfunktion am Lösungspunkt sind nicht nur < 1 sondern = 0 !

### Welche Iterationsschritte werden bei der Basisversion des Newton-Verfahrens ausgeführt? Und wie sind diese begründet?

- Schnitt von Tangente mit x-Achse → neuer X Wert usw.

### Welche praktischen Schwierigkeiten können beim Newton-Verfahren auftreten? Und wie kann man diesen begegnen?

- Startwertwahl (nahe an Nullstelle)
- möglicherweise andere Nullstelle
- Vorallem hoch nichtlineare Probleme schwer

### Warum ist inverse Kinematik schwieriger als Vorwärtskinematik?

- Mehre Lösungen möglich
- Implizites Gleichungsmodell muss gelöst werden

## Kapitel 3

### Müssen wir bei Punktmassen die Orientierung modellieren?

Nein

### Wie kann ich ein einfaches mechanisches System modellieren?

### Was bedeuten Ordnung, Autonomisierung, Lösbarkeit einer gewöhnlichen Differentialgleichung?

## Kapitel 4

### Wie lautet ein allgemeines Zustandsraummodell dynamischer Systeme?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c497035-e592-4e16-8d1d-27b0557c2924/Untitled.png)

### Wie lautet ein Beispiel für ein Dynamikmodell?

### Wie kann bei einem linearen Dynamikmodell die Zustandsgleichung und das Messystem dargestellt werden?

### DGL Eigenschaften

- autonom := nicht explizit von t abhängig nur von x(t) oder so
- Ordnung := höchste auftretende Ableitung
- linear/quadratisch := höchste Potenz von x(t) (natürlich auch den Ableitungen)

## Kapitel 5

### Wofür benötigt man numerische Integrationsverfahren?

- Für nicht lineare ODE-Systeme

### Was sind Einschrittverfahren und deren Konsistenzbedingungen?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2141ca5-dad1-4b1d-8a8f-616504a98e2f/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4edb3af0-9382-41da-a3b1-ea6dbdcf195c/Untitled.png)

### Was sind Schwächen von Einschrittverfahren der Ordnung 1?

- Für kleinen globalen Fehler werden kleine Schrittweite benötigt
- Durch kleine Schrittweite aber großer Rundungsfehler

## Kapitel 6

### Wodurch entstehen Approximationsfehler?

- Jeder Iterationsschritt der numerischen Integration hat einen Fehler
- durch die Approximation des Integrals
- durch Rundungseffekte aufgrund der Darstellung von Gleitkommazahlen auf heutigen Rechnerarchitekturen mit endlicher Mantisse
- Kleine Schrittweite reduziert Approximationsfehler aber erhöht Rundungsfehler bei zu kleinen Schrittweiten.

### Was ist eine Schrittweitensteuerung?

### Wodurch entstehen Berechnungsfehler bei der Anwendung eines numerischen Integrationsverfahrens für ein gegebenes ODE-System?

- Durch die Wahl des Integrationsverfahrens
- Durch die Wahl des Datentyps, z.B. Single, Double, Quad Precision
- Durch die Nichtlinearität der zu integrierenden Funktion 𝒇(𝒙)

### Was sind die Zeitcharakteristika eines linearen (bzw. linearisierten) Differentialgleichungssystems?

- Zeitcharakteristika beschreiben Zeitspannen, in denen sich relevante Vorgänge der einzelnen Lösungskomponenten 𝒙𝑗(𝑡) abspielen

### Was kann mit Hilfe von Zeitcharakteristika abgeschätzt werden?

- Schrittweiten und Simulationsdauer

### Was sind steife Differentialgleichungen?

- Große Unterschiede in den Zeitcharakteristika
- Verschieden schnelle Charakteristiken

### Warum ist Steifheit eines ODE-Systems problematisch?

- numerisch schwierig
- implizite verfahren nötig (bilden Stabilität richtig ab)
- explizite Verfahren brauchen sehr kleine Schrittweite

### Warum sind ODEs mit Unstetigkeiten wichtig?

### Welche Schwierigkeiten verursachen Unstetigkeiten bei ODEs für die numerische Simulation?

- 𝒇 muss mindestens so oft stetig differenzierbar sein wie die Ordnung des numerischen Integrationsverfahrens
- Schaltfunktionen müssen bestimmt werden

## Kapitel 7

### Was ist ein stationärer Zustand und wie hängt er mit der Gleichgewichtslösung zusammen?

- Gleichgewichtslösung haben Beschleunigung = 0
- stationäre Zustände treten immer bei lang genug Simulation
- Gleichgewichtslösungen können stationäre Lösungen sein

### Was bedeutet Linearisierung? Wann kann ich sie anwenden?

- Nichtlineare ODEs mit linearen ODEs approximieren in der näher der Gleicchgewichtslösung
- Nicht anwenbar wenn Gleichgewichtslösung bei Sprung- bzw. Knickstelle

## Kapitel 8

### Was ist der Unterschied zwischen Steuerung und Regelung?

- Steuerung (open loop control) := Stellgrößen nur zeitabhängig
- Regelung (closed loop control) := Stellgrößen abhängig vom aktuellen Zustanf

### Kann man per „Software“ eine virtuelle Feder oder einen virtuellen Dämpfer zu einem dynamischen System hinzufügen?

### Was ist der Unterschied zwischen einer „Sollwert“- und einer „Sollwerttrajektorien“-Regelung?

### Was ist ein PD-Regler? Was würde einen PID-Regler ausmachen?

### Was ist ein Zustandsregler?

### Was bedeuten „open loop“ und „closed loop“?

### Was bedeuten „feedforward“ und „feedback“?

### Wie kann man den geschlossenen Regelkreis als Differentialgleichung beschreiben?

### Was ist (über-/unter-/)kritische Dämpfung?

## Kapitel 9

## Kapitel 10

### Wie werden reelle Zahlen auf heutigen Computerarchitekturen typischerweise repräsentiert?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dc3f2303-7454-42e7-9aef-02a4ca161242/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b70b8af-53d0-4a33-bad6-aaa6b741e6b9/Untitled.png)

### Welche grundlegenden Unterschiede gibt es für die elementaren arithmetischen Operationen auf heutigen Computerarchitekturen im Vergleich zu deren theoretischen mathematischen Eigenschaften?

- endlich

### Was versteht man unter Rundung?

- Anpassung an verfügbaren Platz

### Wie setzen sich Rundungsfehler fort? Was hat das mit Kondition zu tun?

### Was versteht man unter „Auslöschung“ (cancellation)?

### Welche Möglichkeiten gibt es, den Einfluss von Rundungsfehlern auf die Berechnungsergebnisse abzuschätzen und zu bewerten?

### Wie hängen Mess- und Rundungsfehler zusammen?

### Warum ist Ariane 5 abgestürzt? Was hat das mit Zahldarstellung und Rundungsfehlern zu tun?

- Überlauf

## Kapitel 11

### Warum brauchen wir Parameterschätzung?

- Weil man das System nicht immer zersägen und alles ausmessen kann
- Weil die CAD Daten manchmal nicht gut genug sind
- Um unsere Annahmen bzgl. des Systems zu hinterfragen
- Um die Qualität des Modells zu verbessern

### Warum funktioniert die System Identifikation aus dem direkten quadratischen Fehler nicht immer gut genug?

- Weil die Eingangsdaten korreliert sind
- Weil die unterschiedlichen Ausgangsgrößen unterschiedlich stark und unkorreliert verrauscht sind
- Weil das Rauschen am Ausgang korreliert ist.
- Weil die Eingangsdaten verrauscht sind.

### Welche Kostenfunktion ist hier gemeint?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1f97ef8e-cd61-42a7-bb10-4a18314e9993/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e36b50da-b9bc-40a3-978f-f7ac2b2d2b7b/Untitled.png)

### Welche Annahmen liegen „Least Squares“ zu Grunde?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/046eb9d7-b34a-4d3e-aefe-e967c4017c45/Untitled.png)

### Was sollte man tun, wenn die Eingangsdaten verrauscht sind?

- Filtern

### Ist Least Squares robust gegenüber verrauschten Ausgangsdaten?

### Warum sollte man mehrmals mit unterschiedlichen Daten schätzen?

## Kapitel 12

### Was sind die Chancen und Risiken bei Black-Box Basis-Funktionen?

- Risiko: Man braucht genau die richtigen Basis-Funktionen!
- Risiko: Man hat manchmal zu viele Basis-Funktionen!
- Chance: Mit genügend vielen [interessanten] Basis-Funktionen lässt sich jede Funktion darstellen.

### Welche Chancen und Risiken bieten tiefe

neuronale Netze?

- Risiko: Sie sind schwerer zu trainieren.
- Risiko: Sie haben manchmal auch zu wenige Features!
- Chance: Sie generieren sich ihre Features selber!

### Warum ist nichtlinear least squares schwerer als

linearer least squares?

### Warum ist White-Box System Identifikation immer unvollständig?

schwer zu modllieren teilweise (Reibung usw

### Warum sind „unvollständige“ Modelle gefährlich?

Un- oder falsch modellierte Aspekte können systematisch die Parameterschätzung verfälschen

### Was ist an realen Systemen schwer zu modellieren?

- Reibung
- Reibmoment

### Was für Black-Box Basis Funktionen gibt es?

- Monome und Cosinusterme

### Was sind die Probleme mit Basis-Funktionen? Was passiert bei zu vielen oder zu wenigen?

### Wie unterscheiden sich neuronale Netze von Basis Funktion-Ansätzen?\

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a1490934-f300-4a2e-8de0-d54264eb4d61/Untitled.png)

### Was für Funktionen können sie repräsentieren?

### Wie viele Basis Funktionen kann ein neuronales Netz repräsentieren?

## Kapitel 13

### Bei der Systemidentifikation bei Monomen…

- … müssen die zu den jeweiligen Monomen gehörigen Parameter bestimmt werden
- … muss die Zahl und maximale Ordnung der Monomen manuell festgelegt werden
- … muss die Zahl und maximale Ordnung der Monomen aus den Daten bestimmt werden

### Was für Fehlerquellen gibt es bei der Parameterschätzung?

- Modellierungsfehler
- Fehlerakkumulation durch wiederholten Einsatz des Modells
- Rundungsfehler
- Programmier-, Implementierungsfehler

### Wie kann man mit Modellfehlern umgehen?

### Was bedeuten Verifikation und Validierung?

Verifikation

- Formaler (meist mathematischer) Nachweis der Korrektheit, dass ein Modell eine vorgegebene Spezifikation erfüllt
- Meist unmöglich vollständige Korrektheit zu beweisen (zu komplex)

Validierung

- Plausibilitätsüberprüfung, dass ein Modell einer vorgegebenen Spezifikation entspricht
- Geschieht durch geeignete systematisch und erfolgreich untersuchte Beispiele/Tests

### Wie unterscheidet sich Verifikation von Programmen zu Verifikation von Modellen? Gibt es ein „wahres“ Modell?

### Wie unterscheidet sich Validierung von Programmen zu Validierung von Modellen?

Programm

- Syntax
- Plausibilitäþsprüfung
- numerische Korrektheit

Modell

- Zulässigkeit und logische Konsistenz der Modellannahmen
- Ausreichende Detailliertheit des Modells
- Korrektheit (Genauigkeit) der Modellparameter

### Was sind Test- und Trainingssets? Wie generiert man diese Datensätze?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/10af7c54-6e1c-491a-8a69-2657055d6c93/Untitled.png)

### Was passiert wenn der Testfehler hoch und der Trainingsfehler niedrig ist?

### Wann sollte man White-Box Modelle nehmen? Wann nicht?

### Was stimmt zu Schätzfehlern?

# Richtungsfelder

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ce6557d-70bb-465b-87ba-1a6e916fe8fe/Untitled.png)

# Programmieren
