---
title: IM
aliases:
  - Informationsmanagement
tags:
  - fb20
  - bachelor
  - semester-4
  - 5CP
description: ""
draft: false
---

# Grundlagen

## Daten, Informationen und Wissen

### Daten

- **Zeichenkette** über bestimmtes **Alphabet**
- Eine **Zeichenkette** die einer bestimmen **Grammatik** folgt nennt man **Nachricht**

→ **Daten** sind noch nicht interpretierte Zeichenfolge die einer Grammatik folgt

### Informationen

- Interpretierte **Daten** werden zu **Informationen** durch einen **Interpretationsbezug**

### Wissen

- Gesamtheit der Kenntnisse, Fähigkeiten, Fertigkeiten, die Personen zur Lösung von Problemen einsetzen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8793b122-7d6e-4d25-b602-ad6557d445a6/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/683cf11a-a59a-4e32-9f84-750116e2650a/Untitled.png)

## Strukturierungsgrade

### Strukturierte Daten

- Tabelle, Diagramm, Wort-/Namensliste, Excel, Messwerte, …

### Semistrukturierte Daten

- Semistrukturierte Daten (XML)

### Unstrukturierte Daten

- Unstrukturierte Daten (Text, Schuabild, Fotografie, …)

## Informationssystem

### Anforderung

- Für Anwendung nötige Daten sollen aus den gespeicherten Daten vollständig abgeleitet werden können (Informationserhalt)
- Wiedergewinnung der Daten soll möglichst effizient sein
- Nur vernünftige Daten sollen gespeichert werden (je nach Informationsbedarf) bzw. gespeichert werden können (Konsistenzerhaltung)
- Anwendungsdaten sollen möglichst redundanzfrei gespeichert werden, um Speicherplatz zu sparen und Anomalien zu vermeiden

## Typische Entwurfsprozesse

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e6dd0039-4737-4bc2-ba96-ba74d0d16e20/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1269ce58-fdca-4733-8de3-ae067850c04a/Untitled.png)

## Arten von Datenzugängen

### Deklarativer Zugang (Suche)

- Spezifiziert durch Prädikate

### Navigierender Zugang (Blättern)

- Anfängliche Positionierung und Verfolgen von Zeigern (Pointern) Wikipedia

# Konzeptionelle Datenmodellierung

ER-Modell

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/aa2fc179-b41e-434a-858c-8867b3300a65/Untitled.png)

# Relationales Datenmodell

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/391569a3-926f-4a87-b90b-76534e8a7f41/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0e59a789-2371-42d3-ac83-4785884c42e5/Untitled.png)

- Relationen müssen Duplikat frei sein (d.h. Eindeutigkeit)
- Reihenfolge ist irrelevant

## Schlüssel

Superschlüssel

- Attributmenge K die jedes Tupel eindeutig identifieziert
- Mehere Superschlüssel pro Relation möglich
- Eigenschaften
    - einfach := K nur ein Element
    - zusammengesetzt := K mehr als ein Element
    - trivial := K enthält alle Attribute
    - minimal := ist doch klar

Schlüsselkandidat

- K muss minimal sein
- Mehrere Schlüsselkandidaten möglich

Primärschlüssel

- Der gewählt Schlüsselkandidat für Schema R als Pk

Fremdschlüssel

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/43d45a3c-be1b-4df7-add9-830fdbd65b84/Untitled.png)

## ER auf Relationales Model abbilden

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d540273c-7004-401a-9ee0-4af183db8361/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5fea416c-7d9d-4054-a240-15b18d48cdce/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f33c5871-d05a-431f-b8bf-578a900b75d3/Untitled.png)

# Relationale Abfragesprache (Imperativ, keine Duplikate)

### Relationalealgebra (RA)

# Befehle

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dac1e5d4-12d3-4fb7-9b68-e6fd50b416fd/Untitled.png)

Auswahl: $\sigma_{Semester > 10} (Student)$ gibt von Relation Student alle Eintge mit Attribut Semester größer 10 zurück.

---

Projektion: $\pi_{A,B}(X)$ gibt alle eindeutigen Einträge der Spalten A und B von Relation X zurück

---

Kartesisches Produkt: $\times$ gibt alle möglichen Kombinationen der zwei Relationen zurück

---

Natürlicher Join: L $\Join$ R

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/74511852-7241-4860-9d97-303ed5031a8b/Untitled.png)

