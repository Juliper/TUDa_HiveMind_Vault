---
title: VC
aliases:
  - Visual Computing
tags:
  - fb20
  - bachelor
  - wahlpflichtmodul
  - semester-5
  - 5CP
description: ""
draft: false
---

# Zusammenfassung

- nicht lineare Filter (median) können nicht als Faltung dargestellt werden
- Für View Frustum Cullling kann man k-d Trees benutzen
- Transfer-Funktionen werden verwendet, um skalaren Werten in Volumendaten optische Eigenschaften wie Transparenz oder Farbe zuzuordnen.

Computer Vision := Aus Bildern Daten

Computer Grafik := Aus Daten Bildern

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/daa2fd61-1c25-4e61-8abc-1c1a2dab211b/Untitled.png)

# Formeln

$$ Buntheit = \frac{Farbigkeit}{Helligkeit(Weiß)} $$

$$ Relative Helligkeit = \frac{Helligkeit}{Helligkeit(Weiß)} $$

$$ Sättigung = \frac{Farbigkeit}{Helligkeit}=\frac{Buntheit}{Relative Helligkeit} $$

# Wahrnehmung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/68957224-12b7-4386-a721-4f9b9558d1d3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/139b207d-56ab-416c-8108-1cfa58791d4b/Untitled.png)

Wahrnehmung (visuell, akustisch, haptisch) → Entscheidung → Reaktion(stimmlich, motorisch)

## Stäbchen

- Für Helligkeit (grün)
- außerhalb von Fovea

## Zapfen

- Für Farben (rot, grün, blau)
- Innerhalb Fovea

## Seharten

- skotopisches Sehen := Nachtsehen / Stäbchensehen (adaptiert an Dunkelheit) Empfindlichkeitsmaximum bei grün
- photopisches Sehen := Tagsehen / Farbzapfen (blau, grün, rot)

## Netzhautzellen

- Horizonttalzellen := kombinieren mehrer Rezeptoren einer Region
- Bipolarzellen := Informationsfilter
- Amakrinzellen := zeitliche Verarbeitung
- Ganglienzellen := integrieren informationen

## Sensoraufbau

- Zapfenmosaik in der Fovea Centralis (10% blau, 48% grün, 42% rot)
- Bayermuster (50% grün, 25% blau, 25% rot)

## Aufmerksamkeit

- gewählt := Fokus auf eine von mehreren Möglichkeiten
- geteilt := Multitasking
- erfasst := Reiz zieht Aufmerksamkeit auf sich

## Helligkeitsarten

- Helligkeit (brightness): Entspricht der wahrgenommenen Menge an Licht, das von einer selbstleuchtenden Lichtquelle (z.B. Monitor) ausgeht.
- Helligkeit (lightness): Entspricht der wahrgenommenen Menge an Licht, das von einer reflektierenden Oberfläche ausgeht

## Frühe Wahrnehmung

- Farbe, Richtung, Bewegung, Größe, Beleuchtung/Schattierung
- Raumwahrnehmung: Tiefenwahrnehmung, Entfernungs- und Distanzwahrnehmung, Ausrichtung des Körpers im Raum

## Depth Cues

Für Größe/Entfernung von Objekten einschätzen oder Navigation in 3D. Sind additiv und haben verschiedene Gewichtungen bei interpretation.

- Pictorial Depth Cues (Monokular, mit einem Auge)
    - linearperspektive(parallelen laufen zusammen), verdeckung, texturgradient (größenverlauf vermittelt Tiefe), fokus und blur (scharfe sachen wirken weiter vorne), Schattierung, atmospährische Tiefe, Schattenwurf (Schatten auf Boden vermittelt tiefe)
- Binokulare Depth Cues (mit zwei Augen)
    - disparität, parallaxe, akkomodation, konvergenz
- Dynamische Depth Cues (Animation)
    - bewegungsparallaxe (objekte in unterschiedlichen Entfernungen bewegen sich anders), kinetische tiefeneffekte, interposition, Bewegung von Highlights

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7c84a8d5-9370-442d-b271-63b823d6b63a/Untitled.png)

## Vektion

