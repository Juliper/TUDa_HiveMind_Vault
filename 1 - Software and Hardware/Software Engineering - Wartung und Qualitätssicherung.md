---
title: SEWQ
aliases:
  - Software Engineering - Wartung und Qualitätssicherung
tags:
  - fb20
  - bachelor
  - wahlpflichtmodul
  - semester-6
  - 6CP
description: ""
draft: false
---
## Warum Projekte scheitern?

Unklare Anforderungen und Abhängigkeiten sowie Probleme beim Änderungsmanagement!!!

### Nachteile von Wasserfallmodell

- Anforderungen werden früh eingefroren
- Keine Wartungsphase

## QS-Ziele

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ae8c487f-51f8-4eb0-b49d-2ed744be34ac/Untitled.png)

## Reverse und Reengineering

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3f8d9f13-0b38-4f5d-a2bd-2823ec227cfc/Untitled.png)

Aus dem erhaltenen Design vom Reverse Engineering kann wie folgt vorgegangen werden

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9319d7a4-5736-4232-a3fd-ac0118121f5a/Untitled.png)

---

## Konfigurationsmanagement

## Begriffe

**Dokument:**

- Ist ein Gegenstand, der der Konfigurationsverwaltung unterworfen wird.
- Kann eine einzelne Datei oder ein ganzer Dateibaum sein.

**Versionsobjekt:**

- Ist der Zustand eines Dokuments zu einem bestimmten Zeitpunkt in einer bestimmten Ausprägung.
- Beispiel: Ein Dokument in der Version 1.0.

**Variante:**

- Ist eine parallel existierende Ausprägung eines Dokuments, die unterschiedliche Anforderungen erfüllt.
- Beispiel: Ein Dokument in Deutsch und Englisch.

**Revision:**

- Ist ein zeitlich aufeinander folgender Zustand eines Dokuments.
- Beispiel: Ein Dokument mit der Revision 1, das nach einer Änderung die Revision 2 erhält.

**Konfiguration:**

- Ist ein komplexes Versionsobjekt, eine bestimmte Ausprägung eines Programmsystems.
- Oft hierarchisch strukturierte Menge von Dokumenten.
- Beispiel: Die Konfiguration einer Software mit allen zugehörigen Dokumenten in einer bestimmten Version.

**Baseline:**

- Ist eine Konfiguration, die zu einem Meilenstein (Ende einer Entwicklungsphase) gehört und evaluiert (getestet) wird.
- Beispiel: Die Baseline einer Software vor dem Release.

**Release:**

- Ist eine stabile Baseline, die ausgeliefert wird.
- Kann intern an Entwickler oder extern an bestimmte Kunden oder die Öffentlichkeit ausgeliefert werden.
- Beispiel: Die neueste Version einer Software, die den Kunden zur Verfügung gestellt wird.

## KM-Versionsmanagement (Verwaltung Entwicklungsgeschichte des Produkts)

### Diff/Patch Datei

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ef39cc7f-7d63-4b2e-bb9d-317806002d89/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5e87950d-3a7c-46c4-85df-c83a5500b651/Untitled.png)

- Zeilennummern inklusive Kontextzeile
- - (entfernt), + (hinzgefügt), ! (geändert)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c917e8f7-b901-492b-9849-18b688d9e23b/Untitled.png)

### Drei-Wege-Verschmelzung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a2325d1e-50b4-40b7-a6d0-22ba8764d27b/Untitled.png)

- Textzeile in B, NV1 und NV2 gleich ⇒ Textzeile in E
- Textzeile in B aber nicht in NV x oder/und NV y ⇒ Textzeile nicht in E
- Textzeile in NV x oder/und NV y aber nicht in B ⇒ Textzeile in E
- Textzeile aus B in NV1 und NV2 geändert ⇒ manuelle Konfliktbehebung (gilt auch für neue Textzeilen in NV1 und NV2 an gleicher Stelle)

### Source Code Control System SCCS

