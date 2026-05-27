---
title: ADMS - Quiz 1
aliases:
  - ADMS Quiz 1
tags:
  - adms
  - quiz
  - fb20
description: "Collection of all quiz questions for ADMS Quiz 1 preparation (Weeks 1-6)"
draft: false
---

# ADMS - Quiz 1

> [!info] Note
> The actual quiz is **25 points** and lasts **15 minutes**.
> This collection covers all content from **Weeks 1-6**.

---

# A - In-Memory Storage

> [!abstract]- Own Notes
> * What is disk-based DBMS?
> 	* Primary storage is HDD/SSD
> 	* Organized as "slotted" pages
> 	* Uses Ram as in-memory buffer pool for "hot" pages
> * How is Data accessed in disk-based DBMS?
> 	* Using RIDs containing the ID of the Page and the specific Slot inside the page
> 	* Index -> PageTable -> Buffer Pool / Disk
> * What are slotted pages?
> * What are disadvantages of disk-based DBMS?
> 	* Buffer pool causes high overhead (indirection: index -> page table -> (Buffer Pool OR Disk -> Buffer Pool); calculate memory pointer)
> 	* CPU are much faster than memory and keep wating
> * What is in-memory DBMS?
> 	* All data of a table is stored as large "vectors" in memory
> 	* Compression is important because RAM is smaller than disk
> * What is row store?
> 	* Saving the table rowwise in memory
> * What is column store?
> 	* Saving the table columnwise in memory
> 	* Efficient when: All rows but few columns get accessed; compression works on column wise (only one datatype in one column); enables SIMD;
> * Heavyweight vs lightweight compression
> 	* heavyweight: data gets heavily compressed but no queries can be executed before decompressing
> 	* lighweight: less compression but queries can be excecuted
> * What is X compression and its pros/cons?
> 	* [[Dictionary Encoding|Dictionary Compression]]
> 	* [[Bit-Packing Encoding|Bit-Packing]]
> 	* [[Run-Length Encoding]]
> 	* [[Frame of Reference Encoding|Frame of Reference]]
> 	* [[Differential Encoding]]
> 	* [[Bitvector Encoding|Bit-Vector Encoding]]
> * Which Problem can occur with order-preserving dictionaries?
> 	* If data needs to be updated (e.g. Dict{0: Frankfurt; 1: Hamburg} and now add Berlin. Berlin should be before Frankfurt but 0 is already in use)
> 	* Solution: Leave gaps between codes OR store new values separetly and merge regulary
> * What is Early Materialization?
> 	* Decompress columns and reconstruct tuples (rows) as part of your table scan
> * What is Late Materialization?
> 	* [[Late Materialization]]
> * What is GPU-IN-DATA-PATH DBMS?
> 	* SSDs get cheaper but still have less bandwidth than main memory
> 	* User GPU for fast pruning and decompressing to use bandwidth more efficient and lower decompressing overhead

## Task 1 - True / False

> [!question] Question 1
> Since modern main-memory databases process all data in main memory, they require no mechanisms for persisting data to disk.
> - [ ] True
> - [ ] False

> [!question] Question 2
> Compression is used in in-memory DBMSs solely to reduce I/O overhead when reading from disk.
> - [ ] True
> - [ ] False

> [!question] Question 3
> A disk-based DBMS with a very large buffer pool is a good in-memory DBMS.
> - [ ] True
> - [ ] False

> [!question] Question 4
> In a disk-based DBMS, the query engine accesses data via Record IDs (RIDs) that point to slots in slotted pages.
> - [ ] True
> - [ ] False

> [!question] Question 5
> Column stores are particularly well-suited for OLTP workloads because individual tuples can be efficiently updated.
> - [ ] True
> - [ ] False

> [!question] Question 6
> Run-Length Encoding (RLE) on a column can be improved by sorting the data.
> - [ ] True
> - [ ] False

> [!question] Question 7
> With order-preserving dictionary compression, range queries can be executed directly on the compressed codes without decompressing first.
> - [ ] True
> - [ ] False

> [!question] Question 8
> Late materialization reconstructs tuples as early as possible in the query execution plan to minimize memory usage.
> - [ ] True
> - [ ] False

> [!success]- Solutions Task 1
> 1. **False** - In-memory DBMSs still need persistence mechanisms (e.g., logging, checkpointing) since RAM is volatile.
> 2. **False** - Compression also helps utilize memory bandwidth more efficiently (more data per cache line).
> 3. **False** - Disk-oriented DBMSs still incur significant overhead from latches, page table lookups, and indirections even with a full buffer pool.
> 4. **True**
> 5. **False** - Column stores are better suited for OLAP. OLTP prefers row stores.
> 6. **True** - Sorting produces longer runs, making RLE more efficient.
> 7. **True** - Since codes preserve the same order as original values, range predicates can be evaluated directly on codes.
> 8. **False** - Late materialization *delays* tuple reconstruction as long as possible.

---

## Task 2 - Short Answers

> [!question] Question 2a - Buffer Pool Overhead
> Name the two main overheads (indirections) that occur when accessing a record through the buffer pool - **even when the page is already in the buffer pool**.

> [!success]- Solution 2a
> 1. **Page Table Lookup**: PageID -> memory pointer to the page (lookup cost in the page table).
> 2. **Pointer Calculation to Tuple**: RID -> memory pointer to the tuple (page address + slot offset must be computed).

---

> [!question] Question 2b - Compression in In-Memory DBMS
> Why is compression useful in a pure in-memory DBMS even though there are no disk I/O costs? Name **two reasons**.

> [!success]- Solution 2b
> 1. **Reducing RAM requirements** - Data grows faster than RAM prices fall (memory costs have stagnated since ~2015).
> 2. **Better utilization of memory bandwidth** - More data per cache line -> fewer memory stalls (relevant due to the *Memory Wall* problem).

---

> [!question] Question 2c - Heavyweight vs. Lightweight
> Describe the difference between heavyweight and lightweight compression regarding **compression ratio** and **query processing**.

> [!success]- Solution 2c
> | | Compression Ratio | Query Processing |
> |---|---|---|
> | **Heavyweight** (e.g., ZIP) | Very high | Data must be **fully decompressed** before queries can be executed |
> | **Lightweight** (e.g., Dictionary, RLE) | Moderate | Queries can be executed **directly on compressed data** |

---

## Task 3 - Buffer Pool & Data Access

> [!question] Question 3
> Describe the steps a query engine goes through to access a record with RID `(PageID=2, Slot=3)` when the page is **already** present in the buffer pool. Address the use of **latches**.

> [!success]- Solution Task 3
> 1. Query engine receives RID `(PageID=2, Slot=3)` - e.g., from an index lookup.
> 2. **Acquire latch on page table entry** -> look up PageID=2 in the page table -> determine memory pointer to the page in the buffer pool.
> 3. **Acquire latch on the buffer frame** (Page2).
> 4. Compute memory pointer to the tuple: `page address + slot offset`.
> 5. Read the tuple.
> 6. Release buffer frame latch -> release page table entry latch.

---

## Task 4 - Compression Schemes

### 4a) Dictionary Compression

> [!question] Question 4a
> Given the following column `Country`:
>
> | Row | Country |
> |-----|---------|
> | 1   | Germany |
> | 2   | France  |
> | 3   | Germany |
> | 4   | Italy   |
> | 5   | France  |
> | 6   | Germany |
>
> Create a **single-value dictionary compression**. Provide the dictionary and the encoded column.