- Scheinbare Eigenbewegung
- Einflussgrößen := Größe des bewegten Feldes, Statischer Vordergrund als Referenzrahmen vs. bewegter Hintergrund, Stereo

## Stroop-Effekt (Stimulus-Response Compatibility)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/455250f2-2b23-4b9c-8408-cfa3a31a73a4/Untitled.png)

## Change Blindness

- Effekt wenn einem große Änderungen nicht auffallen
- Wegen Aufmerksamkeit?

# Objekterkennung

- sliding window scale (bild wird kleiner gemacht und pixel für pixel abgescannt)
- Wie erstellt man so ein Modell? → Objekt Representation(Merkmal wahl z.B. lokal global), Trainingsdaten, Klassifikator und Lernmethode

## Appearance Model

1. Repräsentation der Objekte (lokale/globale Merkmale)
2. Trainingsdaten (positive und negative Beispiele)
3. Klassifikator und Lernmethoden

# Bayes Decision Theor

- Welche Annahmen trifft der Naive Bayes Classifier?
    - Das Merkmale statistisch unabhängig sind
    - liefert aber häufig guter Ergebnisse

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/99bac672-ec90-4643-9eee-ee00123cffee/Untitled.png)

P(A) = P(A | B) * P(B) + P(A | NOT B) * P(B)

## Entscheidungstheorie

- P(C1 | x) > P(C2 | x)
- P(x | C1)P(C1) > P(x | C2)P(C2)

## Erkennungsarten

- Verifikation := Passt gegebenes Merkmal zu Datenbank
- Identifikation := Person Merkmale werden festgestellt

# Fourier-Theorie

## Funktionen

- Gerade wenn f(x) = f(-x) → nur Cosinus weil Sinus wegfällt (bn = 0)
- Ungerade wenn -f(x) = f(-x) → nur Sinus weil Cosinus wegfällt (an = 0)

## Dirichlet Bedingung

1. Die Anzahl Unstetigkeiten innerhalb einer Periode ist endlich
2. Die Anzahl Maxima und Minima innerhalb einer Periode ist endlich
3. Die Funktion ist in jeder Periode integrierbar

- Jede Funktion, die die Dirichlet-Bedingungen erfüllt, läßt sich als Summe von Sinus- und Cosinusfunktion darstellen

## Whittaker-Shannon Theorem

- Abtastrate doppelt so hoch wie Grenzfrequenz

## Fourier-Transformation

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ad2eacfa-df4a-42ee-a7cb-86bd00136245/Untitled.png)

- zerlegt Funktion in ihre Frequenzbestandteile
- Eine Faltung zweier Funktionen im Ortsraum entspricht einer Multiplikation der Fouriertransformierten im Frequenzraum.
- Eine Faltung zweier Fouriertransformierten im Frequenzraumentspricht einer Multiplikation der Funktionen im Ortsraum
- Frequenz fehlerfrei rekonstruierbar, wenn Abtastfrequenz delta x ^1 doppelt so hoch wie Grenzfrequenz

# Bilder

## Farbräume

- YCBCR, CIEXYZ

### CIELAB

- Gegenfarbraum
- nahezu Wahrnehmungsgleichabständig
- modelliert Nichtlinearitäten des visuellen Systems

## Technische Farbräume

- RGB, sRGB, HSI, CMYK

## Histogramm

- Man kann Kontrast, Helligkeit, Über- und Unterbelichtung erkennen
- Häufigkeitsverteilung

## Aliasing

- Frequenzen die oberhalb der halben Abtastfrequenz liegen, werden als niedrige Frequenzen interpretiert, da eine vollständige Rekonstruktion des Ausgangssignals nicht möglich ist

## Pixeloperationen

- Negativ, Binärisierung (eher runter), Fensterung, Kontrastspreizung, Dynamikkompression, Gammakorektur, Helligkeit, Histogrammausgleich, Differenz, Mittelung

## Filter im Ortsraum

Werden durch Filtermasken beschrieben

Hochpass

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fffd6e54-088f-4adf-ade6-5140e4537dd2/Untitled.png)

Tiefpass

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c590de76-76a9-4ce9-9400-cc1cfbd07b27/Untitled.png)

Band Pass

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3ebd7d78-b1af-4cfa-be58-43bcdc968d98/Untitled.png)

