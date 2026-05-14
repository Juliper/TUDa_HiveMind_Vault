---
title: CSS
aliases:
  - Computersystemsicherheit
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

## Einführung & Motivation

## Safety vs. Security

Safety und Sicherheit können sich gegenseitig behindern (z.B. Notausgang)

## Safety (Betriebssicherheit)

- Schutz gegen Fehler/Unfälle
- unabsichtlich (von benutzer)

→ Verifikation, Testen hilft

## Security (Angriffssicherheit)

- Schutz vor Angreifer
- bad intend

→ Verifikation und Testen hilft wenig

## Sicherheitsprinzipien

## Sicherheitseigenschaften

- Vertraulichkeit von Daten/Nachrichten
- Anonymität von Benutzern
- Integrität von Daten/Berechnungen
- Authentizität von Dateien
- Verfügbarkeit von Diensten

## Sicherheitsprinzipien

- Kenne die Angreifer (beeinflusst Maßnahmen)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b816fb68-9337-4336-893c-9fc5ecbbf674/Untitled.png)
    
    - Rechtzeitiges erkennen schwierig (Angreifer kann unbemerkt bleiben)
    - Angreifer kann System (BS, HW, …) kennen und Schwachstellen ausnutzen
    - Cyberkrimialität immer mehr professionalisiert
- Menschen machen Fehler
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/591b843f-11ea-4f44-88b4-29e62dcdc1bf/Untitled.png)
    
- Wirtschaftliche Faktoren beeinflussen Sicherheit
    
    - Organisierte Krimminalität nimmt zu
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2d3f9afe-96db-4765-8717-34396343819a/Untitled.png)
    
- Detektieren falls nicht verhinderbar
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1b6b5133-7ba3-498d-b721-78e61f816b30/Untitled.png)
    
- Defense in Depth: Mehrere, verschiedene Sicherheitsmaßnahmen als Schichten
    
- Fail-safe Standards (Gerät geht in “sicheren” Zustand wenn etwas schiefgeht)
    

## Einführung in die Kryptographie

## Ziele der Kryptographie

## Ziele von Kryptographie

- Vertraulichkeit: Angreifer kann Inhalt der Nachrichten nicht lernen
- Integrität: Angreifer kann Nachricht nicht ändern, ohne das Änderung bekannt wird
- Authentizität: Angreifer kann nicht behaupten, dass eine Nachricht von Alice kam, die diese nicht gesendet hat

## Bausteine von Kryptographie

- Kurzer Schlüssel: Kryptoverfahren verwenden zufällig gewählten, kurzen Schlüssel (leicht zu schützen, zu erzeugen und austauschen)
- Symmetrische Kryptographie: Alle Nutzer verwenden gleichen Schlüssel
- Asymmetrische Kryptographie: Öffentlicher und geheimer Schlüssel
- Ein Kryptoverfahren soll sicher bleiben, selbst wenn der Angreifer den Kryptoalgorithmus kennt

## Klassische Chiffren

## Verschlüsselung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/40f99c3e-5ee3-4a9b-9b54-ee4f1cf6948c/Untitled.png)

- Shift-Chiffre
    - Schlüssel k ist die Anzahl der Shifts (bei k=3 A → D)
    - Mit Brute-Force-Angriff lösbar
    - Auch mit Buchstabenhäufiigkeit lösbar
- Substitutionschiffre
    - Jeder Buchtstabe der Eingabe wird auf einen anderen gemapped
    - Vigenère Chiffre
        - Schlüssel mit beliebiger Länge der angibt wie Buchstaben geändert werden soll
        - Wird wiederholt damit zu Plaintext passt

## Ansätze der modernen Kryptographie

1. Formale Definition
    1. Ziel des Angreifers: z.B. bei Verschlüsselung sollte Angreifer nichts über Klartext lernen
    2. Angreifermodell: Was kann der Angreifer tun und sehen (z.B. Angreifer sieht nur Chiffretexte)
2. Konstruktion
    1. z.B. Konstruktion komplexer Kryptoverfahren aus einfachen Kryptoprimitiven
3. Sicherheitsbeweis
    1. Annahme hält → Kryptoverfahren ist sicher gemäß der formalen Definition (z.B. zahlentheoretische Annahme)
    2. Reduktionsbeweis: Angreifer gegen Kryptoverfahren → Annahme hält nicht

### Kryptoprimitive

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/beb77838-704d-4854-83a0-c2aea2e8279d/Untitled.png)