> [!success]- Solution 4a
> **Dictionary:**
>
> | Code | Value   |
> |------|---------|
> | 0    | France  |
> | 1    | Germany |
> | 2    | Italy   |
>
> **Encoded column:** `1, 0, 1, 2, 0, 1`

---

### 4b) Bit-Packing

> [!question] Question 4b
> The column from 4a) should additionally be **bit-packed**.
> - How many bits are needed per value?
> - Show how the first **three** encoded values are stored in an 8-bit word.

> [!success]- Solution 4b
> - m = 3 distinct values -> **n = ceil(log2(3)) = 2 bits** per value.
> - First three codes (1, 0, 1) in an 8-bit word: `01 | 00 | 01 | xx` (xx = unused padding).

---

### 4c) Run-Length Encoding

> [!question] Question 4c
> Given the following (already sorted) column `Quarter`:
> ```
> Q1, Q1, Q1, Q1, Q2, Q2, Q2, Q3, Q3, Q3, Q3, Q3, Q4, Q4
> ```
> Encode the column with RLE in the format `(value, start_pos, run_length)`.

> [!success]- Solution 4c
> ```
> (Q1, 1,  4)
> (Q2, 5,  3)
> (Q3, 8,  5)
> (Q4, 13, 2)
> ```

---

### 4d) Frame-of-Reference Encoding

> [!question] Question 4d
> Given the following price column with **Frame = 100** and **4 bits per offset**:
> ```
> 98, 102, 101, 99, 103, 140, 100
> ```
> - Encode all values.
> - Which value requires an escape code?
> - How is this exception handled?

> [!success]- Solution 4d
> | Value | Offset | Encoding         |
> |-------|--------|------------------|
> | 98    | -2     | `1110`           |
> | 102   | +2     | `0010`           |
> | 101   | +1     | `0001`           |
> | 99    | -1     | `1111` -> **Escape!** |
> | 103   | +3     | `0011`           |
> | **140** | +40  | `1111` -> followed by uncompressed value `140` |
> | 100   | 0      | `0000`           |
>
> **Value 140**: Offset +40 doesn't fit in 4 bits -> escape code `1111` is written, followed by the full uncompressed value.
>
> **Value 99**: Offset -1 in signed representation -> may also require escape depending on the bit scheme used.

---

## Task 5 - Order-Preserving Dictionaries

> [!question] Question 5a
> Explain why a **normal** (non-order-preserving) dictionary is problematic for range queries.

> [!success]- Solution 5a
> Without order preservation, codes are assigned arbitrarily. A range predicate on original values (e.g., `name BETWEEN 'A' AND 'C'`) **cannot** be expressed as a simple range predicate on codes - all codes would need to be decoded.

---

> [!question] Question 5b
> Given an order-preserving dictionary for the column `Name`:
>
> | Code | Name      |
> |------|-----------|
> | 10   | Andrea    |
> | 20   | Andy      |
> | 30   | Dana      |
> | 40   | Prashanth |
>
> Write the equivalent query on **compressed codes** for:
> ```sql
> SELECT * FROM users WHERE name LIKE 'And%'
> ```

> [!success]- Solution 5b
> ```sql
> SELECT * FROM users WHERE name BETWEEN 10 AND 20
> ```
> Since Andrea (10) and Andy (20) are the only values with prefix "And" and the dictionary is order-preserving.

---

> [!question] Question 5c
> What **two strategies** exist for handling insertions/updates in an order-preserving dictionary?

> [!success]- Solution 5c
> 1. **Separate unsorted partition**: New values are stored in a separate partition and periodically merged into the sorted main partition.
> 2. **Gaps between codes**: Gaps are intentionally left between codes when building the dictionary, so new values can be inserted.

---

## Task 6 - Bit-Packing Calculations

> [!question] Question 6a (1 Point)
> A column has at most **m = 1000** distinct values. Calculate the minimum number of bits **n** (formula + result).

> [!success]- Solution 6a
> $$n = \lceil \log_2(m) \rceil = \lceil \log_2(1000) \rceil = \lceil 9{,}97 \rceil = \textbf{10 Bits}$$

---

> [!question] Question 6b
> How many dictionary-encoded values can theoretically fit in a **64-bit** processor word if **n = 9 bits** per value are used? By what factor does this theoretically increase data throughput?

> [!success]- Solution 6b
> $$\lfloor 64 / 9 \rfloor = \textbf{7 values}\ \text{per 64-bit word}\ \text{(1 bit unused)}$$
> Theoretical throughput factor: **7x** compared to 1 value per 64-bit load without bit-packing.

---

## Task 7 - Row Store vs. Column Store (3 Points)

> [!question] Question 7a
> Name **three concrete advantages** of column stores for OLAP workloads.

> [!success]- Solution 7a
> 1. **Higher read efficiency** - Only the actually needed columns are read.
> 2. **Better compression** - Each column contains only one data type -> lower entropy.
> 3. **Efficient sequential scanning** - Pre-fetching works optimally; SIMD vectorization is directly applicable.

---

> [!question] Question 7b
> When is a **row store** preferable to a column store? Briefly justify.

> [!success]- Solution 7b
> For **OLTP** workloads (e.g., single-tuple inserts, point updates). Since all attributes of a tuple are stored contiguously, an entire tuple can be read or written with a single access.

---

## Task 8 - Early vs. Late Materialization
```sql
SELECT ProductID, COUNT(*)
FROM Sales
WHERE Quarter = 'Q2'
GROUP BY ProductID
```

> [!question] Question 8a - Early Materialization
> Describe how **early materialization** processes this query. What is the **disadvantage**?

> [!success]- Solution 8a
> **Process:** During the table scan, all required columns are immediately decompressed and assembled into complete tuples. All subsequent query operators work on uncompressed tuples.
>
> **Disadvantage:** Higher memory usage; optimization potential on compressed structures is wasted.

---

> [!question] Question 8b - Late Materialization
> Describe how **late materialization** works (`Quarter` = RLE-encoded, `ProductID` = bitvector-encoded). What **advantage** results?

> [!success]- Solution 8b
> **Process:**
> 1. Quarter column (RLE) -> filter `Quarter = Q2` -> directly yields the **position list** without decompression.
> 2. Look up these positions in the bitvector-encoded `ProductID` column -> compute `COUNT(*)` directly **on the bitvectors**.
> 3. Only the **result** is decompressed/materialized at the end.
>
> **Advantage:** Significantly less data is decompressed; query operators can operate on compressed structures.

---

## Task 9 - Heavyweight Compression & SSDs

> [!question] Question 9a
> Explain why an SSD-based DBMS with heavyweight compression **on CPU** alone provides no significant advantage over an uncompressed SSD-DBMS.

> [!success]- Solution 9a
> While compression reads less data from the SSD, the **decompression on CPU dominates runtime** (CPU-bound). The gain from reduced SSD transfer is almost entirely offset by decompression overhead.

---

> [!question] Question 9b
> What role does the **GPU** play in a GPU-in-Data-Path DBMS? Name three concrete ideas/tasks of this approach.

> [!success]- Solution 9b
> The GPU handles massively parallel computation directly in the data path from the SSD.
>
> **Three ideas:**
> 1. **Opportunistic Pruning** - Irrelevant data blocks are skipped before loading.
> 2. **GPU Direct I/O** - Data is loaded directly from SSD into GPU memory, bypassing CPU main memory.
> 3. **On-the-fly decompression on GPU** - Thanks to thousands of GPU cores, decompression can happen massively in parallel.

