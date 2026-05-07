---
title: Mitmachen
---
Du willst beitragen? Nice! Hier erfährst du wie.

## Zugang bekommen

**Option 1 - Collaborator werden:** Meld dich einfach bei mir (siehe Kontakt unten) - ich füge dich als Collaborator hinzu und du kannst direkt pushen.

**Option 2 - Fork & Pull Request:** Forke das Repository, mach deine Änderungen und stelle eine PR.

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
   * Alle Änderungen werden nach einen kleinen Verzögerung auf der Webseite veröffentlicht - [Quartz](https://juliper.github.io/TUDa_HiveMind_Quartz/).

---
## Struktur
Die Grundidee von HiveMind ist es, die Grenzen zwischen Modulen aufzureißen und so intermodulares Lernen zu ermöglichen, mit dem Ziel, tief verwurzeltes Verständnis von Themen zu fördern.

Der Vault ist dabei hierarchisch aufgebaut. Die Ordnerstruktur wird verwendet um `Notes` und `Module` nach Themenschwerpunkte zu organisieren. Die Zuordnung nach CP, Pflicht oder Wahlbereich usw. geschieht über Frontmatter-Tags.
### Atomic Notes (`/Notes`)
Alles beginnt bei einer **Atomic Note** - eine kurze, präzise Erklärung eines einzelnen Konzepts. Sie kann beliebig auf andere Notizen verweisen. Atomic Notes leben wie in einem Zettelkasten frei im `Notes`-Ordner.
### Modul-Notizen
Am Ende steht die eigentliche Notiz zu einer Vorlesung oder einem Modul. Sie verlinkt auf bereits vorhandene Atomic Notes oder legt neue an und verweist auf diese. Das reduziert Redundanz: Hat jemand z.B. tolle Notizen zu Reihen erstellt, können diese sowohl in Mathe 1 als auch Mathe 2 einfach verlinkt werden, statt alles doppelt zu schreiben.

---
## TODO / Roadmap

Offene Verbesserungspunkte für die Vault-Struktur (Ergänzungen sind wilkommen):

- [ ] **Aktuelle Ordnerstruktur überdenken** - Die Struktur sollte skalierbar und leicht zu maintainen sein. Ich bin unsicher ob dies auf die aktuelle Struktur zutrifft
- [ ] **Modul/Notiz-Templates verbessern** - Um das Beitragen zu diesem Projekt einfacher zu machen, sollten die templates ermöglichen gut formatierte Notizen zu erstellen. Alle Besonderheiten von github/obsidian flavored markdown sollten gezeigt werden. Auch Erweiterungen wie Mermaid sollten erklärt werden.
- [ ] **Frontmatter-Validierung automatisieren** - Pre-Commit-Hook oder GitHub Action, die `title`, `tags` und `description` als Pflichtfelder enforced.
- [ ] **Konventionen-Dokument anlegen** - kurze `CONTRIBUTING.md` mit Naming-Regeln, Tag-Vokabular (englisch, lowercase, Bindestriche) und wann `draft: true` statt published. Könnte auch mit Templates zusammengeführt werden.

---
## Kontakt

- **Discord:** [Juliper](https://discord.com/users/266008516324491275)