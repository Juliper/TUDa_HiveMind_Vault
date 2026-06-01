---
title: ADMS
aliases:
  - Advanced Data Management Systems
tags:
  - 6CP
  - fb20
  - master
  - wahlmodul
description: Research-oriented course about modern architectures for DBMSs
draft: false
---

# Syllabus

| Moodle       | [Link](https://moodle.informatik.tu-darmstadt.de/course/view.php?id=1960) |
| ------------ | ------------------------------------------------------------------------- |
| Dozent       | Carsten Binning + Zsolt Istvan                                            |
| Prüfungsform | Quizzes + Lab                                                             |
> [!WARNING]
> The courses **InfMan**, **FOMO** and **SDMS** are not mandatory but they are highly recommended prerequisites for this course.

# Lectures

## Lecture 1 - In-Memory Storage

### Motivation and Architecture
- [[Disk-Based DBMS]]
- [[Main Memory DBMS]]
- [[Memory Hierarchy]]
### Storage Models
- [[Row Store]]
- [[Column Store]]
- [[PAX]]
- [[Late Materialization]]
### Data Compression
- [[Lightweight Compression]]
- [[Dictionary Encoding]]
- [[Run-Length Encoding]]
- [[Bit-Packing Encoding]]
- [[Frame of Reference Encoding]]
- [[Delta Encoding]]
- [[Null Suppression]]
- [[PFOR Encoding]]
- [[Query Processing on Compressed Data]]

### Hardware-Conscious Processing
- [[SIMD Processing]]

## Lecture 2 - In-Memory Scan

### Scan Techniques
- [[Vectorized Scan]]
- [[Vectorized Query Execution]]
- [[Predicate Evaluation]]

### Secondary Index Structures
- [[Column Imprints]]
- [[Zone Maps]]

### Compression and Scans
- [[Lightweight Compression]]

## Lecture 3 - Databases and SSDs (Guest Lecture)

### SSD Fundamentals
- [[SSD Architecture]]
- [[Flash Translation Layer]]
- [[SSD Performance Characteristics]]

### SSD Challenges
- [[Write Amplification]]
- [[Wear Leveling]]

### SSD-Optimized Data Structures
- [[LSM Tree]]
- [[SSD-Aware Database Design]]

## Vorlesung 4 - In-Memory Indexes

### OLAP Indexes
- [[Zone Maps]]
- [[Column Imprints]]
- [[CSS-Tree]]
- [[CSB+ Tree]]

### OLTP Index Concurrency
- [[B+ Tree Latch Coupling]]

### Back to SSDs
- [[Pointer Swizzling]]

## SSD Talk - Databases and SSDs

### SSD Fundamentals
- [[SSD Architecture]]
- [[SSD Performance Characteristics]]
- [[Flash Translation Layer]]

### SSD Internals
- [[SSD Garbage Collection]]
- [[Write Amplification]]
- [[Wear Leveling]]

### SSD-Optimized Database Design
- [[SSD-Aware Database Design]]
- [[LeanStore]]
- [[Database I/O Interfaces]]
- [[LSM Tree]]


## Research Papers

### Adaptive Radix Tree (ART)
- [[Adaptive Radix Tree]]

### ART vs Hash Tables (Alvarez et al.)
- [[ART vs Hash Tables]]


# Quizzes
* [[ADMS - Quiz 1]]