---

# B - In-Memory Scan

> [!abstract]- Own Notes
> * What is Vectorized Execution?
> 	* [[Vectorized Query Execution|Vectorized Execution]]
> * How to achieve Vectorized Execution?
> 	* Compiler go brr
> 	* Compiler Hints
> 		* parameter with 'restrict' to mark distinct memory locations
> 		* $\#pragma$ ivdep to ignore loop dependencies
> 	* Explicitly use SIMD-Instructions

## Task 1 - True/False
> [!question] 1.1
> Since modern in-memory databases process all data in main memory, they require no mechanisms for persisting data to disk.
>
> - [ ] True
> - [ ] False

> [!question] 1.2
> Compression is used in in-memory databases solely to reduce I/O overhead when reading from disk.
>
> - [ ] True
> - [ ] False

> [!question] 1.3
> A SIMD instruction (Single Instruction Multiple Data) processes a single operation on multiple data elements simultaneously.
>
> - [ ] True
> - [ ] False

> [!question] 1.4
> The compiler can automatically vectorize any loop as long as the optimization level is set high enough.
>
> - [ ] True
> - [ ] False

> [!question] 1.5
> The `restrict` keyword in C++ is part of the official C++ standard.
>
> - [ ] True
> - [ ] False

> [!question] 1.6
> AVX-512 enables parallel processing of up to 16 single-precision floats in a single SIMD register.
>
> - [ ] True
> - [ ] False

> [!question] 1.7
> In SIMD-Scan, data must always be fully decompressed before a filter predicate can be applied.
>
> - [ ] True
> - [ ] False

> [!question] 1.8
> Dictionary Encoding assigns each unique value of a column a compact integer code, which is then stored in the column.
>
> - [ ] True
> - [ ] False

> [!success]- Solutions Task 1
>
> | Question | Answer | Reasoning |
> |----------|--------|-----------|
> | 1.1 | **False** | In-memory DBs need logging/recovery (e.g., WAL) for persistence |
> | 1.2 | **False** | Compression also saves main memory and improves cache efficiency |
> | 1.3 | **True** | Definition of SIMD |
> | 1.4 | **False** | Only simple loops without pointer aliasing can be auto-vectorized |
> | 1.5 | **False** | `restrict` is not a C++ standard, but supported in GCC/Clang/MSVC |
> | 1.6 | **True** | 512 bits / 32 bits = 16 single-precision floats |
> | 1.7 | **False** | SIMD-Search filters directly on SIMD-lane-aligned data |
> | 1.8 | **True** | Definition of Dictionary Encoding |

---

## Task 2 - Short Answers

> [!question] 2.1 - Vectorization Approaches
> Name the **three approaches** a developer can use for SIMD vectorization in code.

> [!success]- Solution 2.1
> 1. Automatic Vectorization
> 2. Compiler Hints (`restrict`, `#pragma ivdep`)
> 3. Explicit Vectorization (SIMD Intrinsics)

---

> [!question] 2.2 - SISD vs. SIMD
> Briefly explain the difference between **SISD** and **SIMD**.

> [!success]- Solution 2.2
> SISD processes one operation on one data element; SIMD processes the same operation simultaneously on a vector of elements (e.g., 4x32-bit in a 128-bit register).

---

> [!question] 2.3 - SIMD Scan Filter Algorithm
> Describe the four steps of the **SIMD scan filter algorithm** for a column store (without bit-packing).

> [!success]- Solution 2.3
> 1. Load vector into SIMD register
> 2. SIMD comparison with lower/upper bound -> output mask
> 3. Store results at positions where mask = 1
> 4. Repeat until entire column is filtered

---

> [!question] 2.4 - Automatic Vectorization
> Why can the following loop **not** be automatically vectorized?
>
> ```c
> void add(int *X, int *Y, int *Z) {
>     for (int i = 0; i < MAX; i++) {
>         Z[i] = X[i] + Y[i];
>     }
> }
> ```

> [!success]- Solution 2.4
> The compiler cannot guarantee that `X`, `Y`, `Z` point to different memory regions (pointer aliasing). If e.g., `Z == X`, parallel execution would be incorrect.

---

> [!question] 2.5 - Bit-Packing
> What is **bit-packing** and why is it beneficial for in-memory databases?

> [!success]- Solution 2.5
> Bit-packing stores values using the minimum necessary number of bits (e.g., 2 bits for 3 dictionary entries). Saves main memory and improves cache utilization.

---

## Task 3 - Compression Schemes

> [!question] 3.1a - Dictionary Encoding
> Given the following column `City`:
>
> | Row | City      |
> |-----|-----------|
> | 1   | Frankfurt |
> | 2   | Darmstadt |
> | 3   | Frankfurt |
> | 4   | Mainz     |
> | 5   | Darmstadt |
> | 6   | Mainz     |
> | 7   | Darmstadt |
>
> Create the **dictionary encoding**. Provide the dictionary and the encoded column.

> [!success]- Solution 3.1a
> Dictionary: `0=Darmstadt, 1=Frankfurt, 2=Mainz`
> Encoded column: `1, 0, 1, 2, 0, 2, 0`

---

> [!question] 3.1b - Bit-Packing Width
> How many bits are needed for **bit-packing** the encoded values from 3.1a? Briefly justify.

> [!success]- Solution 3.1b
> 2 bits, since 3 distinct values -> $\lceil \log_2(3) \rceil = 2$ bits

---

> [!question] 3.2 - Lightweight Compression
> Name **four** lightweight compression schemes from the lecture and describe each in one sentence.

> [!success]- Solution 3.2
> 1. **Dictionary:** Replaces recurring strings with small integer codes
> 2. **Bit-Packing:** Stores integer codes with minimal bit width instead of full 32/64 bits
> 3. **RLE (Run-Length Encoding):** Stores consecutive identical values as (value, count) pairs
> 4. **Frame-of-Reference:** Stores only the difference of values from a reference value (base value)

---

## Task 4 - SIMD Decompression Algorithm

> [!question] 4.1 - 4-Step Decompression
> The SIMD decompression algorithm for bit-packed data (e.g., 9-bit packing) consists of 4 steps. Describe each step and explain **why** it is necessary.

> [!success]- Solution 4.1
> | Step | Name | Description | Why necessary? |
> |------|------|-------------|----------------|
> | 1 | Load | Load bit-packed data from memory into 128-bit SIMD register | All subsequent operations run on the register |
> | 2 | Shuffle | Copy bytes via mask to new target positions so each value sits in its own 32-bit lane | Bit-packed values span byte boundaries -> must be aligned first |
> | 3 | Shift/Extract | 32-bit SIMD shift with variable shift amounts per lane | Fine-grained bit alignment within the lane; removes excess bits from neighboring values |
> | 4 | Store | Write contents of result register back to normal memory | Makes decompressed values available for further processing (e.g., filter, projection) |

---

## Task 5 - Intel SIMD Extensions

> [!question] 5.1 - AVX-512 Capacity
> How many **32-bit integer values** can be processed simultaneously in an AVX-512 register?

> [!success]- Solution 5.2
> 512 / 32 = **16 values**

## Task 6 - Application Scenario