---

Allegmeiner Join: L $\Join_p$ R

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fca73478-3961-4045-a351-d6ea31985cb2/Untitled.png)

---

Left/Right Outer Join:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/42e405bb-1140-426a-a199-d7bb9fa1b30a/Untitled.png)

---

Full Outer Join:

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5b3695c1-02ac-4d2f-865b-932a1b704230/Untitled.png)

---

Semi Joins

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/142caef2-48af-4b38-b33a-9c0a7000eeba/Untitled.png)

### Relationentupelkalkül (RTK)

nicht behandelt

### Relationenwertebereichkalkül (RWK)

nicht behandelt

# Anfragesprache SQL (deklarative, Duplikate)

Können Duplikate haben

## Data Query Language (DQL)\

Select distinct; := Auswahl ohne Duplikate

order by X asc/desc; := Sortierung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b0fb8db7-b248-4135-9f44-4ed6d324906a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bf5ee4fc-624d-4b08-8958-e042a9d4b80f/Untitled.png)

## Data Definition Language (DDL)

| create table (if not exists) ProfessorIn (PersNr integer, Name varchar(30),

|Rang character(2) );|erstellt Tabelle Professorin mit den jeweiligen Attributen (wenn sie nicht schon existiert)|
|---|---|
|create table ProfessorIn||
|(PersNr integer,||
|Name varchar (30),||
|Rang character (2),||
|primary key(PersNr) );|Same aber mit primär schlüssel|
|drop table (if exists) ProfessorIn;|Entferne Tabelle wenn sie exsitiert|
|drop table ProfessorIn cascade;|Entfernt Tabelle und alle abhängigen Objekte|
|alter table ProfessorIn add column Raum integer;|Attribut hinzufügen|

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a1623c07-1d79-48ec-b407-e6f3f8705a33/Untitled.png)

## Datenintegritäten

### Primärschlüssel

- Eindeutigkeit := Jede Zeile muss eindeutigen Primärschlüssel haben
- Fremdschlüsselbeziehungen
- Minimalität

### Not Null

- Attributwerte müssen explizit not null gesetzt werden

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6b242b19-0ac6-4819-a290-6b19f674ff3d/Untitled.png)

### Default-Werte

- Standward wert ‘Null’ oder explizit genannt

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cb02d288-046c-4bac-8a75-e83b4d7bc439/Untitled.png)

### Check-Bedingung

- Werte überprüfen
- In check können auch ganze SQL-Anfragen stehen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a05bd005-b869-4974-93f2-ba4c1eb066cf/Untitled.png)

### Unique-Bedingung

### Fremdschlüssel

## Data Manipulation Language (DML)

### Einfügen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/684f2867-93f7-4bcb-b2bd-a6e938b14ecb/Untitled.png)

### Automatisch inkrementierende PKs

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2a13ed67-1e84-4878-a91b-99caffe944cb/Untitled.png)

### Löschen von Einträgen

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f47f2cf6-bd02-4691-a17c-8483f29b439d/Untitled.png)

### Ändern von Tupeln

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a05a3298-7aa9-4961-a7b1-d950415e73b5/Untitled.png)

## Data Control Language (DCL)

# Relationale Entwurfstheorie

## Anomalien

### Update Anomalie

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c782c9c-7a97-40cd-92f9-c0ea3f7198ce/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/787268d0-36a5-4a88-b491-6dd2a730804a/Untitled.png)

### Einfüge Anomalie

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1c0a1658-826e-483e-9c68-c0b8e7882872/Untitled.png)

### Lösch Anomalie

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/79465429-c6a1-4b15-9134-eeeca4dfa285/Untitled.png)

## Abhängigkeiten

### Funktionale Abhängigkeiten

- Die Menge β ist von α funktional abhängig genau dann, wenn für jeden Wert aus α genau ein Wert für β existiert
- α ist Determinante für β (PLZ bestimmt Ort)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d2f66962-f0c3-4866-bbf8-69efdc8f196c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d79aa72-9921-4778-8653-12394841be5a/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/73c1ff03-3c2a-474b-bf34-22a69792b46c/Untitled.png)

### Schlüsselabhängigkeit

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c8acb924-29f4-4bde-99bc-446d1f6abe41/Untitled.png)

## Normalisierung

Große Relationen in mehrere kleine aufteilen und Anomalien vermeiden

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1ff2b6b0-3ebd-4f8a-8ef6-e9ba955709a6/Untitled.png)