### Hochpassfilter

- Positive und negative Koeffizienten und Summer ergibt 0
- Produzieren positive und negative Werte
- Berechnet Erste Ableitung/Differenzfilter (partielle Gradienten) oder Zweite Ableitung

### Laplacian Filter

- Kein Weichzeichnungsfilter

### Tiefpassfilter

- Positive Koeffizienten und Summe ergibt 1
- Produzieren nur positive Werte
- Mittelwert Filter (verwischt), Gauß Filter, Median Filter
- entfernt bzw. reduziert rauschen

### Median

- Median nehmen
- ist nicht linear (sortieren und so)

### Gaussian Filter

- Weichzeichnet

## Filter im Frequenzraum

- schnelle Berechnung
- einfache Handhabung
- Orstraum approximiert nur

### Hochpassfilter

- tiefe Frequenzen abschneiden
- scharfe Übergänge werden deutlich

### Tiefpassfilter

- hohe Frequenzen abschneiden
- weniger Rauschen aber unschärfer
- glattes Bild

### Bandpassfilter

- Nur Frequenzen innerhalb range

## JPEG Kompression

Eliminierung redundanter Daten

1. Umwandlung in YCbCr
2. Farb Subsampling (kleine Gebiete bekommen einheitlichen Farbwert, aber genauen Helligkeitswert weil grün und so)
3. Diskrete Cosinus Transformation (Bildinformationen in Frequenzbereichzerlegen)
4. Quantisierung (informationen beseitigt die nicht wichtig sind)
5. Kodierung der Koeffizienten (bitstrom erzeugen)

# Bildverarbeitung

## Bildverbesserung

- Korrektur von Nicht-Linearitäten der Kamera
- Anpassung der Helligkeit, Kontrast
- Bildbereiche hervorheben/ unterdrücken

## Blurring

- Weichzeichnen von Kanten und Farbübergängen in einem Bild
- Gauss, Median, Box
- Blurring ist stabil, daher auch auf verrauschtes Bild anwendbar

## Deblurring

- numerische Fehler → komplex konjugierte Matrix verwenden
- nicht korrekt gestellt nach hadamard
    - kleine Eingabeänderungen verändern Ausgabe stark

## Scale-Space

- zuviele zusätzliche Terme führen zu Ergebnis verschlechterung
- entfernt image blurring

## Wiener Filter

- Wenn R zu klein wird zu Hochpass FIlter := Entfernt grobe Struktur & Kanten; Verstärkt das Rauschen
- Wenn R zu groß wird zu Tiefpass Filter := Grobe Strukturen bleiben, Kanten werden verwischt und Rauschen wird entfernt
- R optimal (Bandpass) := Grobe Struktur bleibt erhalten, Kanten werden verstärkt, Rauschen wird entfernt

## Energie

- Pixel Intesität
- wichtige Nachbarschaftsbeziehungen

## Mehrschrittverfahren

- Rauschen wird verwischt
- Kanten werden verstärkt

### Perona Malik

- stoppt Zeit muss definiert werden
- Verhältnis Signal/Rausche steigt and und fällt dann ab
- schwierig richtigen Stopppunkt zu finden
- k bestimmt welcher Gradinent erhalten bleiben soll (groß (nur große Gradienten) = starke Kanten; klein(fast alle) = starke, schwache KIanten und rauschen)

### Total Variation

- distance penalty (Abweichung zu Originalbild)
- Algo terminiert bei optimaler Lösung

## Hadamard

1. Eine Lösung existiert
2. diese ist eindeutig
3. die Lösung in einer vernünftigen Topologie kontinuierlich von den Daten abhängt (bei kleiner Änderung der Eingabe keine große Änderung der Ausgabe)

- Laut Hadamard ist das Problem ”Image Deblurring” nicht korrekt gestellt. Was wird (z.B. im Falle des Wiener Filters) getan, um dem entgegenzuwirken? Regularisierung zB Wiener filter extra parameter R

# Graphik-Pipeline

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8d586ed5-fbf9-4965-88ce-6f6fa7f7d8b5/Untitled.png)