> [!question] 6.1 - SIMD-Search on Compressed Data
> Given the following SQL query on a column store with dictionary encoding:
>
> ```sql
> SELECT * FROM Customers WHERE City >= 'F' AND City <= 'M'
> ```
>
> The column `City` is stored **2-bit-packed** (Dictionary: `0=Darmstadt, 1=Frankfurt, 2=Mainz, 3=Mannheim`).
>
> Which dictionary codes qualify? Describe how SIMD-Search proceeds without full decompression.

> [!success]- Solution 6.1
> Qualifying codes: `1` (Frankfurt) and `2` (Mainz). SIMD-Search:
> 1. Load bit-packed data & align into SIMD lanes (Shuffle)
> 2. SIMD comparison of aligned values with `vec_low=1` and `vec_high=2`
> 3. Result is a bitmask of qualifying positions -> column is selectively decompressed only for those

---

> [!question] 6.2 - Advantage of SIMD-Search
> What is the advantage of **SIMD-Search** over the "decompress first, then filter" approach?

> [!success]- Solution 6.2
> Saves full decompression of non-qualifying values -> less work, better cache utilization, higher throughput.

# C - In-Memory Indexes

> [!abstract]- Own Notes
> * B+ Tree Operations
> 	* Upsert(6, bar)
> 	* Lookup(38)
> 	* standard lock coupling (lc)
> 	* optimistic lock coupling (olc)
> * Each inner node and leaf is mapped to a database page of multiple KB (using a slotted page design)
> * What happens if a B-tree is traversed? Which operations are needed in a disk-based DBMS? How are pages coming to memory?
> * What could be the sources of inefficiencies of B-trees when we target in-memory DBMSs? Remember the first lecture!
> 	* Index -> PageTable -> Buffer Pool/Disk
> * What is T-Tree
> 	* Bad perfomance on modern CPUs due to many pointer lookups
> 	* T-Tree is from time where CPU where slow but now Cache is super fast
> * What is Cache Locality?
> 	* Temporal
> 	* Spatial
> * HARDWARE PREFETCHING
> 	* next-line prefetching: read a -> fetch a+1
> 	* stream prefetching: read a, a+1 -> fetch a+2, a+3
> 	* cant handle branches, function call or pointer chasing
> * CSS-TREE
> 	* Fit each node into a cache line
> 	* Nodes are 100% filled with data (no pointers!)
> 	* read only
> 	* From b* (m + 1) + 1 to b* (m + 1) + (m + 1)
> * CSB+-TREE
> * Search rate: CSS > CSB+ > CSB+ seg > B+
> * Insertion rate: B+ = CSB+ seg > CSB+ > CSS

## Part A - True/False

> [!question] A3
> The B-tree was originally designed for disk-based database systems and is therefore not directly optimized for main-memory DBMSs.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - B-Tree was designed for disk-based systems (large nodes = page size, not cache line size).

---

> [!question] A4
> T-Trees were developed when CPUs were slower than today and therefore benefit greatly from CPU caches in modern systems.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **False** - T-Trees do *not* benefit well from CPU caches. Many pointer lookups lead to random accesses = many cache misses.

---

> [!question] A5
> OLAP workloads focus on short point lookups with frequent updates, while OLTP prefers long range queries with infrequent updates.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **False** - Swapped! OLTP = point lookups + frequent updates + many clients. OLAP = long range queries + infrequent updates + few clients.

---

> [!question] A6
> A cache miss occurs when the requested cache line is already in the cache and can be read directly.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **False** - That describes a cache **hit**. A cache miss means the line is not in the cache and must be loaded from main memory.

---

> [!question] A7
> The typical cache line size of modern CPUs is 64 bytes.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - 64 bytes is the standard for modern CPUs.

---

> [!question] A8
> Hardware prefetching supports sequential accesses and spatial locality but struggles with pointer chasing (random access).
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - Next-line / stream prefetching helps with sequential access. Pointer chasing creates unpredictable access patterns.

---

> [!question] A9
> The CSS-Tree (Cache-Sensitive Search Tree) supports both read and write operations with equally good performance.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **False** - The CSS-Tree is **read-only** optimized. Updates require a complete rebuild of the tree.

---

> [!question] A10
> The CSB+-Tree improves cache friendliness over the classic B+-Tree by using only **one** pointer per inner node to a contiguous array group of all child nodes.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - Exactly the core idea of the CSB+-Tree: one pointer per node group instead of N pointers per node.

---

> [!question] A11
> Locks (in the sense of transaction locks) and latches serve the same purpose in a DBMS and can be used synonymously.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **False** - **Locks** guarantee transaction isolation (managed by the lock manager). **Latches** protect internal data structures from concurrent thread access.

---

> [!question] A12
> In standard lock coupling, a parent node can be released as soon as the child node is considered "safe" (i.e., no split/merge needed).
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - This is the core of the lock coupling protocol: latches are passed along step by step.

---

> [!question] A13
> Optimistic Lock Coupling (OLC) uses version numbers instead of write latches and is therefore typically more efficient than standard lock coupling for read-intensive workloads.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - OLC avoids write latches for reads -> no blocking of readers by writers -> better parallelism for read-heavy workloads.

---

> [!question] A14
> Pointer swizzling avoids repeated translation of page IDs to memory addresses by rewriting page IDs to direct memory pointers on first load.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **True** - This is the definition of pointer swizzling (eager or lazy).

---

> [!question] A15
> Temporal locality means that data at neighboring addresses are likely to be used shortly after each other.
> - [ ] True
> - [ ] False

> [!success]- Solution
> **False** - That describes *spatial* locality. Temporal locality = recently used data will likely be used again soon (e.g., `sum` in a loop).

---

## Part B - Short Answers

> [!question] B1 - Buffer Pool Access
> Explain the steps the query engine must perform to access a record on a page that is **already in the buffer pool**.

> [!success]- Model Solution
> 1. Query engine determines the **page ID** and **slot** of the target record (e.g., from an index).
> 2. The page ID is looked up in the **page table** to find the buffer frame (memory address).
> 3. The buffer frame is **latched** (pinned) so it cannot be evicted.
> 4. The record is read via the **slot in the frame** directly from main memory.
> 5. After processing, the frame pin is **released**.

---

> [!question] B2 - T-Tree Performance
> Why are T-Trees often slower than expected on modern CPUs, even though they were designed as main-memory index structures?

> [!success]- Model Solution
> T-Trees were developed in the 1980s when CPUs were slower than main memory. Today there is a large CPU-Memory Gap. T-Trees navigate via many pointer jumps (pointer chasing), leading to random accesses. These are hard for hardware prefetchers to predict and cause many cache misses.

---

> [!question] B3 - CPU-Memory Gap
> What is the **CPU-Memory Gap** (Memory Wall), and what significance does it have for the design of in-memory index structures?

> [!success]- Model Solution
> The CPU-Memory Gap describes the growing speed difference between CPU clock speed and DRAM access latency. CPUs wait increasingly longer for memory accesses. Multi-level CPU caches (L1/L2/L3) were introduced in response. For in-memory index structures this means: **cache misses**, not main memory accesses, are the bottleneck. Index structures must therefore be designed cache-consciously.

---

> [!question] B4 - Locality Principles
> Explain the difference between **spatial locality** and **temporal locality** and give one example each from the database context.

