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


## Vorlesung 5&6 - Parallelism

### Parallel Execution Models & Scheduling
- [[Query Parallelism]]
- [[DBMS Execution Architecture]]
- [[DBMS Task Scheduling]]

### Memory Models & Data Placement
- [[NUMA Architecture]]
- [[Data Partitioning and Placement]]
- [[Translation Lookaside Buffer]]

### Parallel Join Algorithms
- [[Partition-Based Hash Join]]
- [[Radix Partitioning]]
- [[Parallel Hash Table Construction]]
- [[Bloom Filter]]
- [[Parallel Sort-Merge Join]]

## Lecture 6 - Accelerators in the Cloud

### Motivation and Specialized Hardware
- [[Hardware Specialization Spectrum]]
- [[Von Neumann Architecture]]
- [[Instruction-Level Parallelism]]

### Accelerator Architectures
- [[Systolic Array]]
- [[Tensor Processing Unit]]
- [[Application-Specific Integrated Circuit]]
- [[Field-Programmable Gate Array]]

### Case Study: FPGA-Accelerated Data Decoding
- [[FPGA-Accelerated Parquet Parsing]]

## Lecture 7 - Accelerators for DBMSs: GPU

### GPU Architecture and Programming
- [[GPU Architecture]]
- [[CUDA Programming Model]]

### In-Memory OLAP on GPUs
- [[Parallel Reduction and Prefix Sum]]

### Beyond-Memory OLAP on GPUs
- [[GPU Query Execution Models]]
- [[Operator and Data Placement]]
- [[GPU-Direct Storage]]
- [[GOLAP]]

# Quizzes
* [[ADMS - Quiz 1]]