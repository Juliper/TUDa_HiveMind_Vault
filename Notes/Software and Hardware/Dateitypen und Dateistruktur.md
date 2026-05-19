---
title: File Types and Structure
aliases:
  - Dateitypen und Dateistruktur
tags:
  - operating-systems
  - file-systems
description: "Types of files, their internal structure, access methods, and attributes in operating systems"
draft: false
---

> [!NOTE] Definition
> A file is an abstraction of data blocks on disk. A file system defines how files are stored, organized, and accessed.

## File Types

| Type | Description |
|------|-------------|
| **Regular files** | Data storage (text, binary) |
| **Directories** | Structures containing references to other files |
| **Character special files** | Model I/O devices (printer, mouse, screen) - stream-based, not addressable |
| **Block special files** | Model storage devices (disks) - block-based read/write |

## File Structure

| Structure | Description |
|-----------|-------------|
| **Byte-oriented** | Sequence of bytes (most common: UNIX, Windows) |
| **Record-oriented** | Sequence of fixed-length records |
| **Tree structure** | Hierarchical organization of records |

## Access Methods

- **Sequential access**: bytes read in order only
- **Random access**: bytes can be read at any position

## File Naming

- UNIX: case-sensitive, file extensions are optional
- Windows: case-insensitive, extensions are significant

## File Attributes

Owner, permissions, creation/modification/access timestamps, size, hidden/archive/temporary flags.

## File Operations

Create, delete, open, close, read, write, append, seek, get/set attributes, rename.

## Directories

A directory is a file that contains a collection of files, organized hierarchically.

- **Absolute path**: from root (e.g., `/usr/bob/test`)
- **Relative path**: from current directory (e.g., `./test`)
- `.` = current directory, `..` = parent directory

### Directory Operations

Create, delete, opendir, closedir, readdir, rename, link, unlink.

### Shared Files

- **Hard links**: direct reference to the file's i-node (same file, multiple directory entries)
- **Soft links (symlinks)**: pointer to the file path (resolving the link can add overhead)

## Related Concepts

- [[Disk Partitions]]: how the disk is organized
- [[File Allocation-Typen]]: how files are stored on disk