## Symmetrische Kryptographie

## Definition von symmetrischen Chiffren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1eac0224-430b-4b2a-a748-42dbc42252d0/Untitled.png)

- Nur einen Schlüssel bzw. für jedes Parteienpaar einen
- Bei n Parteien $\frac{n \cdot (n-1)}{2}$

### Korrektheit

- Die Entschlüsselung eines gültigen Chiffretexts resultiert in die original verschlüsselte Nachricht
- Dec(k, Enc(k, m)) = m

### Effizienz

- Verschlüsselung und Entschlüsselung sind effizient

## Sicherheitsbegriff für symmetrische Chiffren (IND-CPA)

### Ziel des Angreifers

- Naive Option: Angreifer will Schlüssel k lernen
- In der Kryptographie: Angreifer lernt etwas neues über m

### Angreifermodelle

- Angreifer lernt nur Chiffretexte (known ciphertext attack)
- Angreifer lernt Paare von Klartexten/Chiffretexten (known plaintext/ciphertext attack)
- Angreifer wählt Klartexte und lernt zugehörige Chiffretexte (chosen plainext attack)

### SICHERHEITSSPIEL (IND-CPA)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/377a198c-6aa4-4072-9997-f5c9907b6b73/Untitled.png)

Wenn Verfahren IND-CPA sicher ist:

- effizienter Angreifer kann b nur raten (1/2 wahrscheinlichkeit)
- c* bietet keine zusätzlichen Informationen
- deterministische Verschlüsselung kann nicht IND-CPA sicher sein

## OTP Verschlüsselung

### One Time Pad

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c85b48c9-97e5-4069-95f7-76442e451d1e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/230e61b7-1b70-4a37-80cf-cc617890a8e5/Untitled.png)

Nachteile:

- Schlüssel kann nur einmal benutzt
- Schlüssel ist so lang wie Nachricht
- Sicherheit nur im beschränkten Angreifermodell (kein Zugriff auf ciphertext)

## Blockchiffren (DES, AES)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cdc06748-a2c5-4ab6-ac9f-dcfe72cd316d/Untitled.png)

- Nicht IND-CPA sicher, weil Verschlüsselung deteministisch
- Werden daher nicht direkt für Verschlüsselung verwendet
- Nachrichten können nicht beliebig lang sein
- Schlüssel wiederverwendbar im gegensatz zu OTP

### DATA ENCRYPTION STANDARD (DES)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6e38eda4-6948-4f95-b855-ea8c25a047b1/Untitled.png)

weil nur 56 bit schlüssel bruteforce möglich

### ADVANCED ENCRYPTION STANDARD (AES)

- Schlüssel-Größe: 128, 192 or 256 bit, Block-Größe: 128 Bits
- Gilt als ungebrochen
- Brute Forcee auf modernen Chifren mit Schlüsseln ≥ 128 Bits unmöglich

### Angiffe in der Praxis

Seiten-Kanal-Angriff

- Geräte bei Ent- / Verschlüsselung beobachten
- Zeit und Stromverbrauch messen

Fehlerangriff

- Fehler (durch Laser) erzeugen und Veränderung beobachten

## Modes of Operation

### ELECTRONIC CODE BOOK (ECB) MODUS

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/a957fe50-c460-43b0-9b3e-9c633ef94eec/Untitled.png)

Ist nicht sicher weil deterministisch (M1 = M2 → C1 = C2)

### CIPHER BLOCK CHAINING (CBC) MODUS

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/66b808f6-a64f-4544-b6bf-f652bfafa171/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/17afe90b-d5d5-4107-8bf7-dfac632ddecb/Untitled.png)

Sicher da nicht deterministisch (M1 = M2 → C1 != C2)

### COUNTER MODUS (CTR)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d18dc4cb-f495-4fd9-8aca-3196c9054f28/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/215eceab-7fc0-4f2c-b89a-04221a108c13/Untitled.png)

### Vergleich

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0b4f4477-62a2-4d80-a9e3-071c61b76cc5/Untitled.png)

## Hashfunktionen

Bildet von großer Definitionsmenge auf kleinen Bildbereich ab

### Sicherheitsdefinitionen

- Preimage resistance
    - Gegeben h ist es schwer m‘ zu finden, so dass H(m‘) = h
- Second Preimage resistance
    - Gegeben h und H(m) = h, ist es schwer m’ ≠ m zu finden, so dass H(m‘) = h