> [!success]- Model Solution
> - **Temporal locality**: Recently used data will likely be used again soon. Example: A frequently queried index node (e.g., the root of a B+-Tree) stays in the cache.
> - **Spatial locality**: Data at nearby addresses are likely to be used together. Example: When sequentially scanning an array (e.g., a leaf node in CSS-Tree), adjacent keys are loaded together into a cache line.

---

> [!question] B5 - CSS-Tree Concept
> Describe the fundamental concept of the **CSS-Tree** (Cache-Sensitive Search Tree). How are child nodes found without using explicit pointers?

> [!success]- Model Solution
> The CSS-Tree is a read-optimized in-memory index structure based on the B+-Tree. All inner nodes are stored pointer-free in a contiguous array, with each node filling exactly one cache line. Child nodes are found via **offset calculation**: For a node at position `b` with `m` entries, children are at positions `b*(m+1)+1` to `b*(m+1)+(m+1)`.

---

> [!question] B6 - Lock vs. Latch
> What is the difference between a **latch** and a **lock** in a DBMS?

> [!success]- Model Solution
> | | Lock | Latch |
> |--|------|-------|
> | **Purpose** | Transaction isolation | Protecting internal data structures |
> | **Managed by** | Lock Manager | Directly in code |
> | **Duration** | Entire transaction | Only during critical sections |

---

> [!question] B7 - Lock Coupling Release Condition
> Under what condition can a transaction release the latch on a parent node before reaching the leaf node during lock coupling? Distinguish between read and write operations.

> [!success]- Model Solution
> - **Read (Search)**: The parent can always be released once the child node is latched.
> - **Write (Insert/Delete)**: The parent can be released when the child is **safe**: For insert = not full (no split needed). For delete = more than half full (no merge needed). In the worst case, latches are held from root to leaf.

---

> [!question] B8 - Optimistic Lock Coupling
> Explain the principle of **Optimistic Lock Coupling (OLC)**. What happens when a validation fails?

> [!success]- Model Solution
> OLC replaces classic read latches with version numbers. Instead of locking a node, the thread reads the current version number, accesses the node, and then validates whether the version has changed. If no concurrent writer was active, the operation is valid. If validation fails (version changed), the entire operation is **restarted**. OLC is especially efficient for read-intensive workloads since readers don't block writers.

---

> [!question] B9 - CSS-Tree Updates
> Why is the CSS-Tree not update-friendly? Which variant solves this problem, and how?

> [!success]- Model Solution
> The CSS-Tree stores all nodes in a dense, pointer-free array. An insert or split requires shifting large parts of the array. The **CSB+-Tree** solves this: it uses one pointer per child node group (Node Group). On a split, only the affected node group needs to be reallocated. With segmentation (e.g., 2 segments), splits become even cheaper.

---

> [!question] B10 - Pointer Swizzling
> What is **pointer swizzling** and why is it relevant for SSD-based databases with a buffer pool?

> [!success]- Model Solution
> Pointer swizzling is the technique of rewriting page IDs in an index to direct memory pointers on first load (eager or lazy). Classic disk-based indexes store page IDs. Each access requires translating the page ID via the page table to a memory address. Swizzling eliminates this overhead for pages in the buffer pool, achieving in-memory performance for "warm" pages.

---

## Part C - Calculation Problems

> [!question] C1 - Lock Counting on B+-Tree
> Given the following B+-Tree:
> ```
>                     [ 20 ]  (A)
>                    /        \
>             [ 10 ]  (B)      [ 35 ]  (C)
>            /        \       /        \
>         [6]  (D)  [12] (E)  [23] (F)  [38|44] (G)
> ```
> Execute the following two operations and count the **total number of acquired locks**:
> - **Upsert(6, "bar")**
> - **Lookup(38)**
>
> | Method | Upsert(6, "bar") | Lookup(38) | Total |
> |---|---|---|---|
> | Standard Lock Coupling | | | |
> | Optimistic Lock Coupling | | | |

> [!success]- Solution (NOT SURE IF THIS IS TRUE)
> **Lookup(38) - Standard Lock Coupling:**
> Path: A -> C -> G
> R(A) acquire -> R(C) acquire, R(A) release -> R(G) acquire, R(C) release
> = **3 locks acquired**
>
> **Lookup(38) - Optimistic Lock Coupling:**
> read_version(A) -> read_version(C) + validate(A) -> read_version(G) + validate(C) -> validate(G)
> = **6 operations** (3 reads + 3 validates)
>
> **Upsert(6, "bar") - Standard Lock Coupling:**
> Path: A -> B -> D. D has only key [6] -> not full -> safe.
> W(A) -> W(B) acquire, B is safe -> W(A) release -> W(D) acquire, W(B) release
> = **3 locks acquired**
>
> **Upsert(6, "bar") - Optimistic Lock Coupling:**
> read_version(A) -> read_version(B) + validate(A) -> W(D) acquire + validate(B)
> = **5 operations** (2 reads + 2 validates + 1 write latch)
>
> | Method | Upsert(6) | Lookup(38) | Total |
> |---|---|---|---|
> | Standard LC | 3 | 3 | **6** |
> | Optimistic LC | 5 | 6 | **11** |

---

> [!question] C2 - CSS-Tree Offset Calculation
> A CSS-Tree has **m = 3** entries per node (i.e., 4 child nodes per inner node).
>
> Formula: Children of node `b` are at offsets `b*(m+1)+1` to `b*(m+1)+(m+1)`
>
> **a)** Child node offsets for node at position **b = 0**?
>
> **b)** Child node offsets for node at position **b = 2**?
>
> **c)** Search key **k = 17** in node b = 0 with entries [5 | 43 | 99]: Which child node offset is descended to?

> [!success]- Solution
> **a)** b=0, m=3: `0*(3+1)+1 = 1` to `0*(3+1)+(3+1) = 4` -> children at offsets **1, 2, 3, 4**
>
> **b)** b=2, m=3: `2*(3+1)+1 = 9` to `2*(3+1)+(3+1) = 12` -> children at offsets **9, 10, 11, 12**
>
> **c)** k=17: 17 > 5 and 17 <= 43 -> second range -> child at **offset 2**

---

> [!question] C3 - Cache Line Analysis
> Cache line size: **64 bytes**. Integer keys: **4 bytes**. Child pointers: **8 bytes**.
>
> **a)** How many key-pointer pairs (12 bytes each) fit in a cache line?
>
> **b)** CSS-Tree: No pointers. How many integer keys (4 bytes) fit in a cache line?
>
> **c)** What is the practical consequence for tree height and cache misses?

> [!success]- Solution
> **a)** `64 / 12 = 5.33` -> **5 key-pointer pairs** per cache line
>
> **b)** `64 / 4 = 16` -> **16 keys** per cache line
>
> **c)** More keys per node -> higher branching factor -> **lower tree height** -> fewer node visits -> **fewer cache misses**.

---

## Part D - Comparison Questions

> [!question] D1 - OLTP vs. OLAP
> Complete the table:
>
> | Criterion | OLTP | OLAP |
> |---|---|---|
> | Query Type | | |
> | Update Frequency | | |
> | Number of Clients | | |
> | Index Requirements | | |

> [!success]- Solution
> | Criterion | OLTP | OLAP |
> |---|---|---|
> | Query Type | Short point lookups | Long range queries |
> | Update Frequency | Very frequent | Infrequent (e.g., 1x/day via ETL) |
> | Number of Clients | Many (thousands) | Few |
> | Index Requirements | High throughput, concurrency, OLC | Read-optimized, cache-sensitive (CSS-Tree) |