- Anwendung := Eingabe Daten, Repräsentation von 3D Daten
- Geom. := Clipping, Culling, Transformation, Sim. Beleuchtung
    - Modell Trans.: Skaliert und rotiert Modelle
    - View Transformationen: Verschiebt und rotiert alle Modelle im Kamerabereich
    - Projection Transformation: perpektivische oder parallele Projektion der Szene
- Rast. := Verdeckungsrechnung, Farbwertinterpolation
- Ausgabe := Speichern, Display, Hardcopy

Octree 1 2

```
        4 3
```

## Grafische Primitive

- Punkte, Linien, Dreiecke

## Rasterisierung

- Aufteilung des Models in festgelegten Abständen: "Primitive (Linien, Polygone) werden in Pixel zerlegt“

## Algorithmus von Bresenham

- Wieiviele Pixel werden gezeichnet := max((x1, y1) - (x0, y1)) + 1

## Scanline Algo

Füllt Dreiecke bzw. auf 2D projezierte Objekte

## Shading

### Phong-Shading

- Die Normalen in den Eckpunkten werden für jeden Punkt linear interpoliert und normiert
- Der Helligkeitswert ergibt sich aus der interpolierten Normalen
- Leuchtdichte I_total = ambient, Diffus, Specular

### Flat

- Die Normale des Primitivs ergibt eine einheitliche Helligkeit

### Gouraud

- Die Normalen in den Eckpunkten ergeben die Helligkeitswerte für die Eckpunkte
- Die Helligkeitswerte der Eckpunkte werden linear interpoliert

## Clipping

- abschneiden von Objekten am Rand von gewähltem Bildausschnitt

## Occlusion Culling

### z-Buffer Algo

- Jede Szene mit jeder Art von Objekten kann behandelt werden
- Komplexität ist unabhängig von der Tiefenkomplexität
- In eine fertige Szene können nachträglich Objekte eingefügt werden
- Leicht in Hardware zu realisieren
- Transparenz ist nicht realisierbar
- Die Genauigkeit des z-Buffers ist beschränkt

### Painters Algorithmus

- Primitve von hinten nach vorne (z-Wert) zeichnen
- Transparents und im Kreis überdeckende Objekte nicht möglich

### Culling

- Rückseite von Objekten nicht rendern
- Weil sieht man nicht
- Backface Culling, View Frustum Culling, Occulusion Culling

# Transformation

## Transformationen in Grafikpipeline

- Modelling Transformation := Ordne 3D Objekte im Raum an
- Viewing Transformation := wählt Betrachterstandpunkt und positioniert
- Project Transformation := projiziere Viewing Volume in 2D
- Viewport Transformation := Wandle Bildschirmkoordinaten um

## Transformationen

- Die Verkettung beliebiger affiner Abbildungen ist nicht kommutativ
- Bei einer Skalierung sind alle Werte außerhalb der Diagonalen null
- Projektionstransfomrationen sind keine affine Transformation

### Affine Abbildungen

- Affine Transformationen := Translation, Rotation, Skalierung, Sicherung
- Verhältnisse von Längen, Flächen, Volumen bleiben erhalten
- Beschränkte Objekte bleiben beschränkt
- Geraden werden auf Gerade abgebildet
- Parallele Objekte bleiben parallel

## Matrizen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/39548116-dcba-4213-865d-df76c9dacf07/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a176150d-cfba-4e4a-a3d0-f8483c794934/Untitled.png)

Translation → Skalierung → Rotation

### How to rotate

1. Verschiebung des Rotationszentrums in den Ursprung
2. Rotation
3. Zurückverschiebung in das Rotationszentrum

Bei Formel = 3 * 2 * 1

## Projektion

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/540a6bf9-7151-485d-acba-2537b3163d27/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/41cb9a4a-acc3-49e5-8dc6-61b467ca3e95/Untitled.png)

### Perspektivische Projektion (nicht affin)

- Längenverhältnisse ändern sich
- Winkel ändern sich
- Beschränkte Objekte bleiben beschränkt
- Geraden werden auf Gerade abgebildet
- parallel bleibt NICHT parallel
- “Natürliche” Wahrnehmung
- COP = Punkt wo sich Strahlen schneiden

### Paralleler Projektion (affin)