- Kann nur auf text Dateien angewendet werden
- Eine Basisversion wird gespeichert
- Andere Revisionen können mittelts vorwärts Delta ausgecheckt werden
- Ausgecheckte Revisionen sind Schreibgesperrt
- Je mehr Revisionen, desto länger dauert die Rekonstruktion

### Revision Control System RCS

- Die neuste Version auf Hauptzweig wird gespeichert und alle anderen mittels Vorwärts und Rückwärtsdeltas
- optionale Schreibsperren
- Revisionsbäume mit besserem Zugriff auf Revisionen

### Concurrent Version System CVS

- optimistisches Sperrkonzept (Drei-Wege-Verschmelzung)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4f604017-52e4-4a18-91ea-9f41fa1baa9b/Untitled.png)
    
- Revisionsidentifikation und damit rudimentäres Releasemanagement auch durch frei wählbare Bezeichner
    
- Deltas funktionieren nur für Text und nicht binär
    
- keine Versionierung von Verzeichnisstrukturen (Directories)
    
- keine gute Unterstützung für geographisch verteilte Software-Entwicklung
    
    - Nur ein Server zum syncen
    - Volle Daten wurden hin und her gechickt

### Subversion SVN

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f2c766d5-a91c-4dd2-993f-93b407ce0e0d/Untitled.png)

Zweidimensionaler Zustandsraum des Subversion-Repositories IDK

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f32e6f80-c26c-4aac-aa06-9109a846d036/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/931b55eb-1959-4de6-acca-6766d529da26/Untitled.png)

### Git

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/513db0d0-7131-4778-9a1d-e2caa18516dc/Untitled.png)

## KM-Variantenmanagement (Ausprägungen von Produkten)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5ed84d5f-5794-4496-a1b4-7ca6014ce9ba/Untitled.png)

Domänenentwicklung := Entwicklung der gemeinsamen Plattform bzw. Rahmen

Anwendungsentwicklung := konkrete SPL Instanz in der Domäne

### Feature Model (Welche varianten sind möglich)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e36c3c27-224a-469e-a35e-d0b14e772642/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8f3d1bd1-483b-4a4f-ba84-02a25a7befb9/Untitled.png)

### Wie in Software Varianten verwalten?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3ecbb9b1-e9ba-44e4-8357-45e1504c1f4b/Untitled.png)

## KM-Releasemanagement

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55cfd1ff-6b7c-4889-b5e9-16f96b332f15/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/44ca70b7-a2fc-4594-9786-0d70a9a80e9a/Untitled.png)

## KM-Änderungsmanagement

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/96f9f1d5-9f68-4dd9-bad5-f4c62e3eb754/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8462d264-a0e6-478f-b587-c2931fca4325/Untitled.png)

---

## Statische Programmanalyse & Metriken

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/40679960-47bc-4614-829c-ec7536b7d53b/Untitled.png)

## Analysierende Verfahren (Prüfung von Menschen)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8d08407d-34b4-4f8d-9b2d-d3af6464148c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f9cc5f05-3eb9-454c-9dbb-0f5987dd7778/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/186722df-0002-46e8-bde0-19c458a6aab6/Untitled.png)

## Strukturierte Gruppenprüfungen (Reviews)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c30062b2-1846-4285-87a3-f3ed0bc03430/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6aeb3ec2-3720-4f91-8164-b6dda5d43073/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5c5b8521-052d-4948-87d1-8bef77392e47/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3c1ee7ff-7aee-42e7-8b6c-a4c81e2f3e54/Untitled.png)

## Testende Verfahren (mit Eingabewerten testen)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4da7cb0b-cf16-473b-ac8b-93cc5240f74f/Untitled.png)

## Kontrollflussorientierte Analysen

### Kontrollflussgraph

- Jede Zeile ein Knoten (außer wo nix ist wie else, break oder nur Klammern)
- Datenflussattribute d(x), c(x), p(x) und u(x) an Zustand schreiben
    - d(x) := Variablendeklaration mit Initalisierung oder neue Wertzuweisung
    - c(x) := Variable ist Teil einer Berechnung (auch print)
    - p(x) := Variable ist Teil von logik
    - u(x) := Variable ohne Initalisierung bzw. wenn beim verlassen eines scopse variablen gelöscht werden (variablen innerhalb einer Schleife oder am Ende von Methode alle Parameter)