### Verlustlosigkeit

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f1feb3c4-c9fa-4ed9-bb32-f89a1b753d1a/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/acb97c13-ee17-4717-9562-41c1e1112ff0/Untitled.png)

### Abhängigkeitsbewahrung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2b27efd4-f05c-43cc-9fa5-09c160ddb329/Untitled.png)

## Normalformen

### 1NF

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9f4ce5bb-a106-445d-924a-1f47d7f90c62/Untitled.png)

### 2NF

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6864eaca-a934-45f2-9fb2-0d64f8bdf1c5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a06b6eca-698d-4291-989e-84fe6d9688be/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/72ab5661-e2bd-430e-b031-e3176b3a33b5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a5944ad7-b606-4011-acd5-df9509e1c2a7/Untitled.png)

### 3NF

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/36b93307-49d6-4ada-b4b6-bb93f813b1f7/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7f5e4571-10fb-40ac-b78e-e46e2c3c3a63/Untitled.png)

## Synthesealgorithmus

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f67603c0-ee1f-41a4-9b84-a6020c9ba432/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/58ab8897-7d2b-4f68-8d94-1b4a34fc6fdc/Untitled.png)

# Anfragenverarbeitung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fa82a084-d91b-4f63-9770-d3e300eb6fb2/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/03cf9fdf-2b86-4102-bec9-79df1eca4514/Untitled.png)

## Regelbasierte Optimierung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ead951b0-e551-48ca-b4db-6fa3c36ecb5d/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/25446837-ab5d-4695-82f4-e89e38b1f25b/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/798ea693-ddaa-49f8-89a3-caf22c5ea35e/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c0de056a-9f39-4b98-a4bc-283fc8b2aef2/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ca0fb349-397e-44de-bf7f-c3cfbad0ac7c/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/453e3214-3efc-477a-aa27-16e302a58aeb/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cfe890d0-2242-4f48-b058-d7f11b992f05/Untitled.png)

## Kostenbasierte Optimierung

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac0c5e0c-4978-4044-93f8-666191988aca/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c6bc6cd4-66f4-4439-97ff-0607aae1c434/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5ae248d3-1de5-478c-827a-0e96bc218d61/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/70a2d51d-d0b0-495a-a95c-39a1cc78755a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a7b50af6-9a6e-41bc-b7c7-f4d62462ce68/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/79bdf092-b636-467f-ac28-19804fa25709/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a941e043-3f81-423d-9ef8-1e24e9461a25/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/096270c5-1764-4464-9a97-5f65aca24da3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3f64d039-0a03-4f8d-b5d2-daf7a9086476/Untitled.png)

# Transaktionsverarbeitung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fd92f197-1028-4d37-a60c-f9bfc78ead58/Untitled.png)

## Welche Anomalien ohne korrekte Isolation?

### Lost Update

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/864726b7-c9ec-4812-9adf-380c5db5ed81/Untitled.png)

### Dirty Read

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1d87b2ff-e4b4-4ef5-9c7c-eb03eed1a6a0/Untitled.png)

### Non-Repeatable Read

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7619a130-b1b3-47bd-b92e-a5d8b9eebecd/Untitled.png)

### Phantom Read

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8e9124b9-bd61-4042-b33c-aa1ef5b40f22/Untitled.png)

## Konfliktgraph

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d78fabba-fbb7-4002-a952-4b93aa31efdc/Untitled.png)

Pessimistische Ansätze: Konflikte vermeiden (z.B. durch Sperren)! Optimistische Ansätze: Konflikte im Nachhinein erkennen!

## Pessimistische Ansätze

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55d5597b-8bc0-4a91-a05d-8006a1bdb8cb/Untitled.png)

## Lock-based Concurrency Control

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/36eb4c27-e2c9-46b1-90d8-bf85dfddceb2/Untitled.png)

### Two-Phase Locking (2PL)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3141f967-e838-4bf2-b83d-6bc5a2a398f4/Untitled.png)

Verhindert Deadlocks und Cascading Abort nicht

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/656d2067-ea27-4d8f-a921-3f44a1ed248d/Untitled.png)

Verhindert Deadlocks und Cascading Abort

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f1134d9d-7b61-437c-84a3-db80bab0751c/Untitled.png)