- parallel bleibt parallel
- Beschränkte Objekte bleiben beschränkt
- Geraden werden auf Gerade abgebildet
- Winkel ändern sich
- MEDIZIN

# Informationsvisualisierung und Visual Analytics

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9467f4c4-029d-47f2-a829-8ba495ac747e/Untitled.png)

## Visualisierungstechiken

### 1D

- Kuchendiagramm
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/586658a8-5802-4306-a640-e8c3b77849b2/Untitled.png)
    
- Balkendiagramm
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/212919c9-5ba2-4b90-8475-ead2f451e887/Untitled.png)
    

### Zeitreihen

- Liniengraph
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4ed2476d-1018-4dc8-bbd7-164b379a2509/Untitled.png)
    

### 2D oder 3D

- Scatterplot (matrix → alle Paare der Dimensionen als Scatterplot)
    
    - Viele Dimensionen → limitierter Platz
    - Nur paarweise Abhängigkeiten sichtbar
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3582af04-5c86-42ec-94c8-81cb711fe6b1/Untitled.png)
    
- Parallele Koordinaten
    
    - abhängigkeit zwischen mehreren Dimensionen leicht sichtbar
    - falsche Ordnung → Daten mehrdeutig
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/31661c78-7698-4cd4-9402-f90d523db8e2/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/88856bcf-a8af-4334-a8d2-4e1e13b00b73/Untitled.png)
    

### Hierachien oder Bäume

- Node Link Diagramme
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d012aba7-14cb-4171-85c6-ffd6fc20ed32/Untitled.png)
    
- Treemap
    
    - Die Vergleichbarkeit von Rechtecken mit unterschiedlichen Seitenverhältnissen ist schwierig
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/73c3a99f-2813-42ab-b7c0-1eb16069b39b/Untitled.png)
    

### Netzwerke oder Graphen

- Knoten Link Diagramm
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/682f4025-3fe5-4d7d-8b19-b2755e780d90/Untitled.png)
    

# Farbe

## Metamerie

- Zwei ungleiche Farbreize sind Metamere, wenn sie die selbe Spektralwertmatrix besitzen
- Beobachtermetamerie := zwei ungleiche Farbreize bei gleichen Betrachtungsbedingungen sind Metamere, wenn sie für eine Person die gleichen, für eine andere unterschiedliche Farbvalenzen liefern
- Beleuchtungsmetamerie := zwei ungleiche Reflektionsspektren sind Metamere, wenn sie die selbe Lichtmatrix besitzen

## Farbeigenschaften

- Helligkeit, Relative Helligkeit, Farbton, Farbigkeit, Buntheit
- achromatisch = Nur schwarz, weiß grau
- chromatisch = Gelb, Rot, Blau, Grün

## Farbwahrnehmungsmodelle

Ermöglichen eine Anpassung der Farbreize für den Farbabgleich bei unterschiedlichen Betrachtungsbedingung

S(patial)-CIELAB und iCAM

## Farbwahrnehmungsphänomene

- Simultankontrast := Hintergrund auf dem ein Farbreiz präsentiert wird, beeinfluss die wahrgenommene Farbe (→ Farbverschiebung folgt Gegenfarbtheorie)
- Crispening Effekt := Der wahrgenommene Farbunterschied zweier Farbreize wird durch einen ähnlichen Hintergrund vergrößert
- Stevens Effekt := Kontrast steigt mit der Leuchtdichte
- Hunt Effekt := Farbigkeit steigt mit Leuchtdichte

# 3D Visualisierung

## 3D-Datenerfassugnsmethode

- Laser-Scanning: Ein Laserstrahl wird auf die Oberfläche des Objektes projiziert, die Skulptur muss nicht berührt werden
- CT-Scan: Umfangreiche 3D-Datenmengen, je nach Skulptur und Gerät muss das Objekt nicht „direkt“ berührt werden

## Voronoi Diagramm und Delaunay-Triangulation