### Datenfluss-Anomalien (nochmal angucken)

- dd := unbenutzer Wert wird überschrieben
- du := defnierter Wert wird unbenutzt auf undefiniert gesetzt
    - stark := zyklische Pfade werden ausgeschlossen
- ur := undefinierter wert wird verwendet
    - stark := zyklische Pfade werden ausgeschlossen

Nachteile

- funktioniert schlecht bei komplexen Datenstrukturen
- verzeigerte Datenstrukturen auch schlecht

## Datenflussorientierte Analysen

### Datenflussgraph

- Jede Zeile ein Knoten (außer wo nix ist wie else, break oder nur Klammern)
- Kanten beschreiben Benutzung von Definitionen
    - d(x) → c(x) oder p(x) (kein d(x) Mitten im Pfad)

### Abhängigkeitsgraph

- Enthält alle Datenflussgraph Kanten
- Kanten (des Kontrollflussgraphen) von allen Bedingungen zu direkt kontrollierten Anweisungen (das sind die Anweisungen, deren Ausführung von der Auswertung der betrachteten Bedingung abhängt).

### Vorwärts-Slice / Rückwärts-Slice

- Rückwertsslice einer r(v)-Anweisung beeinhaltet alle eingehenden Kanten und auch die eingehenden Kanten der Knoten der eingehenden Kanten (rekursiv).
- Vorwärtsslice wie Rückwärts aber mit ausgehenden von d(v) (welche zeilen sind abhängig von definition)

## Softwaremetriken

Produktmetriken

- messen Eigenschaften der Software
- Qualität der Software

Prozessmetriken

- messen Eigenschaften des Entwicklungsprozesses
- Dauer oder Kosten der Entwicklung

## Eigenschaften von Metriken

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b27c2077-cf62-432f-b614-7ce3a47870a7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b247a4b7-a1bc-45a3-867a-20827c424293/Untitled.png)

## Ziele von Metriken

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b5e45c6b-40a0-4ea1-aa5c-696d85d83254/Untitled.png)

## Kontrollflussmetriken

### Lines of Code (LOC)

Anzahl Knoten in Kntrollflussgraph

- Zu groß = Zu komplex
- Zu klein = Schnittstellenprobleme
- Berücksichtigt Kanten nicht

### Zyklomatische Zahl

- Anzahl Knoten - Anzahl Kanten + 2 * Zahl voneinander unabhängiger Graphen (meistens 1)

### Programmlänge (L) nach Halstead (unnötige Komplexität messen).

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e53fa442-c3d0-4f38-96bf-8d51006b0f7f/Untitled.png)

- Operatoren und Operanden (auch Konstanten wie Zahlen) aufschhreiben und Verwendungen zählen
- $L = n_1~~log_2~~n1~~+~~n_2~~log_2~~n_2$

### Programmgröße (V) nach Halstead

- $N~=~N_1~+~N_2$
- $n~=~n_1~+~n_2$
- $V~=~N~\cdot~log_2~n$

## Datenflussmetriken

Code komplexität messen (weniger komplex = weniger Fehler)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7f85ab9b-24e3-45a7-9895-2e0e46e2371d/Untitled.png)

### Live Variables

- Die „Live Variables“-Metrik berechnet für eine Programmkomponente die durch- schnittliche Anzahl lebendiger Variablen dieser Komponente je Knoten des zugehöri- gen Kontrollflussgraphen
- lebendig := ab d(x) (NICHT SCHON BEI u(x)) ist Variable lebendig bis zum letzten d(x) oder r(x)
- LiveVariables := Summe aller lebendigen Variablen pro Knoten / Anzahl der Knoten

### Variablenspanne