- Collision resistance
    - Finde m’ ≠ m mit h := H(m’) = H(m)

### Beispiele

- SHA-1 gebrochen
- SHA-256
- SHA-3
- Blake3

## Message Authentication Codes (MACs)

Da Verschlüsselungen keine Integrität sicherstellen MACs

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5431400f-80ad-4d59-bf44-3fea58d121f9/Untitled.png)

Sicherheitsdefinition: Angreifer kann keinen validen Tag t für m erzeugen

### Arten von MACs

Informationstheoretisch sichere MACs → nicht effizient für Authenfizierung

Komplexitätstheoretisch sichere MACs

- Für Nachrichten mit fixer Länge
- Für Nachrichten mit beliebiger Länge CBC-MAC und HMAC

### CBC-MAC

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/fb354a7c-daf3-40d5-a843-b26f2999ca78/Untitled.png)

### HMAC

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7ab80499-d0e4-4e23-b94e-6aba2d76e540/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b38738a3-d2bf-44e1-888c-253dd34dc57e/Untitled.png)

## Authentifizierte Verschlüsselung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/caec4d28-7c1a-4fef-95e1-63240d20c9b2/Untitled.png)

## Asymmetrische Kryptographie

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ff0984bc-9772-4381-8905-e8879461779a/Untitled.png)

- Ein Schlüsselpaar pro Partei
- Bei n Parteien n Schlüssel

## Vor- und Nachteile

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/30022c75-fcaa-4a57-9a54-5bf069b7f1f3/Untitled.png)

## RSA

Ist nicht IND-CPA sicher weil determinsitisch (RSA OAEP fügt zufälligkeit hinzu)

Verschlüsselungsverfahren ist homomorph: Enc(pk, m0) * Enc(pk, m1) = Enc(pk, m0 * m1)

1. Wähle zwei Primzahlen p,q mit p ≠ q
2. Berechne N = pq
3. Wähle e > 1 sodass ggT (e, phi(N)) = 1
4. berechne d = e^-1 mod phi(N) bzw. e * d = 1 mod phi(N) bzw. eek e x + phi(N)y = 1
5. phi(N) = (p - 1)(q - 1)
6. c = m^e mod N
7. n = c^d mod N

### RSA Annahme

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/95263534-f8d4-4f0b-a1db-48d534656ce6/Untitled.png)

## Elgmal

Annahme: Diskreten Logarithmus zu finden ist hart für geeignete Gruppe 𝔾.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0b5e6306-2382-4aab-8a1f-504362df6105/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d102a26c-b1a2-4065-839e-cc2e791a27f7/Untitled.png)

## Protokoll für Schlüsselaustausch (DIFFIE-HELLMAN)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/19aab45c-afea-4d8d-b33e-e37474f8791e/Untitled.png)

## Hybride Verschlüsselung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/d2806186-3f27-44be-a62f-849de15e0458/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/0e870429-e140-4fc7-9e18-83a44204d45a/Untitled.png)

## Integrität mittels Signaturen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/433b0cdb-0fd7-44f7-847d-077691cc2899/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ade6aa38-ee59-433b-b869-fb03ad8011c2/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/20447338-866f-4045-a790-802c4934d4f3/Untitled.png)

## SIGNATUREN: KONKRETE VERFAHREN

RSA-basierte Signaturen und Diskreter-Logarithmus-basiert (alles Hash and Sign)

### Hash and Sign

Signieren beliebig langer Nachrichten durch hashen

### RSA Signieren

Geg.: privater Schlüssel sk = (N, d)

1. Nachricht m hashen H(m)
2. Hashwert auf RSA Länge kodieren
3. Signaturverfahren: Encode(H(m))^d mod N

### RSA Verifizieren

Geg.: öffentlicher Schlüssel pk = (N, e)

1. Nachricht m hashen H(m)
2. Hashwert auf RSA Länge kodieren
3. Vergleiche Sigantur s^e mod N mit Encode(H(m))

## Sicherheitsspiel (EU-CMA)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1c9d59ee-0909-4ed3-b109-c9c4d017e9bb/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c2418221-dce8-418d-a099-f95c207e1bbf/Untitled.png)

## Zertifikate und Einblick in Public Key Infrastruktur

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/be45aa49-3f63-40b2-936e-23f20bb8d129/Untitled.png)

### Inhalt von Zertifikat