---

> [!question] D2 - Search Performance Ranking
> Rank by **search performance** (best first): B+-Tree, T-Tree, CSS-Tree, CSB+-Tree

> [!success]- Solution
> **1. CSS-Tree** -> pointer-free, maximum cache density, no pointer chasing
> **2. CSB+-Tree** -> similar to CSS, but one pointer per node group -> slightly more overhead
> **3. B+-Tree** -> pointer-based, but large nodes with many keys
> **4. T-Tree** -> many pointer jumps, poor cache locality, many cache misses

---

> [!question] D3 - Insert Performance Ranking
> Rank by **insert performance** (best first): B+-Tree / CSB+-Tree (2 seg.), CSB+-Tree (1 seg.), CSS-Tree

> [!success]- Solution
> **1. B+-Tree = CSB+-Tree (2 segments)** -> cheap splits
> **2. CSB+-Tree (1 segment)** -> split requires new node group allocation
> **3. CSS-Tree** -> no update support; insert would require complete rebuild

---

## Part E - Scenario/Design Questions

> [!question] E1 - Online Shop Index Choice
> A startup is planning a database for an online shop (high transaction rate, many concurrent users, frequent inserts and point lookups). Which index structure would you recommend? Consider concurrency.

> [!success]- Model Solution
> Recommendation: **B+-Tree with Optimistic Lock Coupling (OLC)**. The B+-Tree supports efficient point lookups and inserts with dynamic splits. OLC minimizes locking overhead for read-intensive workloads and scales well on multi-core systems. CSS-Tree is ruled out (no update support). T-Trees are unsuitable due to cache misses.

---

> [!question] E2 - When is OLC Worse?
> Explain when **Optimistic Lock Coupling** can perform worse than standard lock coupling.

> [!success]- Model Solution
> OLC is worse for **write-heavy workloads with high contention**. When many threads write simultaneously, validations fail frequently and operations must be restarted often (wasted work). With many restarts, the overhead exceeds the saved latch costs.

---

> [!question] E3 - OLAP Read-Only Index
> A developer wants to build an in-memory index for a **read-only data warehouse** (data is reloaded daily). Which index structure is best suited?

> [!success]- Model Solution
> Recommendation: **CSS-Tree**. Since data is rebuilt daily via bulk load, missing update support is not a problem. The CSS-Tree offers the best search performance through pointer-free nodes, optimal spatial locality, and no locking overhead.

---

# D - ART (Adaptive Radix Tree)

## Task 1 - True/False 

- [ ] **T** / **F** - Radix trees have a lookup complexity of O(log n), where n is the number of stored keys.
- [ ] **T** / **F** - In ART, tree height depends primarily on the key length k, not on the number of elements n.
- [ ] **T** / **F** - Hash tables support range scans since they store data in sorted order.
- [ ] **T** / **F** - ART uses a span of 8 bits, i.e., each inner node processes exactly 1 byte of the key per level.
- [ ] **T** / **F** - FAST (Fast Architecture Sensitive Tree) supports incremental updates without rebuilding the structure.
- [ ] **T** / **F** - In ART, keys are stored in bitwise lexicographic order, enabling range scans.
- [ ] **T** / **F** - Path compression in ART increases tree height but reduces memory usage.
- [ ] **T** / **F** - The worst-case memory consumption of ART is bounded at 52 bytes per key, regardless of key length.

> [!success]- Answers
> - F - Complexity is O(k), where k is the key length, not dependent on n
> - T
> - F - Hash tables scatter keys randomly, only support point queries
> - T
> - F - FAST is a static structure, updates require complete rebuild
> - T
> - F - Path compression **reduces** tree height (and memory)
> - T

---

## Task 2 - Multiple Choice

> [!question] Which statements about the four ART node types are correct? *(Multiple answers possible)*

- [ ] a) Node4 stores keys and pointers in separate, sorted arrays of length 4.
- [ ] b) Node16 uses SIMD instructions (SSE) to compare all 16 keys in parallel.
- [ ] c) Node48 stores keys directly as a 256-element array indexed by the key byte.
- [ ] d) Node256 requires an additional indirection via an index array before the pointer can be found.
- [ ] e) A node is replaced by a larger type when its capacity is exhausted (on insert).
- [ ] f) All node types use a constant-size header (16 bytes) that stores node type, child count, and compressed path.

> [!success]- Answers
> Correct: **a, b, e, f**
> - c) false: Node48 has a 256-element **index** array (not key array) that points to a separate pointer array
> - d) false: Node256 is a direct 256-pointer array - a single array access, no indirection

---

## Task 3 - Short Answers

### 3a) ART Node Types

> [!question] Fill in the table with the four node types, their capacity limits, and size in bytes.

| Node Type | Min. Children | Max. Children | Size (Bytes) |
| --------- | :-----------: | :-----------: | :----------: |
|           |               |               |              |
|           |               |               |              |
|           |               |               |              |
|           |               |               |              |

> [!success]- Answers
> | Node Type | Min. | Max. | Size |
> |-----------|:----:|:----:|:----:|
> | Node4     |  2   |  4   |  52  |
> | Node16    |  5   |  16  | 160  |
> | Node48    |  17  |  48  | 656  |
> | Node256   |  49  | 256  | 2064 |

### 3b) Weaknesses of Classic Trees

> [!question] Why are classic binary search trees (T-Trees, Red-Black Trees) inefficient on modern hardware? Name **two** reasons.

> [!success]- Answers
> 1. **Poor cache behavior**: Pointer-based traversal causes many cache misses since nodes are scattered across memory
> 2. **Branch mispredictions**: Comparison-based traversal is poorly predicted by the CPU branch predictor, causing pipeline stalls

---

## Task 4 - Fill in the Blanks

> [!question] Fill in the blanks with the correct terms.

ART uses two techniques to reduce tree height:

**Technique 1: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**
Inner nodes are only created when they must distinguish at least two leaf nodes. Paths to single leaves are truncated.

**Technique 2: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_**
Inner nodes with exactly one child are removed. The skipped partial key is handled either:
- **pessimistically**: stored as a vector at the node, compared during search
- **optimistically**: only the length is stored, comparison only at the leaf

ART uses a **hybrid** approach with a fixed-size vector of **\_\_\_** bytes. If exceeded, the algorithm switches to the optimistic strategy.

> [!success]- Answers
> - Technique 1: **Lazy Expansion**
> - Technique 2: **Path Compression**
> - Vector size: **8 bytes**

---

## Task 5 - Calculation

### 5a) Node48 Size

> [!question] Calculate the size (in bytes) of a **Node48**. Given: 16-byte header, 64-bit pointers.
> Formula: Header + Child-Index-Array (256 x 1 byte) + Pointer-Array (48 x 8 bytes)

> [!success]- Answer
> 16 + 256 + (48 x 8) = 16 + 256 + 384 = **656 bytes**

---

### 5b) Tree Height with s=8

> [!question] A radix tree with span s=8 stores 32-bit integer keys. How many levels of inner nodes does the tree have (without path compression)?

> [!success]- Answer
> ceil(k/s) = ceil(32/8) = **4 levels**

---

### 5c) Budget Analysis for Node4

> [!question] Using budget analysis, show that ART's worst-case memory consumption is <= 52 bytes/key. Verify for **Node4** (min. 2 children), where b(leaf) = x = 52.
> b(n) = sum b(children) - memory(n)