- Die „Variablenspannen“-Metrik einer Programmkomponente berechnet die durchschnittliche Spanne zweier direkt aufeinander folgender definierender oder referenzierender Auftreten derselben Variable im zugehörigen Kontrollflussgraphen (kürzester Pfad)
- Spanne ist Anzahl der Kanten zwischen den Knoten
- [Spannen]x + [Spannen]y / ((#Spannen)x + (#Spannen)y)

## OO-Metriken (missing)

---

## Dynamische Programmanalysen und Testen

### Fehler

- Fehlerzustand := inkorrektes Teilprogramm
- Fehlwirkung := Wirkung eines Fehlerzustands nach außen (Falsche Rückgabe z.B.)
- Fehlhandlung := menschliche Handlung die zu einem Fehlerzustand führt (keine Benutzerhandlungen)

### Validation

- Ist es das richtige System?
- Erfüllt es die Anfworderungen?

### Verifikation

- Ist die Implementierung der Anforderungen richtig

### Fehlerarten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9305363c-c560-4a80-8c7d-0ffeb3a7a113/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/18edf2f4-d6b0-4bbf-b2d9-b7483051eaa8/Untitled.png)

## Was wird getestet?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/59ea9e63-847c-49e4-84df-c64ea54a88a9/Untitled.png)

## Wie wird getestet?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ad33f7b6-9e05-49d2-8717-525012549fc2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/63687e59-07c2-4a61-8a68-24c9cd54c12b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5239b826-c01d-408a-afef-161853072d7d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4c01935a-e40d-4ed2-a273-9622ec934af9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d4019a08-5f9e-4c90-8662-f92598fc6d0e/Untitled.png)

## Grundsätze des Testens

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/af6cb61e-1cef-4b21-9d21-a67da843b573/Untitled.png)

## Funktionsorientierte Testverfahren (Blackbox)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3f7dc070-8fd4-44f2-9ed9-eb5693107fdc/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9a6db666-3372-4ced-b403-e53acee28616/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/76e41ccf-af8a-4b5c-926c-31f8cc829651/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7d4427d3-8572-433f-a3d1-ae6d2e0af626/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fc12169a-4cfd-4ed1-9b6f-ff3711af6a4b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/595f7f4e-f1da-4595-9041-6fffae06db07/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/840fa4bf-ee60-4c1b-a4a7-a56f26ab5d16/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/00649850-07b7-4d47-91eb-f53de3bfff1a/Untitled.png)

## Funktionsorientiertes Testen

### Äquivalenzklassen- vs. Grenzwertanalyseverfahren

Beim Äquivalenzklassenverfahren wird ein Wert aus jeder Äquivalenzklasse genommen, beim Grenzwertanalyseverfahren werden zusätzlich noch die Grenzwerte der Äquivalenzklasse betrachtet.

### Klassifikationsbaum

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/32eaa303-d073-4a8a-8ea3-00c8878f778d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f267f9be-dabb-4b63-8dd2-212026b3c5df/Untitled.png)

### Paarweises Testen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/909b92fa-519c-425b-9ffa-84b5f18a60da/Untitled.png)

## Kontrollflussbasierte Testverfahren (Whitebox)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a7beb2c1-9510-4920-81d6-15e9b6ff441c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a5085ae5-b728-48aa-bdbb-4c91dd738632/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/890cd6c2-f86a-43d9-8174-5e3ad0f43cd1/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/affe72fd-0b50-420d-ad8d-27803576d02a/Untitled.png)

## Kontrollflussbasierte Testverfahren (repeat)

### Anweisungsüberdeckung (C0-Test)

- Jeder Knoten des Kontrollflussgraphen muss mindestens einmal ausgeführt werden

### Zweigüberdeckung (C1-Test)

- Jede Kanten des Kontrollflussgraphen muss mindestens einmal ausgeführt werden
- Umfasst Anweisungsüberdeckung

### Atomare Bedingungsüberdeckung

- Atomare Tailbedingungen müssen einmal true und einmal false sein
- Umfasst nichtmal Anweisungsüberdeckung

### Minimale Mehrfachbedingungsüberdeckung

- atomare Teil- und Gesamtbedinungen müssen einmal true und einmal false sein
- umfasst Zweigüberdeckung

### Boundary Test

- alle Pfade auf denen Schleifen maximal einmal durchlaufen werden (ohne besondere praktische Bedeutung)

### Boundary Interior Test