- Inhaber
- Aussteller
- Gültigkeitsdauer
- Informationen zum pk des Inhabers (verwendeter Algorithmus)
- Signaturwert

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/03227790-9f56-41aa-8750-f026078ff076/Untitled.png)

## Modulare Arithmetik

## Authentisierung und Autorisierung

## Begriffsunterscheidung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cd34f092-1430-40c4-9376-b6e5b9727163/Untitled.png)

- Identifizierung ≠ Authentisierung

## Authentisierung

### Authentisierung: Passwort vs. Chipcard vs. Biometrie

||Passwort (Was man weiß)|Chipkarte (Was man hat)|Biometrie (Was man ist)|
|---|---|---|---|
|Vorteile|einfach zu ändern, einfach mitnehmbar|einfach mitnehmbar, nicht leicht duplizierbar|nicht übertragbar, individuell|
|Nachteile|vergessbar, leicht duplizierbar|einfach übertragbar, stehlbar|leicht fälschbar, unveränderbar, Privacy Problem|

### Passwort leak sicher machen

- Verschlüsselung (schlecht)
- Hashen (schlecht) → Rainbow tables
- Salted Hashing (gut) → besser mit individuellen salt für jeden user/salts geheim halten/ hashfunktionen iterieren (Angreifer hat wahrscheinlich keinen Rainbow Table mit passendem Salt)

### Phishing

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2ec90d92-4f2b-4974-90a7-ae710a6dfee0/Untitled.png)

## Tokens

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/5a1e3bd3-18d8-4f85-9fdf-3b51f05da895/Untitled.png)

### Ynamische Tokens

- zufällig Challange wird gestellt
- Token wird mittels Geheimnis und Challenge erstellt
- Replay Attack nicht möglich

### Implementierung mit Signaturen oder MACs

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/f3673e37-2813-4931-98f9-dc09517a94cf/Untitled.png)

### Implementierung per Verschlüsselung

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/19d1a118-a363-41e6-9303-28c7882c7879/Untitled.png)

## CAPTCHAs

Completely Automated Public Turing test to Tell Computers and Humans Apart

- Sollen DoS Angriffe verhindern

## Autorisierung

Soll Integrität und Vertraulichkeit schützen indem Zuhriff kontrolliert wird

### Discretionary Access Control (DAC)

- Eigentümer legt Zugriffsrechte fest
    
- Access Matrix Model
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/4feed22f-dda2-4cb0-a4c3-6e46d4657606/Untitled.png)
    
    - Sehr einfach zu implementieren und zu nutzen
    - Grundlage vieler BS
    - keine formale Garantien für Informationsfluss
    - Kann dynamische Rechte schwer abbilden
    - Beschrnkter Zugriff z.B. ändern des eigenen Passworts schwierig zu implementieren
- Access Control List
    
    - Spaltenweise Speicherung der Zugriffskontrollmatrix
    - Vorteil: Rechte an einem Objekt sind effizient bestimmbar
    - Nachteil: Schlechte Skalierbarkeit bei dynamischen Subjektmengen

### Mandatory Access Control (MAC)

- Autorität setzt Zugriffsrechte fest

### Role-based Access Control (RBAC)

- Zugriffsrechte durch Rolle festgelegt

### Attribute-based Access Control (ABAC)

- feinere Zugriffsrechte gemäß logischer Formel

### Bell-la Padula Modell

- formales Sicherheitsmodell
- Regelt die Informationsflüsse in einer Hierarchie, um Vertraulichkeit zu gewährleisten
- No-Read-Up Regel
- No-Write-Down

## Netzwerksicherheit *

## Schichtenmodell

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/06a64d46-a7bf-4b6d-a1d6-4b289262ddc3/Untitled.png)

### Link Layer

- Übertragung zwischen zwei Punkten inklusive Konvertierung in physikalische Signale innerhalb eines LAN (Local Area Network)
- Ethernet, Wi-Fi
- Identifikation über MAC Adresse 6 Byte (3 Bytes Hersteller, 3 Bytes Gerätespezifisch)

### Internet Layer

- Sendung von Paketen (Sender- & Zieladdresse, Daten) von jedem Quellgerät zu jedem Zielgerät
- Kommunikation über verschiedene LANs hinweg
- Internet Protocol (IP) mit IPv4/6
- Pakete können verloren gehen, Fehler aufweisen und falsche Ordnung

### Transport Layer