> [!success]- Answer
> - Min. children of Node4: 2
> - Budget of children: 2 x 52 = 104
> - Memory Node4: 52 bytes
> - b(Node4) = 104 - 52 = **52 >= 52** (check)
>
> Since the budget never goes negative, worst-case consumption is bounded at 52 bytes/key.

---

## Task 6 - Binary-Comparable Keys

### 6a) Signed Integer Problem

> [!question] Why can't signed integers (two's complement) be used directly as radix tree keys if the natural sort order should be preserved?

> [!success]- Answer
> In two's complement, negative numbers are bitwise **larger** than positive ones (MSB is 1). This would make e.g., -1 lexicographically greater than +1000, contradicting the desired numeric order.

---

### 6b) Transformation for Signed Integers

> [!question] Describe the transformation for **signed b-bit integers**.

> [!success]- Answer
> The **sign bit is flipped** (XOR with 2^(b-1)). The value is then stored like an unsigned integer (with byte-order swap on little-endian systems if needed).

---

### 6c) Requirement for Character Strings

> [!question] What additional requirement must character strings as keys fulfill that is not needed for integer types?

> [!success]- Answer
> Strings must be terminated with a **unique termination byte** (e.g., `\0`) that does not appear elsewhere in the string. Otherwise, one string could be a prefix of another, leading to incorrect lookups.

---

## Task 7 - Algorithm Analysis

> [!question] Analyze the ART search algorithm:

```python
search(node, key, depth)
 1  if node == NULL
 2    return NULL
 3  if isLeaf(node)
 4    if leafMatches(node, key, depth)
 5      return node
 6    return NULL
 7  if checkPrefix(node, key, depth) != node.prefixLen
 8    return NULL
 9  depth = depth + node.prefixLen
10  next = findChild(node, key[depth])
11  return search(next, key, depth+1)
```

### 7a) Lines 3-6

> [!question] What is being checked, and which ART technique makes this check necessary?

> [!success]- Answer
> It checks whether the found **leaf node actually matches the search key**. Necessary due to **Lazy Expansion**: paths to single leaves can be shortened, so you can arrive at a leaf that has a different key.

---

### 7b) Lines 7-8

> [!question] What happens here, and which technique is behind it?

> [!success]- Answer
> The **compressed path** of the node is compared with the search key. If it doesn't match, the search is immediately aborted (NULL). This is **Path Compression** (pessimistic approach).

---

### 7c) findChild for Node256

> [!question] What does `findChild` do for a Node256, and why is it particularly efficient?

> [!success]- Answer
> `findChild` performs exactly **one array access**: `node.child[byte]`. No further comparisons or indirections needed since the key byte directly serves as the index - O(1) with minimal overhead.

---

### 7d) Unsuccessful vs. Successful Search

> [!question] Why is an **unsuccessful search** faster than a successful one in radix trees?

> [!success]- Answer
> An unsuccessful search can **terminate early** as soon as a NULL pointer or non-matching prefix is found. A successful search must traverse the complete path to the leaf.

---

## Task 8 - Comparison & Classification

### 8a) Comparison Table

> [!question] Complete the table:

| Structure      | Sorted Order | Point Queries | Range Scans | Incremental Updates |
| -------------- | :----------: | :-----------: | :---------: | :-----------------: |
| Hash Table     |              |               |             |                     |
| Red-Black Tree |              |               |             |                     |
| FAST           |              |               |             |                     |
| ART            |              |               |             |                     |

> [!success]- Answers
> | Structure      | Sorted Order | Point Queries | Range Scans | Incremental Updates |
> |----------------|:---:|:---:|:---:|:---:|
> | Hash Table     | x | yes | x | yes |
> | Red-Black Tree | yes | yes | yes | yes |
> | FAST           | yes | yes | yes | x |
> | ART            | yes | yes | yes | yes |

---

### 8b) TPC-C: Why is ART Faster?

> [!question] In the TPC-C benchmark, ART is nearly **twice as fast** as Hash Table + Red-Black Tree. Name two structural reasons.

> [!success]- Answers
> 1. **Unified index structure**: ART can handle all operations (point queries, range scans, prefix lookups) as a single structure. Hash Table + RB-Tree must be combined, creating overhead.
> 2. **Better cache efficiency**: ART's compact, adaptive nodes fit better into CPU caches. In the benchmark, ART used only **half as much memory** as HT + RB-Tree.

---

# E - SSDs & Databases

> [!abstract]- Own Notes
> * Leanstore?
> 	* SSDs got super fast and created big IO gap (CPU can't utilize all that bandwidth)
> 	* Solution:
> 		* User small page size to have many concurent IO Operations to leaverage parallelism of SSDs
> 		* CPU is bottleneck -> no locks/mem. allocation, simpler page eviction

## Task 1 - True / False

> [!question] Question 1.3
> NVMe SSDs offer roughly **100x** more sequential read bandwidth than HDDs.
> - [ ] True
> - [ ] False

> [!question] Question 1.4
> SSDs can **overwrite a single page in-place** without erasing the surrounding block.
> - [ ] True
> - [ ] False

> [!question] Question 1.5
> The **Flash Translation Layer (FTL)** maps logical block addresses to physical flash locations.
> - [ ] True
> - [ ] False

> [!question] Question 1.6
> A **4 KB page size** yields the highest random-read IOPS throughput on NVMe SSDs.
> - [ ] True
> - [ ] False

> [!question] Question 1.7
> Using `O_DIRECT` on a block device **always** eliminates the need for `fdatasync`.
> - [ ] True
> - [ ] False

> [!question] Question 1.8
> SPDK (kernel-bypassing I/O) is **strictly necessary** to saturate a modern NVMe array.
> - [ ] True
> - [ ] False

> [!question] Question 1.9
> Under a **skewed** (non-uniform) write workload, Greedy GC typically achieves **lower** WAF than under a uniform workload.
> - [ ] True
> - [ ] False

> [!question] Question 1.10
> Increasing the **over-provisioning ratio** on an SSD reduces the Write Amplification Factor (WAF).
> - [ ] True
> - [ ] False

> [!success]- Task 1 - Solutions
>
> | # | Answer | Reasoning |
> |---|--------|-----------|
> | 1.3 | **True** | PM1743: 13 GB/s vs. HDD ~150 MB/s |
> | 1.4 | **False** | Out-of-place writing - the entire block must be erased first |
> | 1.5 | **True** | FTL manages the L2P table (Logical-to-Physical Mapping) |
> | 1.6 | **True** | 4 KB shows highest IOPS peak on PCIe 4.0 SSD |
> | 1.7 | **False** | SSDs with volatile write cache still require a flush |
> | 1.8 | **False** | SPDK is efficient, but `io_uring` (poll) achieves similar results |
> | 1.9 | **False** | Skew increases WAF with Greedy GC - hot/cold pages mix within blocks |
> | 1.10 | **True** | More OP -> fewer full blocks -> fewer GC writes -> lower WAF |

---

## Task 2 - Multiple Choice

> [!question] Question 2.1 - I/O-Gap
> Which of the following best describes the "I/O-Gap" presented in the lecture?
>
> - [ ] a) The latency difference between DRAM and NVMe storage
> - [ ] b) The gap between the maximum hardware I/O capability of an NVMe array and what database systems actually utilise
> - [ ] c) The bandwidth difference between PCIe 4.0 and PCIe 5.0 SSDs
> - [ ] d) The performance difference between sequential and random reads on SSDs

