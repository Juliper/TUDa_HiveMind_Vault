---
title: Mitmachen
---
Du willst beitragen? Nice! Hier erfährst du wie.

## Zugang bekommen

**Option 1 — Collaborator werden:** Meld dich einfach bei mir (siehe Kontakt unten) — ich füge dich als Collaborator hinzu und du kannst direkt pushen.

**Option 2 — Fork & Pull Request:** Forke das Repository, mach deine Änderungen und stelle eine PR.

---
## Setup

1. **Repository clonen**
   ```bash
   git clone git@github.com:Juliper/TUDa_HiveMind_Vault.git
   # oder deinen Fork
   git clone git@github.com:XXX
   ```

2. **In Obsidian öffnen**
   - Obsidian starten → "Open folder as vault" → den geclonten Ordner auswählen
   - Fertig! Alle Plugins und Einstellungen sind schon dabei
   - Schau dir auch gerne die Notiz-Templates an, um die Formatierung zu verstehen

3. **Änderungen pushen**
   - Die Git-Extension ist bereits im Vault konfiguriert
   - Links in der Sidebar findest du den Git-Reiter
   - Dort kannst du deine Änderungen committen und pushen

4. **Webseite** 
   * Alle Änderungen werden nach einen kleinen Verzögerung auf der Webseite veröffentlicht — [Quartz](https://juliper.github.io/TUDa_HiveMind_Quartz/).

---
## Struktur
Die Grundidee von HiveMind ist es, die Grenzen zwischen Modulen aufzureißen und so intermodulares Lernen zu ermöglichen, mit dem Ziel, tief verwurzeltes Verständnis von Themen zu fördern.

Die Grundidee von Hive Mind ist es die grenzen zwischen Modulen aufzureisen und somit intermodul Lernen zu ermoeglichen um tief verwurzeltes Verstaendnis von Themen zu foerdern.

Der Vault ist dabei hierarchisch aufgebaut, von grob nach fein:
```
Fachbereich (z.B. Informatik, Mathematik)
└── Studiengang (z.B. B.Sc. Informatik)
    └── Modul-Notiz (z.B. Mathe 1)
        └── Atomic Notes (einzelne Konzepte)
```

### Atomic Notes (`/Notes`)
Alles beginnt bei einer **Atomic Note** — eine kurze, präzise Erklärung eines einzelnen Konzepts. Sie kann beliebig auf andere Notizen oder Topics verweisen. Atomic Notes leben wie in einem Zettelkasten frei im `Notes`-Ordner und werden über Tags und MOCs organisiert. Ein Beispiel-Template findest du im `Templates`-Ordner.

### Topics / MOCs (`/Topics`)
Atomic Notes mit demselben Themenschwerpunkt werden optional in **Maps of Content (MOCs)** im `Topics`-Ordner zusammengeführt. Das erleichtert den Überblick und gruppiert verwandte Konzepte. Ein Beispiel-Template liegt ebenfalls in `Templates`.

### Modul-Notizen
Am Ende steht die eigentliche Notiz zu einer Vorlesung oder einem Modul. Sie verlinkt auf bereits vorhandene Topics oder Atomic Notes — oder legt neue an und verweist auf diese. Das reduziert Redundanz: Hat jemand z.B. tolle Notizen zu Reihen erstellt, können diese sowohl in Mathe 1 als auch Mathe 2 einfach verlinkt werden, statt alles doppelt zu schreiben.

---
## Kontakt

- **Discord:** [Juliper](https://discord.com/users/266008516324491275)