- Ende-zu-Ende Kommunikation im Internet für verschiedene Dienste
- Verschiedene Anwendungen auf Host mit Ports

**TCP**

- Verbindungsaufbau
- korekkte Pakete und richtige Ordnung
- langsam

**UDP**

- Verbindungslos
- unzuverlässig
- schnell

### Application Layer

- Funktion für netzbasierte Software (nicht die Anwendung selbst)
- Adressierung der Anwendung mittels Ports
- HTTP(S)/FTP/SMTP

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ede484ab-8690-46b0-b9e8-545839449f63/Untitled.png)

## Link Layer Angriff

### Paket Sniffing

- Bei Broadcast Kommunikation einfach zuhören

### MACs als Zugriffskontrolle

- MAC über Software ändern
- Umgeht MAC Filterung

### MAC Flooding

- Switch mit MAC Adressen fluten
- Weiterleitungstabelle wird geleert
- Switch miss broadcasten

### ARP Spoofing

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cac520e7-8deb-4e13-bd2c-aa4d8cf84989/Untitled.png)

- Zum spoofen einfach Eve muss eunfach schneller Antworten
- Durch Monitoring erkennbar (spoofing führt zu vielen Antworten)
- Kein Integritätsschutz (Verschlüsselung als gegenmaßnahmen)

## Intetnet Layer Angriff

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/81b2d6ad-22cc-4c37-af79-730e0f4ebbe1/Untitled.png)

### DHCP Spoofing

- Angreifer schickt statt DHCP-Server eigenes Angebot

## BGP Hijacking

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/9a4a0da7-92e0-4ccc-ace2-f597b7899cb8/Untitled.png)

## Internet Control Message Protocol (ICMP)

Internet Control Message Protocol (ICMP) für Informations- und Fehlermeldungen des Netzwerks • Typischerweise nicht für Endnutzer (außer ping und traceroute)

### Ping of Death

sende spezielle miskonfigurierte (z.B. zu große Payload) ICMP-Nachrichten, die zum Absturz des Servers führen (DoS)

## Transport Layer *

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/ab7e4a2a-8166-4f52-9b31-3bc02ef0eed0/Untitled.png)

### TCP Hijacking

- Bestehende TCP Sitzung manipulieren

### TCP Flooding

## Application Layer *

### Transport Layer Security (TLS)

- Vertraulichkeit: Angreifer kann Kommunikation nicht mitlesen
- Integrität: Verhindert Abänderung der Kommunikation (z.B. Replay Angriffe)
- Authentizität: Client kommuniziert mit dem legitimen Server
- HTTPS

## TOR für Anonymität *

## WLAN Sicherheit *

## Websicherheit

## SAME-ORIGIN POLICY

- JavaScript auf einer Webseite darf nicht auf Dokumente mit anderer Herkunft (Origin) zugreifen
- Origin ist Protokoll, Domain und Port

## Cookies

- Ermöglicht das behalten von Zuständen über mehrere HTTP anfragen hinweg
- Browser speicher Cookies

## CROSS-SITE REQUEST FORGERY (CSRF)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/2376cacc-dbb4-400a-834a-a205d5f1946a/Untitled.png)

Gegenmaßnahmen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/902d39bd-3977-4b3a-b6c2-175668f5e7e0/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c030b252-0611-43d1-938b-91be8d78acc8/Untitled.png)

## CROSS-SITE SCRIPTING (XSS)

Einbettung von bösartigem JavaScript Code auf einer Webseite, die vom Nutzer besucht und in Browser ausgeführt wird

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cdd32345-36af-4fc0-a02c-ac76455c9598/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/abc09f17-9f40-44f4-95f8-e207abd2499d/Untitled.png)

## ONTENT SECURITY POLICY (CSP)

HTTP Header mit dem Webserver dem Browser mitteilt, welche dynamischen Ressourcen (z.B. JavaScript) erlaubt sind

Whitelisting > Blacklisting

## SQL Injection

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/88515643-0c36-4880-9c9a-c8a85ae8c017/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/cd8c03db-d5e8-408e-a8fd-daae1384a49e/Untitled.png)

## Systemsicherheit

## Malware

Beispiel: Flame malware

### Wurm

- Software die sich über Netzwerk exponentiell verbreitet
- Beinträchtigt häufig nur Leistung

### Virus

- Böswillige Software die sich verbreitet
- hängt sich an andere Software/Systeme
    - Insertion phase
    - Execution phase
    - Replication