> [!question] Question 2.2 - LeanStore Page Size
> What is the primary reason LeanStore moved from **16 KB to 4 KB pages**?
>
> - [ ] a) 4 KB pages reduce CPU cache misses during B-Tree traversal
> - [ ] b) 4 KB is the Linux kernel's native page size, simplifying memory management
> - [ ] c) 4 KB pages achieve the highest random-read IOPS on NVMe SSDs
> - [ ] d) 4 KB pages require less DRAM for buffer pool metadata

> [!question] Question 2.3 - I/O Interface
> Which I/O interface achieves the **lowest CPU overhead** per I/O operation according to the lecture experiments?
>
> - [ ] a) POSIX `pread`
> - [ ] b) `libaio`
> - [ ] c) `io_uring` (interrupt mode)
> - [ ] d) SPDK (kernel-bypassing)

> [!question] Question 2.4 - NAND Flash Units
> In NAND flash, the **unit of erasure** is the:
>
> - [ ] a) Page
> - [ ] b) Block
> - [ ] c) Die
> - [ ] d) Plane

> [!question] Question 2.5 - WAF Definition
> The **Write Amplification Factor (WAF)** is defined as:
>
> - [ ] a) Sequential write bandwidth / Random write bandwidth
> - [ ] b) Physical bytes written to flash / Logical bytes written by the host
> - [ ] c) Number of GC cycles / Number of host write operations
> - [ ] d) Total SSD capacity / Used SSD capacity

> [!question] Question 2.6 - DWPD
> What does **"DWPD = 1"** mean for a 3.8 TB SSD?
>
> - [ ] a) The SSD can sustain 1 GB/s of writes indefinitely
> - [ ] b) The SSD can be fully overwritten once per day over its warranty period
> - [ ] c) The SSD writes each page at most once before requiring an erase
> - [ ] d) The SSD has 1 % over-provisioning

> [!question] Question 2.7 - User-Space Threading
> Which statement about **user-space threading** in the redesigned LeanStore is correct?
>
> - [ ] a) User-space threads are scheduled by the Linux kernel like normal pthreads
> - [ ] b) User-space threads enable full control over scheduling and eliminate thread oversubscription
> - [ ] c) User-space threads require a dedicated background I/O thread per worker
> - [ ] d) User-space threads are only beneficial when the SSD is I/O-bound

> [!question] Question 2.8 - GC Policy
> Under a **uniform** random-write workload, which garbage collection policy is **optimal** for minimising WAF?
>
> - [ ] a) FIFO (First-In First-Out)
> - [ ] b) LRU (Least Recently Used)
> - [ ] c) Greedy (select victim block with the least valid data)
> - [ ] d) Round-Robin

> [!success]- Task 2 - Solutions
>
> | Question | Answer | Hint |
> |----------|--------|------|
> | 2.1 | **b** | 3.5x gap between hardware capability and actual utilization |
> | 2.2 | **c** | Highest IOPS peak at 4 KB |
> | 2.3 | **d** | SPDK: ~2000 cycles/IO vs. ~6000 for libaio/io_uring |
> | 2.4 | **b** | Block is the erasure unit; page is the read/write unit |
> | 2.5 | **b** | WAF = physWrites / hostWrites |
> | 2.6 | **b** | 1 DWPD x 3.8 TB = 44 MB/s sustained write rate |
> | 2.7 | **b** | Boost Context, pinned to cores, no oversubscription |
> | 2.8 | **c** | Greedy is theoretically optimal under uniformity |

---

## Task 3 - Short Answers

> [!question] Question 3.1 - NVMe Challenges (2 pts)
> Name **two** key challenges that NVMe SSDs introduce for database systems compared to HDDs.

> [!question] Question 3.2 - Flash Translation Layer (2 pts)
> Briefly explain what the **Flash Translation Layer (FTL)** does and why it needs DRAM.

> [!question] Question 3.3 - SSD Garbage Collection (2 pts)
> Describe the process of **SSD garbage collection** in your own words. What is the role of over-provisioning (OP)?

> [!question] Question 3.4 - Sequential Writing & WAF (2 pts)
> Why does WAF **not automatically improve** with sequential writing when **multiple** active write zones are used simultaneously?

> [!question] Question 3.5 - WAF Calculation (2 pts)
> Given an SSD with **OP = 0.20** (20% over-provisioning) under a uniform workload.
> Formula: `WAF = 1 / (2 x OP)`
>
> Calculate WAF for OP = 0.20 and OP = 0.10.

> [!success]- Question 3.5 - Solution
> - OP = 0.20 -> WAF = 1 / (2 x 0.20) = **2.5**
> - OP = 0.10 -> WAF = 1 / (2 x 0.10) = **5.0**

> [!question] Question 3.6 - Correct SSD Benchmarking (2 pts)
> Name **three correct steps** when benchmarking an NVMe SSD to obtain reproducible steady-state results.

> [!success]- Question 3.6 - Solution
> 1. Fully erase the SSD beforehand: `nvme sanitize --sanact=start-block-erase` or `blkdiscard`
> 2. Initialize by writing sequentially (write first what you read)
> 3. Run the benchmark long enough until steady state is reached

---

## Task 4 - B+-Tree Locking

```
              [ 20 ]  A
             /        \
     [ 10 ]  B        [ 35 ]  C
    /        \        /       \
[ 6 ] D  [12] E  [23] F  [38|44] G
```

Operations: **Upsert(6, "bar")** and **Lookup(38)**

> [!question] Question 4.1 - Standard Lock Coupling (3 pts)
> For each operation, provide the sequence of locked nodes and the lock mode (`S` = shared, `X` = exclusive).

> [!question] Question 4.2 - Optimistic Lock Coupling (3 pts)
> Explain the difference from standard lock coupling. How many locks/validations are needed for the same operations?

---

## Task 5 - Buffer Pool & I/O Path

> [!question] Question 5.1 - Page Present in Buffer Pool (2 pts)
> Describe step by step what happens when the query engine accesses a record whose page is **already in the buffer pool**.

> [!question] Question 5.2 - Page Not in Buffer Pool / Eviction (2 pts)
> Describe step by step what happens when the page is **not in the buffer pool** (page fault, eviction required).

> [!question] Question 5.3 - Global Latch as Bottleneck (2 pts)
> Why did the original LeanStore implementation (2018) with a **global latch** become a bottleneck on NVMe arrays? What was the solution?

---

## Task 6 - SSD Architecture

> [!question] Question 6.1 - Components
> Provide a brief functional description (1-2 sentences) for each component.
>
> | Component | Function |
> |---|---|
> | Flash Translation Layer (FTL) | |
> | Garbage Collection | |
> | Wear Leveling | |
> | ECC Engine | |

> [!question] Question 6.2 - SLC / MLC / TLC / QLC
> What is the difference between **SLC**, **MLC**, **TLC**, and **QLC** NAND flash? What tradeoff is made?

---

## Task 7 - Open Question

> [!question] Question 7.1 - I/O-Gap Analysis
> A company runs an OLTP database on **8 x PCIe 5.0 enterprise SSDs** (each ~2700K random-read IOPS). The system achieves only ~3.5M lookups/s, although the theoretical capacity is ~21.6M IOPS.
>
> Name and explain **at least three** possible causes of the I/O gap and propose a concrete solution for each.
