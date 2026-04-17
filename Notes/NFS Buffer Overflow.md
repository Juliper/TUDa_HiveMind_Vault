---
title: NFS Buffer Overflow
aliases:
  - NFS rpc.mountd Exploit
tags:
  - cybersecurity
  - cyberattack
  - buffer-overflow
  - exploit
description: "Klassischer Buffer-Overflow-Angriff auf den NFS-Daemon, ein Paradebeispiel für speicherkorrumpierungsbasierte Remote-Exploits."
---

# NFS Buffer Overflow

**Network File System (NFS)** ist ein verteiltes Dateisystemprotokoll, das über **RPC (Remote Procedure Call)** kommuniziert. Historisch war NFS-Software mehrfach Ziel von **Buffer-Overflow-Angriffen**, da sie als privilegierter Daemon (root) läuft und Netzwerkeingaben verarbeitet.

## Angriffsprinzip

Ein Buffer Overflow entsteht, wenn Eingabedaten die Grenzen eines Puffers überschreiben und dabei benachbarte Speicherbereiche korrumpieren — insbesondere die **Rücksprungadresse** auf dem Stack.

```mermaid
block-beta
  columns 2
  vb["Vor Overflow"]:1       nb["Nach Overflow"]:1
  ra["Return Address"]:1     ra2["⚠ Shellcode-Adresse"]:1
  ebp["Saved EBP"]:1         ebp2["AAAAAAAAAA"]:1
  buf["Buffer (256 Bytes)"]:1 buf2["AAAAAAAAAA  ← Overflow"]:1
```

## Konkretes Beispiel: rpc.mountd

Der Daemon **`rpc.mountd`** (verwaltet NFS-Mount-Anfragen) enthielt in älteren Implementierungen Schwachstellen durch unkontrollierte Nutzung von `strcpy()` / `sprintf()` ohne Längenprüfung.

**Angriffsablauf:**

```mermaid
sequenceDiagram
    actor Angreifer
    participant NFS as rpc.mountd (root)
    participant OS as Betriebssystem

    Angreifer->>NFS: Präparierte RPC-Anfrage (überlanger Parameter)
    Note over NFS: strcpy() ohne Längenprüfung
    Note over NFS: Buffer[256] überschrieben
    Note over NFS: Return Address → Shellcode
    NFS->>OS: Shellcode wird als root ausgeführt
    OS-->>Angreifer: Root Shell
```

## Gegenmaßnahmen

| Maßnahme | Wirkung |
|---|---|
| **ASLR** (Address Space Layout Randomization) | Speicheradressen werden randomisiert → Shellcode-Adresse nicht vorhersagbar |
| **Stack Canaries** | Zufälliger Wert zwischen Buffer und Rücksprungadresse → Overflow wird erkannt |
| **NX/DEP** (No-Execute Bit) | Stack-Speicher ist nicht ausführbar → Shellcode kann nicht direkt ausgeführt werden |
| **Safe APIs** (`strncpy`, `snprintf`) | Verhindert Overflows durch Längenbegrenzung |
| **Minimale Rechte** | Daemon nicht als root ausführen → Schaden begrenzen |

## Einordnung

Buffer Overflows in Netzwerkdiensten waren in den 1990ern und frühen 2000ern die häufigste Klasse von Remote-Exploits. NFS-Schwachstellen dieser Art (z. B. in SGI IRIX, Solaris) wurden aktiv in Worm-Propagation eingesetzt. Heute durch Compiler-Schutzmaßnahmen seltener — aber nicht ausgestorben (vgl. Heartbleed als verwandtes Konzept).