- verändert Aussehen (Polymorphie)

### Polymorphic Virus

- Virus ist erst verschlüsselt und wird dann entschlüsselt
- Code hat daher immer andere Signatur und kann schwer erkannt werden
- Code für Entschlüsselung → Schlüssel → Verschlüsselter Virus Code → Verschlüsselter Virus Code für Replikation
- Verbreitet sich nicht selbst

### Metamorphic Virus

- Erzeugt bei replizieren eine sematisch andere Version
- Gleiche high-level Aktion aber kleine Abweichungen
    - add 0 to regsiter
    - sub 0 usw…
- Virus Code → Rewriter
- Kann am Verhalten(-muster) erkannt werden
- Virus kann erst nach langer Zeit ausgeführt werden oder stoppt ausführung falls Analyse tool erkannt

### Trojaner

- repliziert sich in der Regeln nicht selbst
- Ransomware: verschlüsselt Daten und fordert Lösegeld (WannaCry)
- Scareware: Gibt sich als Virenscanner aus der angeblich Viren findet und gegen Geld entfernt
- Suburst

### Verbreitungsarten

- klassich: Anhang an EMail oder Programm installation / nur vertrauenswürdige Quellen akzeptieren
- drive-by-download: Bei Besuch von Websiten / Deactivate Scripts, Sandboxing
- physisch: durch infizierte Tokens / nur vertrauenswürdige Quellen akzeptieren

### Schutz vor Viren

- Reaktiv
    - Systemscan, Real-Time Detection
    - Prüfe ob Viren Signatur gefunden wird
- Proaktiv
    - Activity Monitoring: prüft auf Virentypisches Verhalten

## C Programm ausführen

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/6d717c3b-987b-4cb6-8802-b47f049a4dbd/Untitled.png)

- EBP-Register („Basiszeiger“) zeigt auf den Anfang des aktuellen Stack Frames
- ESP-Register („Stackzeiger“) zeigt auf das untere Ende des aktuellen Stack-Frame
- EIP-Register („Befehlszeiger“) speichert die Adresse des gerade ausgeführten Maschinenbefehls im Code Segement

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/38403426-defe-468b-91bc-f40c3fb66764/Untitled.png)

## Buffer Overflow

## Anfälliger Code

- gets (schreibt so lange Bytes, bis die Eingabe einen Zeilenumbruch ('\n') enthält, nicht wenn das Ende des Arrays erreicht ist!)
    
- Daten werden außerhalb von Arrays geschrieben
    
- Führt zu Datenmanipulation
    

1. Memory Safety Schwachstelle (z.B. Buffer Overflow)
2. Schreibe Shellcode des Angreifers an eine bekannte Adresse des Speichers
3. Überschreibe den RIP mit der Adresse des Shellcodes
4. Springe aus der angegriffenen Funktion zurück
5. Führe Shellcode des Angreifers aus

### Stack Smashing

- Auf Stack sind: lokale Variablen, Funktions Argumente, Gespeicherter Framezeiger (SFP), Rückgabe Instruktions Zeiger(RIP)
- Überschreibe RIP (nach Programm zu unserem)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/b5ad8321-3ca5-4919-8fe6-508f5bbedb73/Untitled.png)

Stackframe := Return Adresse (4 Byte) + Base Pointer (4 Byte) + lokale Variablen der Funktion (int = 4 bytes)

### Integer Overflow

- Integer läuft über und fängt wieder von vorne an

### Gegenmaßnahmen

- Kann alles durch Memory Safety Programmiersprachen verhindert werden (Java, Python, Go, Rust) (sind aber meistens ineffizienter)
- Defensives Programmieren: Gültigkeitsprüfung (nullptr)
- Gefährliche Operationen wie gets vermeiden
- Pre- / Postkonditions und Invarianten verwenden
- Testen
- Stack Canary: Vor RIP und SFL canery vlaue speichern, wenn dieser verändert wird dann Porgramm beenden
- ASLR (Address Space Layout Randomization) → Spraying (Schadcode großflächig verbreiten)

## Seitenkanalangriff

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/7e219ad9-767c-46f0-bf9b-1f06cd56337f/Untitled.png)

### CACHE SIDE-CHANNEL ANGRIFFE

- Cache manipulieren

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/01643b48-8949-4387-ac63-ccc685555fbe/Untitled.png)

# Klausurfragen