### Isolationsstufen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6447a5bb-1377-4840-a41a-89a5397b31e9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0d00379f-a638-49c8-898c-ff3289a25f60/Untitled.png)

## Multi-Version Concurreny Control (MVCC)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ab35a3d1-1e86-43df-a15a-836f117f0da0/Untitled.png)

## Optimistische Concurreny Control (OCC)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c21024b6-eb2c-4d67-9ef6-5be2d5d3f8ee/Untitled.png)

---

# Introduction to Language and Knowledge Processing

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ea34d8cb-c743-440f-a3ad-da1fbba2a1c6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/785ba299-2704-4182-b9ac-7c878b08d12b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/21585917-83ce-430d-89e7-47d29cf62610/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3fa8167b-f4dd-4c0e-8463-85d47f3bc583/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7df6afc6-d3d7-4ef8-a944-18480ba2f400/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/092adab2-1ce5-486a-822d-839c8fddf2d7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/36e45e7c-0967-4465-ba28-767d4ae0382d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/692e032b-8527-4672-b35d-f594367021c3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f0e2fb07-a69a-4754-a48a-f60ef0a96cb7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fcfccfac-300d-4c80-a35b-95c9ddecf4e3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7aea6e7a-2a95-4498-aa92-f2ddeb8902f8/Untitled.png)

### Mehrdeutigkeit

Homophone := Verschiedene Wörter aber gleiche Aussprache

Homograph := Gleiches Wort aber verschiedene Aussprache

## Charakter Sortierung

# Linguistic Preprocessing

## Segmentation

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a43ee473-eb01-41c0-87ea-23be83e110ca/Untitled.png)

## Morphology

Morpheme sind kleinste Einheitt die Sinn hat

freies Morphem/Stamm := kann alleine stehen (wie “cat” von “cats”)

gebundenes Morphem/Affix := kann nicht alleine stehen (wie “s” von “cats”)

Suffix := Nach Stamm (nice + ly)

Prefix := Vor Stamm (un + true)

Infix := Mitte (un + fucking + fassbar)

Circumfix := Auf Beiden Seiten (ge + sag + t)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/742a3640-1c87-434b-a39d-5100c6659cca/Untitled.png)

Wortbildung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f4572c03-a190-44fd-9ea9-f8ca0e238433/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9aa416e4-6866-4609-b452-d5dd44910e3c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ff5dde41-bd83-4e9c-a2ae-98abb3cd4d65/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e8257196-057b-4082-98fe-d686c41f472e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b591bb92-1b40-4f39-b3b2-4ee1c0a17f5d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d3686393-8dde-4347-97ce-cece84e6d7e2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/328d6632-ada3-4c28-a974-a7bcefa195f9/Untitled.png)

## Syntax

### Part of Speech Tagging (POS Tagging)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ed110850-842b-4c2a-a0b7-6448e0d88277/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/35a64dab-a957-444f-ad0e-9a45d73e800b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1998b67c-59cf-4bfe-9319-c931cd4aca7b/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/88c88806-4ba2-4662-b6dc-99626e009822/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/dccd88ae-8e59-4824-b009-258efdf439ce/Untitled.png)

Syntactic ambiguity

Syntactic ambiguity appears if there are multiple possible interpretations of a sentence (we call those sentences ambiguous) and if the possible interpretations are caused by the the way the sentence is composed (i.e., its syntax), rather than by the ambiguity of single words in the sentence

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0a622b7e-765c-48b4-bea3-65a880d92e76/Untitled.png)

## Semantics

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/44d9da3c-762f-44f7-9b67-b85acbce8c31/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/efc586f8-a0b5-463b-a224-c5ead5ede6b1/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/343675e0-ec56-4195-b12e-ac6b7b26c308/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0c4542db-125b-43b4-b524-e099231ddd71/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0fa73cc9-8758-40ef-884e-6f799a919532/Untitled.png)

# Text Corpora

Text Corpora

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/827dc098-de37-4fe7-89a9-b42e2fadd4df/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/829fc21c-4d42-4c0e-9056-3d5f945e0120/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/09f63638-aa34-4546-988a-e1cc2113302d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/084c8535-34ea-48dc-ac01-1d62e7de24f5/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/12ab49fa-f6cf-48ca-b4b6-c0f412f75c7e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a3c3a8c3-d144-4d0a-ac8c-1a68fbf5bfb4/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2fa9ebc3-871d-41f4-bf63-18d5bfe5a756/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/435c2e42-b9db-4bf8-85b8-6117d3e85ff1/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e395ca6b-e518-4757-9c6d-bf3048680ca8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ccddb100-8617-4296-9fb4-47fb0dfa5d3f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/29de13dc-d545-4105-b513-916e8f490032/Untitled.png)