- alle Pfade auf denen Schleifen maximal zweimal (in direkter Folge) durchlaufen werden (Anzahl Testfälle explodiert). If müssen auch jeweils einmal f und t sein
- Bei geschachtelter Schleife und if z.B.:
    - 0xS1, (0)xS2
    - 1xS1, (0)xS2
    - 1xS1, (1)xS2 (mit if einmal t und f)
    - 1xS1, (2)xS2 (mit if einmal t und f)
    - 2xS1, (0,0)xS2
    - 2xS1, (1,1)xS2 (mit if einmal t und f)
    - 2xS1, (2,1)xS2 (mit if einmal t und f)
    - 2xS1, (2,2)xS2 (mit if einmal t und f)

### Modifizierter Boundary Interior Test

- bei geschachtelten Schleifen wird beim Durchlauf einer äußeren Schleife die Anzahl der inneren Schleifendurchläufe nicht unterschieden

## Datenflussbasierte Testverfahre

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f809b4c8-5448-4963-91db-09cdcee6123d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/418f8615-1bb8-4f71-a57f-5486dcdfd325/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5d130137-76b1-40ab-b205-c138449e3ea2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a60c8a9c-419a-42c3-b923-c21fea4bc6b5/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4fa3466e-9d21-4adf-a995-52d8147093f8/Untitled.png)

## Datenflussbasierte Testendeverfahren

### All-defs-Kriterium

für jede Definitionsstelle d(x) einer Variablen muss ein definitionsfreier Pfad zu einer Benutzung r(x) existieren (und getestet werden)

### All-p-uses-Kriterium

für jede Definitionsstelle d(x) wird jeweils ein definitionsfreier Pfad zu allen (erreichbaren) prädikativen Benutzungen p(x) getestet

### All-c-uses-Kriterium

für jede Definitionsstelle d(x) wird jeweils ein definitionsfreier Pfad zu allen (erreichbaren) berechnenden Benutzungen c(x) getestet

### All-p-some-c-uses Kriterium

für jede Definitionsstelle d(x) wird jeweils ein definitionsfreier Pfad zu allen (erreichbaren) prädikativen Benutzungen p(x) getestet; gibt es keine prädikate Benutzung p(x), so wird wenigstens ein Pfad zu einem berechnenden Zugriff c(x) betrachtet

### All-uses-Kriterium

all-p-uses- + all-c-uses-Kriterium

## Testen objektorientierter Programme

## Testplanung

Ereignis [Bedingung] / Folge

### Flacher Automat

- Alle untersysteme auflösen zu normalen Automaten
- Transitionen mit OR werden aufgesplitet
- Untersysteme mit parallelen Abläufen werden in Kreuzproduktzustandsautomat verwandelt

### Transitionsbaum

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/389373e3-8b79-44e6-87c1-ac96376425b5/Untitled.png)

- Jeder Blattpfad ist ein Test
- Irrelevante bzw. verbotene Transition sind einfach alle bekannten Transitionen die aber in einem Knoten nicht erlaubt sind
- Wenn Zustand im Baum bereits vorhanden aufhören

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ef46f817-be2f-4847-bf89-779d56a00552/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8ebc1b54-243e-49dd-bae3-1307bd8166a2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/371eb88e-ce88-4ab6-a1bb-264a5c2c77a4/Untitled.png)

## Testen von Software-Produktlinien

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fa7aa7b8-a217-4b65-9f8a-8be1b9fdece1/Untitled.png)

## Mutationsbasierte Testverfahren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c14b546a-911b-4072-8287-43e710e00f7f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a90b9743-4b35-458f-9ec3-59e172bf6c70/Untitled.png)

---

## Modellbasiertes Testen

Brauchen wir weil Klassen Zustände haben können und Verhalten einer Methode abhängig von diesem Zustand ist

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/82a02dc0-04c6-4337-9248-996669910ed2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/97bbc99e-abca-49b4-9444-cdab1391d136/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/589c52c4-c8e8-485e-b860-d43a98cbf60f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/acfe658b-994c-4b8b-b91a-d3c1fe979173/Untitled.png)