- Um eine Delaunay Triangulation durchzuführen für eine Punktewolke muss diese auf eine 2D ebene projizierrt werden. Für jeden Punkt kann eine Voronoi Zelle definiert werden
- Voronoi → Delaunay := Verbindung der Mittelpunkte benachbarter Voronoi-Zellen mittels Linien, älte"Mittelpunkte bilden Eckpunkte der Dreiecke. Eventuell Edgeflipping durchführen wenn Umkreise von Dreiecken im Netz nicht leer sind.
- Delaunay → Voronoi := Die Eckpunkte der Dreiecke bilden die Voronoipunkte. Die drei Mittelsenkrechten eines Dreiecks bilden die grenzen der Voronoizellen.
- Voronoi und Delaunay sind dual zueinander

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/15793e1b-8b74-4b93-a0f6-ab3b158a7870/Untitled.png)

## Volumenvisualisierung

- Indirekt: Generierung einer Zwischendarstellung des Volumens, Komplexität hängt von der Anzahl an Polygonen ab: z.B. Marching-Squares, Marching-Cubes
- Direkt: Visualisierung ohne Generierung einer Zwischendarstellung, Komplexität hängt von der Anzahl der Voxel und der Auflösung der Anzeigefläche ab: z.B. Density Emitter Modell, Raycasting

## Culling

- unsichtbare Polygone aus der Rendering Pipeline entfernt → verbessert Performance
- Backface := Zum Betrachter gerichtete Rückseiten nicht zeichnen
- View Frustum := Polygone die sich ganz oder teilweise außerhalb von View Frustum befinden nicht zeichnen
- Occlusion := Polygone nach tiefe sortieren und nur rendern falls sie nicht vollständig von anderen verdeckt werden

## Volumen-Rendering-Pipeline

- Basisoperationen := Abtastung, Klassifizierung und Beleuchtung, Komposition (Back to Front, Front to Back)

# Interaction & User Interface

## Interaktionsmöglichkeiten

- Menüs, Kommandozeile, Formulare, Fragen und Antworten, Direkte Manipulation, Metaphern, 3D-Umgebungen, Natürliche Sprache, Gesten

## WIMP

- Windows, Icons, Menüs, Pointers

## UI Komponentenart

- Slider
- Checkboxen
- Radio Button (wie checkboxen mit nur einer auswahl)
- Listboxen (liste mit möglichkeiten)
- Combobox (Wie listbox aber wird ausgeblendet)
- Spinner (beschränkte Liste an Werten)

## 2D Eingabe für 3D Objekte

- Mehrdeutigkeit ist ein Problem → unendlich viele Cursorpositionen

# Multimedia Information Retrieval

## Arten von Suche

- Example, Image, math, sketching, speak, text

## Sucharten

- explorative Suche: Die explorative Suche hat keine konkrete Suchanforderung, sie versucht ein weites Thema zu überblicken und dabei Zusammenhänge und Muster zu erkennen ohne vorher zu wissen, wonach genau gesucht wird/ was entdeckt werden soll. Z.B. kann man nach Trends auf Sozial Media Plattformen suchen, um diese zu analysieren
- inhaltsbasierte Suche: Die inhaltsbasierte Suche hingegen sucht anhand von vordefinierte Kriterien oder Merkmalen gezielt nach Inhalten. Z.B kann somit ein bestimmtes Video gesucht werden, welches gerade sehr beliebt ist.

## Beschreibungsarten

- feature vector, descriptor, annotationen, tags, metadaten

## Metrikeigenschaften

- Nicht Negativ
- Definitheit := d(x, y) = 0 <=> x = y
- Symmetrie := d(x, y) = d(y, x)
- Dreieckungleichung := d(x, y) ≤ d(x, z) + d(z, y)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b363341a-c421-40f2-a865-79e51241cf7c/Untitled.png)

# X3DOM

## Szenengraphstruktur

- gerichtet, azyklich, zusätzlich (nur eine Wurzel), Kein Baum (Knoten können mehrere Eltern haben)
- Ist gut weil: Wiederverwendbarkeit der Objektdaten, Semantische Gruppierung der Objektdaten, ransformationshierarchie ermöglicht Transformation von kompletten Gruppen
- schwierig in HTML zu realisieren weil Baum struktur → X3D mit DEF/USE

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/347fdc79-d61c-41ba-a2c0-08aa64508db1/Untitled.png)

- verwendet XML Syntax
- Basiert nicht auf Bäumen sondern Graphen