# Lexical Resources and Knowledge Bases

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/428e7b8d-85c7-499c-9aa5-b228b55bb481/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/36cd3939-7f92-4f17-863b-cc7702d62c47/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/67885a40-3d6c-489f-a0b2-d23032fe2969/Untitled.png)

# Information Retrieval

## Overview

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/29460476-a6a3-4e0b-ac39-aba029d972e2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/78696b03-a85c-4027-b566-b848bd631b04/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b4eea7b8-7380-4c3a-94a5-e8e630af92f6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f0dd03d6-f043-4beb-a050-4982ff818cb0/Untitled.png)

## Boolean Retrieval

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5a1ba7e3-e3dd-470b-853f-c809d11aa5ee/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/805d60fb-2fad-4769-89da-958cc6e58f26/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7d254584-c779-4f90-b1a6-3d73dbc6b518/Untitled.png)

## Vector Space Model

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2f0e9556-d70e-4579-a3e7-66028c451653/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/93a53899-5f14-446e-ad98-320c90591bb1/Untitled.png)

## IR Evaluation

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1bfecc8f-0023-4559-8c8e-e8ed8c54e004/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a2aba969-e4b6-4c0c-95b2-e7540039f2c0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a81c2015-5cf8-4de8-adb9-8355f24a2dd1/Untitled.png)

# Information Extraction

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5ecb8303-5057-4932-99a4-b15b569ee837/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0db22602-e511-431e-b490-0071c0b66fec/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0c50d533-5de2-4c5e-8cba-44604c7cc435/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9a4c8abc-383c-480f-87cc-b88fc6c62f03/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3e689c64-2609-43b4-a0c7-650da900a052/Untitled.png)

# Automatic Classification

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c694a1f8-f441-41c9-88d2-3f925c15454e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/15bd242c-211a-41e6-b73c-e8f26f2bbaf6/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/66230ecc-7f98-4627-9901-f492be3ea0d3/Untitled.png)

Euklidische Distanz = |v1 - v2| (erst minus dann wurzel…)

dot produkt = v1 * v2 (alle einträge multiplizieren und addieren)

cosine sim = dot product / |v1| * |v2|

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/448ce749-906f-4787-b352-7e3797cccfd8/Untitled.png)



# Entity-Relationship-Modelle

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bc0c04ed-e465-4990-8b39-83d52c303083/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c29df99b-9dd7-497e-a1de-85b2443f8c3f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f3a32153-f70f-4aad-afe1-5a342069800f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3147e69f-53f1-4a09-8367-1256fbb67868/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9a29db0f-5b3c-4a8d-a16d-d56b529105f8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/86f6c713-7e90-41a3-8764-e81cbae8eda4/Untitled.png)

# Relationales Schema

## ER → Relationales Modell

### Regel 1: Abbildung der Entitätstypen auf Relationen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1b2e8910-efd9-4631-96ca-0c648213c902/Untitled.png)

### Regel 2: Abbildung der Beziehungstypen auf Relationen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fd71e2e5-b37c-48ba-ad4b-d60bb33b2717/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/67bd707c-a19a-40e2-aea5-45ff1bb6f539/Untitled.png)

### Regel 3: Zusammenfassung der Relationen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/af779369-fadf-41e8-acf0-5d1a19897200/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b1b3ae73-a262-4c9b-b058-ef8f64be48cd/Untitled.png)

### Regel 4: Behandlung von schwachen Entitätstypen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bbc34dd4-e741-42cb-9950-7005728d974e/Untitled.png)

## Notationkram

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/61ba0347-0fec-449d-a9f8-a14b029bf6b4/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e528b425-97e4-451e-b9a8-ecb957746935/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cfad956d-6e22-44b3-bddc-671db38f248d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/54b8a362-9c34-43c0-a010-5293b1334e78/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7a5a6c9c-d528-41dd-9f0e-6585fc5a325a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2b841c16-1273-4024-bac2-92dea8765bad/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d0fb8490-99eb-4045-a816-60ab645944a0/Untitled.png)

# Schlüssel