- Hashfunktionen sind besser als Schlüsselableitungsfunktionen zum Passwortspeichern
- Was ist Mehrfaktorauthentifizierung?
- Wovor schützt TLS?
- Wovor schützt Passwort Hashing?
- Wovor Schützt Passwort Hashing+Salting?
- Welche zwei Sachen müssen beim Challenge-Response Protokoll für die Nonces gelten?
- Nennen Sie drei Schutzziele und jeweils ein Beispiel für ein kryptographisches Verfahren mit dem dieses erreicht werden kann
- OTP beschreiben und warum es nicht in der Praxis angewandt wird
- XSS reflected Attack anhand selbstgemachter Skizze beschreiben
- Welches Schutzziel wird durch Bell-LaPadula no write down Regel erreicht?
- Welches Schutzziel wird mit Challenge Response erreicht?
- Welches Schutzziel wird mit Access Control List erreicht?
- Was sind statische und dynamische Token und jeweils Beispiele nennen
- RBAC Zugriffsmatrix
- Kerberos Overpass the Hash beschreiben
- Bewerten Sie folgende Aussage: Mit TLS kann ich mir sicher sein, dass der andere Server vertrauenswürdig ist.
- Einen Vorteil und einen Nachteil von assymetrischer Kryptographie gegenüber symmetrischer nennen.
- Ein Angreifer ist in einem WLAN mit anderen Personen verbunden. Kann er einen DNS-Poisoning Angriff durchführen?
- Bestimmen Sie in der zyklischen Gruppe Z^x_11 den diskreten Logarithmus von 4 zur Basis 5. Zeigen Sie, dass Ihr Ergebnis korrekt ist
- Erläutern Sie die Bestandteile eines symmetrischen Kryptosystems (M, K, C, e, d)
- Was soll bei einem symmetrischen Kryptosystem für unterschiedliche Schlüssel k1 != k2 aber gleiche Nachricht m gelten?
- Dynamische und statische Token erklären plus jeweils Beispiel
- TLS-Zertifikat, Challenge Response Protokoll und No-Write-Down und No-Readup-Regel (Bell La Padula) den Schutzzielen zuordnen
- bedeutet ein TLS Zertifikat, dass der entsprechende Server wirklich vertrauenswürdig ist?
- Was ist das besondere an Polymorphen Viren?
- Nennen sie eine Technik um polymorphe Viren zu erzeugen
- Wieso sind polymorphe Viren schwerer zu erkennen als "normale" (oder so ähnlich)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/c9790774-d1ad-4553-841c-49e676d110c6/Untitled.png)

## Malwarearten

- Trojaner
- Ransomware

## Angriffsarten

- Smurf Angriffe
- Checkpointing

## Algorithmen

- eea (ggT bestimmen und diskreten Logarithmus)
- Blockchiffre ausrechnen (CBC)
- Blockchiffre Modes of Operation
- Was für Anforderungen gibt es an ein symmetrisches Kryptosystem für _k_1≠_k_2 und _m_1=_m_2?
- RSA berechnen / Signatur
- Wie kann man RSA und Diffie Hellmman Angriff (mathematische Schwierigkeiten)

## Netzwerk

- DHCP Funktion erklären
- DHCP Pakete erstellen
- DHCP Snooping (auf welcher Schicht?)
- OSI/TCP Schichten erklären
- Was ist DNS
- DNS Resource Record erklären
- Schutzziele von DNSSEC

## BGP

- Sub und Same prefix Hijacking und Folge
- Autonom System Aufgabe (IP Präfix bestimmen)
- BGP Schutzmechanismen
- BGP Hijacking durchführen durchführen (IP-Adresse und welche AS der Attacker AS haben muss um allen traffic von AS3 abzugreifen, der Attacker ist AS2 und mit AS1 und AS3 verbunden, AS3 mit AS2 und AS1 und AS1 (mit geg. IP) mit AS2 und AS3)

## **RBAC**

- Hasse Diagramm für A bis E erstellen
- Bestimmen ob, eine Visualisierung eine partielle Ordnung ist und falls ja was sagt dies über die Rechte von A und B aus.

## HTML

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/1da51d07-7f68-4603-95ee-36c2b0f54d24/1b4279d4-34ca-482c-9a6c-f014f9665746/Untitled.png)

XSS durchführen

## SQL

- Befehle schreiben
- SQL Injection
- Wie abwehren

## Buffer Overflow

- Selbst Buffer-Overflow durchführen