Superschlüssel := Attributmenge die relation eindedutig identifiziert Schlüsselkandidat := minimaler Superschlüssel (kann mehrere geben) Primärschlüssel := Der ausgewählte Schlüsselkandidat Alternativ Schlüssel := Alle Schlüsselkandidaten die nicht Primärschlüssel sind Primatibute := sind die Attribute die in einem Schlüsselkandidaten hat Nichtprimattribute := Sind in keinem Schlüsselkandidaten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/266ba5ff-13f6-4e7e-9712-f6b112c502b6/Untitled.png)

referentielle Integrität := Fremdschlüssel müssen existieren

# Relationale Anfragen

$σ_P(r)$ := alle Tupel von r die P erfüllen

$π_α(r)$ := alle Tupel von den Spalten a von relation r (duplikate werden eliminiert)

L ⨝ R (natürlicher Join)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/747c5d15-4e62-45f9-beb5-9e5d8b22a12f/Untitled.png)

$L ⨝_p R= \sigma _p(L~x~R)$

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/33594dae-697a-421c-9033-de7c951656d3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/33fb65c3-3044-4fc0-b22b-d7fa0be24093/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/29eabedd-c54d-4451-ac04-1d0d68387d82/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/63c4a383-feee-409f-880c-b9418843945c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/004fc9d5-6475-42f5-b381-ea2cfb86f86d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/dc77c103-0d10-4401-92dd-4fd63ad032ad/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/37c2a18d-247f-4d34-8536-99baca88fc43/Untitled.png)

# DDL

## Erstellen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2c1bad0b-f1fe-4df2-9082-ee4098516267/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fe16c129-e20f-4305-b256-3adb7d75c144/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0a4d8fa0-4317-44ba-90c1-4acc072681b7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/eba65180-b72a-49c7-8656-17388485e862/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/dcd2fea1-734a-418b-9eb3-e9e9da6cfec9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7941d543-b850-4b2c-89ed-55795aee7342/Untitled.png)

Sind da wie eigene Attribute

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f9367598-e105-4ccf-99bc-7c6147a0edab/Untitled.png)

## Löschen/Hinzufügen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/96038142-c366-4455-b006-5f06d93a8d3e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b56b4275-292d-4074-b362-5f55afb166eb/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3ee7b28e-938a-43a8-bf36-51c70863ee22/Untitled.png)

# DML und DQL

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0150b5c8-7c83-46d7-8be5-26ed044c5d22/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f9849b6e-c6e1-4086-a7f3-103c61a3ca15/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ee82162c-2f49-4751-98bf-79c845b9f2f7/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/df40ee5f-97d2-4235-afd2-3b128fe2b24d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/db5fd882-6ed0-47aa-8e8c-b467037ad7ec/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c16daab9-3014-4d61-af53-69fbb3226014/Untitled.png)

_ steht für beliebiges Zeichen und % für beliebige Zeichenkette

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9a9517ed-5eb9-4ff9-aff9-ad6ff4834265/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/17a058dd-77ba-4579-991b-463f7c700f97/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/35b7097a-a060-4c78-b633-5145ca7be792/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/34683a5e-568c-4f71-a9a9-609385e15d8c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ccd3acf2-1611-4e6d-969f-825be96885d1/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/55aee145-502a-4aa2-8a06-dc14114e071a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/76ade9e9-2b13-4f25-b596-6d30c6d728a3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/676ec309-54ff-41ec-8311-95de6d6775a9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/29862f31-e1c6-40b3-9c8b-f073f3a3c21e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2ae58440-94b9-4180-a7b6-80646298764a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/31426bcb-7c03-4ca6-87fa-097037a1370c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/969a37b6-0fb0-4e20-aba7-b2aa2299a5bf/Untitled.png)

# Funktionale Abhängigkeiten

## Volle funktionale Abhängigkeit

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/bb0cc08c-cc4d-4919-95fe-6824bc960e9f/Untitled.png)

## Partielle funktionale Abhängigkeit

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b3aaa134-9660-4d35-ad10-6cdfcc2ca7d6/Untitled.png)

## Transitive Abhängigkeiten

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/51a8e8fe-5fad-4d1d-88ae-8246ce4b88f9/Untitled.png)

## Schlüsselkandidaten aus FDs bestimmen

Atributhülle

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e5faf5ec-a4ae-4f83-a15d-90d23476ccdd/Untitled.png)

Algo:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/267eb5bf-f602-47f0-b388-7e2e2d616057/Untitled.png)

Schritt 2 für alle in Schritt 1 gefunden machen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/19451f53-0004-4dec-9996-f0fd888e3824/Untitled.png)

Det. plus fehlt sind Superschlüssel

# Anomalien

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1e7b9b74-5fb3-4e79-a3e5-8ecc177aa13c/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d5ae7c2c-8a34-4cf5-9ae3-eb8b60f862ae/Untitled.png)

# Normalform

1NF

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b0f5a50e-22d2-47f6-8dec-5c97d1efe944/Untitled.png)

2NF

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b5560f9b-3408-48b7-849c-c3e769c0ba43/Untitled.png)

3NF

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a94e6a31-24a2-4b77-a039-ddda9ce1b177/Untitled.png)

# Synthesealgorithmus

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1e0c583a-b79c-44bf-9be2-21fbd269bfa8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/05242611-9bbf-41ef-ba97-d0fb60600b1f/Untitled.png)

# Datenbankanfragen optimieren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ce9e74b3-921b-4d86-8986-20eaa634c74a/Untitled.png)

# UTF-Umwandeln

### UTF-8 to UTF-32

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b7ebe072-5cbf-42c6-b500-4dea3f507c55/Untitled.png)

a,b,c streichen und auf 4 byte auffüllen

### UTF-32 zu UTF-16

Alle führende Nullen streichen bis 21 bits

minus 000010000000…

ersten 10 an high hängen un dletze an low

High Surrogate := 110110

Low Surrogate := 110111

### UTF 32 zu UTF 8

# Programmierer

## Relationale Algebra

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8bd42162-af65-40f7-a005-a0253aa4d2f8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a2d97ace-4ddd-4031-badd-1077aab21ac0/Untitled.png)

## SQL

Tabelle erstellen und Form anpassen (DDL)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8f76a427-06ea-4ded-957a-96a3203910a9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5dce8057-7911-4c1f-b9b6-1e7577004f11/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cca363f0-4347-4ccc-989f-109e68e8d204/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/33056613-2d58-45ff-9f1b-c03165fd6e6f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/43b1111c-0050-437a-bd50-a2030b11ea9d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0ba0a4f1-8e54-4c4b-91bd-6d83685cd9c5/Untitled.png)

Zeilen auswählen und abändern

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2d11828a-87e4-4d34-8d3e-8f07494d72bf/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5789b7c1-f128-4879-b065-0e402f02a00d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/355c4a43-e6fe-4189-b68a-124f6b0d4e2d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3072ed6b-7e65-419e-82c7-a670d7922e38/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/247ea7cf-c0ea-4c8a-b636-58d5120b2cfe/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/66b42500-a10c-4f77-9642-c414597ad926/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3db56f8d-60be-498e-b3e9-b8edc293775f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4f27031a-d810-422f-a009-b49c1bfad9f3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3183a445-1e08-4d71-95c6-d52dc98b2fd9/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9ebe0683-653b-4d6b-8470-31f66bde1a7a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ecddffd1-2162-4b2d-a6a7-5051992aa476/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/162f57ac-13ca-4097-817d-b0a03b7d7092/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ecfb553a-e53e-4b75-b657-13e12e5a1e17/Untitled.png)

<> ist ungleich

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2c62af58-0dd2-4c66-94e1-210ac9a25618/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7bfa0e0c-f9a6-43bf-b408-7a1c6ebab23f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3cd4fdd7-73f9-437c-98a6-09c0debc8604/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a78b3dcc-5446-456b-a0c0-8073efdc77e3/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/99c9eef7-b9ab-446a-bbb7-c2985fed6e7d/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c957ec2d-4bdb-467b-a0e3-fc2c41f5a1c1/Untitled.png)

### Erweiterte DML und DQL

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/e00547b8-232b-4a20-8c4d-0e35a78dd5aa/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8c5141a2-29a0-4e56-b13c-f453b1dfd990/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/8f62c2e4-85b2-4467-8636-c82127f67d68/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4073143e-19d7-4cf4-84bb-81b386132140/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6d21ff71-6af0-4ce7-b4c1-929eefd52778/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/3867b586-451d-405b-8a8f-5b8fa3e7eb11/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0374bbf4-1991-47bf-a4e6-df94b49773b8/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c2848563-86f1-4efe-adc1-6571cad159ae/Untitled.png)