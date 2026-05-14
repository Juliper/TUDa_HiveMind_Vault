---
title: SDMS
aliases:
  - Skalierbare Datenmanagement Systeme
tags:
  - fb20
  - master
  - semester-1
  - 6CP
description: ""
draft: false
---
## Rust Concepts

### Overview

This presentation covers Rust's most distinctive features compared to other languages:

- **Ownership System**: Memory management without garbage collection
- **Borrowing & References**: Safe concurrent access to data
- **Structs, Traits & Methods**: Object-oriented programming without inheritance
- **Enums & Pattern Matching**: Type-safe error handling and optional values
- **Common Collections**: Vec, String, and other essential data structures

### 1. Ownership

**Why Ownership?**

- Stack: Fixed-size data (integers, booleans) - automatic memory management
- Heap: Variable-size data (Vec, String contents) - managed by ownership in Rust

**Three Ownership Rules:**

1. Each value has an owner
2. Only one owner at a time
3. When owner goes out of scope, value is dropped

**Key Concepts:**

- **Move Semantics** (default): Ownership transfers when assigning/passing values
- **Copy Semantics**: Trivially copyable types (i32, bool, char, f64) are automatically copied
- **Cloning**: Explicit deep copy with `.clone()` method

### 2. Mutability

- Variables are **immutable by default** (like `const` in C++)
- Use `let mut` keyword for mutable variables
- Prevents accidental modifications

### 3. References & Borrowing

**Two Types of References:**

- **Immutable borrow** (`&T`): Multiple readers allowed
- **Mutable borrow** (`&mut T`): Exclusive write access

**Borrowing Rules:**

1. Either one mutable reference OR any number of immutable references
2. References must always be valid

**Benefits:** Prevents data races at compile time

### 4. Structs, Traits & Methods

- **Structs**: Group related data (no classes in Rust)
- **Methods**: Defined in `impl` blocks, take `&self` or `&mut self`
- **Constructors**: Convention is `pub fn new(...) -> Self`
- **Traits**: Similar to interfaces, define shared behavior
- **Derive Macros**: Auto-generate trait implementations (Debug, Clone, Eq)
- **Tuple Structs**: Structs without named fields

### 5. Enums & Pattern Matching

**Enums:** Combine alternative values (variants can hold data)

**Option<T>:** Rust's null-safe approach

```rust
enum Option<T> {
    None,
    Some(T),
}
```

**Result<T, E>:** Type-safe error handling (no exceptions)

```rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

**Pattern Matching:** Use `match` to handle all cases exhaustively

### 6. Error Handling

- **Recoverable errors**: Use `Result<T, E>` with custom error enums
- **Unrecoverable errors**: Use `panic!()` for bugs
- **Error propagation**: `?` operator for convenient error forwarding
- **Quick failures**: `.unwrap()` and `.expect()` (crash on error)

### 7. Common Collections

**Vec<T>:**

- Growable array on the heap
- Methods: `push()`, `pop()`, `len()`, indexing with `[]`

**String:**

- UTF-8 encoded, growable text
- Methods: `push_str()`, `format!()` macro
- No direct indexing (by design - UTF-8 complexity)

### Why Rust?

- Most admired programming language (Stack Overflow survey)
- Used by Meta, Amazon, Google, Microsoft, Discord, Dropbox
- Efficient performance with memory safety guarantees
- Modern language for server-side development

## Vorlesung 1 - Storage (gesehen)

### Storage: Single-Node DBMSs

**Overview**

This lecture covers the foundational storage layers of database management systems, focusing on how data is organized, stored, and accessed on a single machine.

### Key Topics Covered

**1. Storage Hierarchy**

- **CPU Registers & Caches** (L1/L2/L3): Fastest but smallest (nanoseconds access, MiB capacity)
- **Main Memory (DRAM)**: Fast access (~100ns), GiB capacity
- **Persistent Storage**: HDDs and SSDs (milliseconds to microseconds, TiB capacity)
- Trade-off: Speed vs. capacity vs. cost

**2. Storage Manager**

**Database Files:**

- Tables are mapped to database files consisting of multiple disk blocks
- Two main types:
    - **Unsorted File**: New blocks appended as table grows
    - **Clustered File**: Sorted by an attribute for faster lookups

**Slotted Pages:**

- Pages organized with header, slots (offset + size), and tuple data
- Variable-length data stored from back to front
- Operations: Insert (append + add pointer), Read (follow pointer), Delete (set flag)
- **Record IDs**: Unique identifiers (Page ID + Slot number) used by indexes

**Row vs. Column Store:**

- **Row-Store**: All attributes of a tuple in one page (better for retrieving full rows)
- **Column-Store**: Different pages for individual columns (better for analytical queries on few columns)
- Column-store can be 10x+ faster for queries selecting few columns

**3. Buffer Pool**

**Purpose:** Cache frequently accessed pages in RAM to avoid slow disk I/O

**Architecture:**

- **Page Table**: Tracks which pages are cached and their location in memory
- **Buffer Pool**: Fixed number of frames to hold pages
- **Frames**: Memory slots for cached pages

**Operations:**

- **PIN(pageID)**: Request page; loads from disk if not cached
- **UNPIN(pageID, dirty)**: Release page; mark if modified

**Eviction Strategies:**

- **FIFO**: First-in-first-out (simple queue)
- **LRU**: Least-recently-used (evict oldest accessed page)
- **Clock Algorithm**: Approximates LRU with lower overhead
    - Circular buffer with reference bits
    - Reference bit set to 1 on access
    - Clock hand advances only during eviction, resetting bits until finding victim

**4. Hardware Details**

**Hard Disk Drives (HDDs):**

- Mechanical access: seek time ~3ms
- Sequential access ~200MB/s, random ~100x slower
- Still important for low $/GB cost

**Solid-State Drives (SSDs):**

- No mechanical parts, flash-based storage
- Latency: 10-100μs
- Bandwidth: several GB/s (with parallelism)
- Faster than HDDs but slower than RAM

### Key Takeaways

1. DBMSs must carefully manage the storage hierarchy to achieve good performance
2. Slotted pages enable variable-length data storage with efficient access
3. Buffer pools are essential for caching hot data in memory
4. Eviction policies (Clock/LRU) determine which pages to keep in the buffer
5. Understanding storage device characteristics is crucial for DBMS design

## Vorlesung 2 - Indexing (gesehen)

### Indexing

**Overview**

This lecture covers database indexing strategies to accelerate data retrieval and avoid full table scans.

### Key Topics Covered

**1. Indexing Basics**

**Goal:** Improve speed of point and range lookups on database tables

**Benefits:**

- Faster WHERE, JOIN, ORDER BY, and GROUP BY operations
- Sub-linear search time (O(log n))

**Trade-offs:**

- Slower INSERT, UPDATE, DELETE (index maintenance overhead)
- Additional storage space required
- Must maintain all indexes

**2. Index Types & Classifications**

**By Key:**

- **Primary Index**: Created on primary key
- **Secondary Index**: Created on non-primary key column(s)
- **Composite Index**: Index on multiple columns

**By Physical Organization:**

- **Clustered Index**: Data pages reorganized to match index order (only one per table!)
- **Non-Clustered Index**: Layer of indirection between index and data

**By Density:**

- **Dense Index**: Entry for every record
- **Sparse Index**: One entry per data page (only possible for clustered indexes)

**3. B+ Tree Indexes**

**Structure:**

- Balanced tree with multiple keys per node
- Parameter m (order): Each interior node has [m, 2m] entries (50% minimum occupancy)
- Root has [1, 2m] entries
- Leaf nodes contain data entries and are chained for range scans
- Non-leaf nodes contain only pointers (no data)

**Operations:**

- **Search**: O(log n) - traverse from root to leaf
- **Insert**: O(log n) - may require splitting nodes
    - Split leaf: Copy middle key up to parent
    - Split internal node: Push middle key up to parent
- **Delete**: O(log n) - may require merging (often deferred in practice)
- **Range queries**: Efficient via leaf chain

**Tree Height:**

- Best case: log₂ₘ(n)
- Worst case: ≤ logₘ(n)
- With 100s-1000s keys per node (page size 4-8KB), height stays very low

**Key Properties:**

- Supports both point and range lookups efficiently
- Self-balancing structure
- High fanout reduces tree height dramatically

**4. Hash Indexes**

**Structure:**

- Hash function h(x) maps keys to buckets in array
- Collision resolution via linked lists (chaining)

**Operations:**

- **Search/Insert/Delete**: O(1) average case
- Expected bucket size: n / T.length

**Properties:**

- **Not ordered** - cannot support range queries
- Only efficient for point lookups (equality search)
- Typically kept <70% full to reduce collisions
- Requires rehashing when dataset grows

**5. Practical Considerations**

**Insert Strategies:**

- Classic: Insert and split on overflow
- Alternative: Split proactively during descent (better for high concurrency)

**Delete Strategies:**

- Textbook: Merge underfull nodes
- Practice: Often allow underfull nodes until explicit maintenance (avoids performance impact)

**Clustered vs. Unclustered:**

- Clustered: Data physically ordered by index key (great for range scans)
- Unclustered: Random I/O pattern (slower for multi-row access)

**Sparse Indexes:**

- Only possible for clustered indexes
- One entry per data page instead of per record
- Reduces index size significantly

**6. Index Selection Guidelines**

**OLTP Workloads** (Online Transaction Processing):

- Create/read/update single or few tuples
- Indexes indispensable for performance
- Index maintenance cost can be significant - choose wisely

**OLAP Workloads** (Online Analytical Processing):

- Aggregate queries over large read-mostly datasets
- Range selections, multi-dimensional predicates
- Index maintenance less critical
- Harder to predict which columns need indexes upfront

### Key Takeaways

1. B+ trees are the dominant index structure - support both point and range queries
2. Hash indexes are faster for point lookups but cannot handle ranges
3. Clustered indexes physically reorganize data (only one per table)
4. Tree height is logarithmic and very shallow with large fanout
5. Index design involves trade-offs between query speed and maintenance overhead
6. Practical implementations often defer expensive operations (splits, merges) for better concurrency

## Vorlesung 3 - Distributed Storage (gesehen)

### Storage: Distributed DBMSs

**Overview**

This lecture covers how database systems distribute data across multiple servers within a data center (parallel DBMSs) to enable scalable query processing.

### Key Topics Covered

**1. Why Distribute a Database?**

**Two Main Contexts:**

- **Within Data Centers** (Parallel DBMSs): Improve query performance, parallelize execution, provide fault-tolerance
- **Across Data Centers** (Geo-distributed DBMSs): Disaster resilience, reduce latency, legal/compliance requirements

![grafik.png](attachment:31eed0ed-f929-4454-a430-78660654591a:grafik.png)

HIER REDEN WIR IMMER ÜBER HOMOGENE WITH CORDINATOR

**2. DBMS Architectures**

**Shared-Nothing:**

- Each worker has private portion of data
- Each node runs full DBMS on its local data
- **Pros**: Low latency (no network for data access), simple to implement
- **Cons**: Prone to load imbalance and node failures

![grafik.png](attachment:f68ca0eb-180f-4700-b62b-330f83933c3d:grafik.png)

**Shared-Data:**

- Multiple workers access shared data over network (e.g., via shared storage layer)
- **Pros**: Load balancing, fault-tolerant (any node can access data)
- **Cons**: Higher latency due to network access → Caching

![grafik.png](attachment:85f38bcf-dce1-4842-85df-19ff32777291:grafik.png)

**3. Parallelism Types**

- **Intra-query parallelism**: One query runs in parallel across machines (focus for OLAP)
- **Inter-query parallelism**: Different queries run in parallel (focus for OLTP)

**Performance Metrics:**

- **Speedup**: Fixed data size, growing resources (ideal: linear)
- **Scaleup**: Growing data and resources together (ideal: constant time)

![grafik.png](attachment:5ff98a6d-0c88-445c-b9bc-93bbd932c37b:grafik.png)

**4. Data Distribution**

**Two-Step Process:**

1. **Fragmentation** (aka partitioning/sharding): Divide table into smaller pieces
2. **Allocation**: Assign fragments to servers (may include replication)

**Fragmentation Types:**

- **Horizontal**: Split by rows (typical for parallel DBMSs)
- **Vertical**: Split by columns

**Horizontal Partitioning Schemes:**

**Round-Robin:**

- Assign tuples one-by-one to partitions cyclically
- **Pro**: Avoids partition skew
- **Con**: No pruning possible, no co-partitioning

**Hash Partitioning:**

- Use hash function h(key) → partition number
- **Pros**: Supports pruning for point lookups, avoids skew (with good hash function)
- **Cons**: No pruning for range queries

**Range Partitioning:**

- Define range predicates for assignments (e.g., by date quarters)
- **Pros**: Pruning for both point and range queries
- **Cons**: Sensitive to partition skew

**5. Key Properties of Partitioning**

**Co-Partitioning:**

- Two tables use the same partitioning function on join keys
- Enables **local joins** without network shuffling (critical for performance!)
- Example: Customer and Orders both partitioned by `h(customer_id) = cid % 3`
- Round-robin cannot guarantee co-partitioning

**Partition Pruning:**

- Skip unnecessary partitions during query execution
- Example: Query for `year=2017` only reads partition with recent data
- Hash and range support pruning; round-robin does not

**Data Skew:**

- **Attribute-value skew**: Some values appear much more frequently
- **Partition skew**: Imbalanced distribution even without value skew
- **Solution**: Over-partitioning (# partitions >> # servers) helps with rebalancing

**6. Advanced Partitioning: PREF**

![grafik.png](attachment:045efbbd-9e3d-40a2-9171-3157018c4d21:grafik.png)

**Problem:** Co-partitioning limited to one join key (e.g., can't co-partition Customer+Orders+Parts simultaneously)

**Solution: Predicate-based Reference Partitioning (PREF)**

- Introduces controlled tuple-level redundancy
- Maximizes data locality for distributed joins
- Minimizes data redundancy

**Approach:**

1. Build schema graph with foreign key relationships
2. Compute maximum spanning tree (maximize communication cost savings)
3. Enumerate partitionings and estimate table sizes

- One table gets HASH partitioning (anchor)
- Related tables get PREF partitioning (tuples replicated to match join patterns)

**Results:** 2-5x faster than classical approaches on TPC-H benchmark

**7. Partitioning for OLAP (Star Schema)**

**Strategy:**

1. Co-partition **fact table** and **largest dimension table** on join key
2. Allocate co-located partitions to same servers
3. **Replicate all other dimension tables** to all nodes

**Result:** No network communication needed for fact-dimension joins!

**Challenge:** Multiple large dimensions that don't fit in memory

- Solution 1: Partition all dimensions (requires distributed joins)
- Solution 2: Use PREF for additional large dimensions

**8. Partitioning for OLTP**

**Goal:** Minimize distributed transactions (network latency kills throughput)

**Approach: SCHISM (Schema-Agnostic Graph Partitioning)**

1. **Build transaction graph** from workload trace:
    - Nodes = tuples accessed by transactions
    - Edges = tuples accessed together (weighted by frequency)
2. **Min-cut partitioning**: Minimize sum of edge weights crossing partitions
    - Cutting high-weight edges = more distributed transactions
    - Keeping connected tuples together = more local transactions

**Result:** Workload-driven partitioning that minimizes cross-partition transactions

### Key Takeaways

1. Distributed DBMSs distribute data/workload across multiple servers for scalability
2. Shared-nothing architectures dominate for on-premise parallel DBMSs
3. Co-partitioning on join keys is critical for avoiding expensive distributed joins
4. Hash partitioning provides good balance (pruning + skew avoidance)
5. OLAP: Replicate small dimensions, co-partition fact with largest dimension
6. OLTP: Use workload-aware graph partitioning to minimize distributed transactions
7. PREF enables advanced co-partitioning beyond simple join keys

## Vorlesung 4 - Query Processing (gesehen)

### Query Execution: Single-Node DBMS

**Query Processing in short**

![grafik.png](attachment:d98e62d7-2858-4642-b707-b0b7a74ae01f:grafik.png)

### Key Topics Covered

**1. Execution Models**

**Materialized Execution:**

![grafik.png](attachment:943bce69-bc83-4cfc-9602-dfca5d6826a8:grafik.png)

- Each operator computes its full output before the next operator starts
- Simple to implement but requires buffering intermediate results
- Can be expensive for large intermediate results

**Pipelined Execution:**

![grafik.png](attachment:749ff297-4f5a-4115-8760-5c7a7332ab49:grafik.png)

- Tuples are moved to the next operator immediately
- Avoids storing large intermediates
- Enables pipeline-parallel operator execution
- Implemented via Volcano Iterator Model with three methods:
    - `open()`: Initialize operator state
    - `next()`: Return next result tuple or EOT
    - `close()`: Clean up resources

**Pipeline Breakers:**

- Operators that must materialize results: hash join, sort, aggregation, etc.
- Cannot emit tuples until all input is consumed

**2. Physical Operators: Selection**

**Goal:** Filter tuples matching a predicate (implements WHERE clause)

**Table Scan:**

- Read all pages sequentially
- Check predicate for every tuple
- Cost: M pages (M = number of pages in table)

**Index Scan (B+ Tree):**

- Traverse index to find matching tuples
- Cost: ⌈log_fanout(m)⌉ + N pages (index height + data pages)
- Example: For 50,000 tuples with fanout 250: ⌈log₂₅₀(50,000)⌉+1 ≅ 3 pages

**Index Scan (Hash):**

- Direct lookup for equality predicates
- O(1) average case

**Multi-Attribute Selection:**

- **AND predicates**: Intersect RID sets from multiple indexes
- **OR predicates**: Union RID sets from multiple indexes

**Cost Considerations:**

![grafik.png](attachment:d9ca6c53-45ee-4f45-81f9-04c4abcc8732:grafik.png)

- Index scan faster for **low selectivity** (few matching tuples) wegen IO hat index mehr random access
- Table scan faster for **high selectivity** (many matching tuples) wegen IO
- Random vs. sequential I/O cost differs significantly

![grafik.png](attachment:f822ebae-e6f0-4419-946d-78bbf5fc69bc:grafik.png)

**3. Physical Operators: Join**

![grafik.png](attachment:f023cb1c-7229-4e8f-aa85-a16c21ae3be6:grafik.png)

**Goal:** Combine tuples from two relations matching join predicate (equi-joins: att1 = att2)

**Nested-Loop Join (NLJ) Variants:**

**Naive NLJ:**

- Two nested loops over tuples
- Cost: m + m*n page requests (catastrophically expensive!)
- Example: 7+ hours for 5000x5000 tuple join

**Block NLJ:**

- Iterate over pages instead of tuples
- Cost: M + M*N pages
- Example: 2.5 seconds for same join

**Index NLJ:**

- Use index on inner relation
- Cost: M + m*⌈log_fanout(n)+1⌉ pages
- Example: 15 seconds for same join

**Sort-Merge Join:**

- Requires both inputs sorted on join key
- Single pass over sorted data
- Cost: M + N pages (but requires sorting first!)
- Example: 0.1 seconds for same join (if already sorted)
- Most efficient when inputs are pre-sorted

**Hash Join:**

- Build hash table on smaller relation (build phase)
- Probe with larger relation (probe phase)
- Cost: M + N pages
- Requires hash table to fit in memory

**Grace Hash Join (GHJ):**

- Used when hash table doesn't fit in memory
- **Partition phase**: Hash-partition both R and S using h₁(x)
- **Join phase**: Build hash table for each partition Rᵢ, probe with Sᵢ using h₂(x)
- Ensures matching tuples always in same partition

**Cost Comparison Example** (M=50, N=50, m=n=5000, fanout=1000):

|Algorithm|Cost|Time|
|---|---|---|
|Naive NLJ|25,005,000|~7 hours|
|Block NLJ|2,550|2.5s|
|Index NLJ|15,050|15s|
|Sort-Merge|100|0.1s|
|Hash Join|100|0.1s|

**4. Physical Operators: Sort**

**Purpose:**

- Implements ORDER BY clause
- Required for sort-merge join, DISTINCT, GROUP BY

**Problem:** Input data larger than available memory

**Solution: K-Way Merge Sort**

**Two-Way Merge Sort:**

- **Pass 0**: Sort individual pages (memory for 2 pages)
- **Pass 1+**: Merge pairs of sorted runs (memory for 3 pages: 2 input + 1 output)
- Cost: (log₂(M)+1) * (2*M) page I/Os
- Memory requirement: 3 pages

**K-Way Merge Sort (Generalization):**

- Merge K sorted runs per pass instead of 2
- Requires K+1 pages of memory (K input buffers + 1 output buffer)
- Cost: (log_K(M)+1) * (2*M) page I/Os
- Larger buffer → fewer passes needed

**Example:** With buffer size 17 pages, sorting 1M pages requires ~5 passes vs. ~30 passes for 2-way merge sort

**5. Cost Model Basics**

**Components:**

- **I/O Cost**: #pages_read + #pages_written (dominant factor)
    - Sequential access cost < Random access cost
- **Compute Cost**: Algorithmic complexity

**Overall Cost:** c_IO * cost_IO + c_Compute * cost_Compute

- Constants c_IO >> c_Compute (I/O dominates)

**PostgreSQL Cost Estimation:**

- Uses arbitrary cost units determined by tunable parameters
- `EXPLAIN ANALYZE` shows estimated vs. actual costs

**6. Iterator Model Implementation**

**Selection Iterator:**

```
function open()
    [R.open](<http://R.open>)()
function next()
    while ((r := [R.next](<http://R.next>)()) != EOT)
        if predicate(r) then emit(r)
    return EOT
function close()
    R.close()
```

**Sort Iterator (Pipeline Breaker):**

```
function open()
    [R.open](<http://R.open>)()
    temp = []
    while ((r := [R.next](<http://R.next>)()) != EOT)
        temp.add(r)
    sortedR = sort(temp)  // Materialize!
function next()
    return [sortedR.next](<http://sortedR.next>)() or EOT
function close()
    R.close()
```

### Key Takeaways

1. **Execution models**: Pipelined execution avoids materializing intermediates when possible
2. **Iterator model**: Clean abstraction for operator implementation (open/next/close)
3. **Selection**: Index scans win for low selectivity; table scans for high selectivity
4. **Joins**: Block NLJ is baseline; hash join and sort-merge join are most efficient
5. **Co-partitioning**: Critical for avoiding expensive distributed joins
6. **Sorting**: K-way merge sort enables external sorting with limited memory
7. **Cost estimation**: I/O dominates; random access much more expensive than sequential
8. **Pipeline breakers**: Some operators (sort, hash join build phase) must consume all input before producing output

## Vorlesung 5 - Distributed Query Processing (gesehen)

### Query Processing: Distributed DBMS

**Overview**

This lecture covers how distributed database systems execute queries in parallel across multiple nodes, focusing on partition-parallel execution and data shuffling strategies.

### Key Topics Covered

**1. Partition-Parallel Query Execution**

**Basic Pattern:**

- Execute relational operators in parallel on different partitions
- Example: Selection query runs independently on each partition, results merged with UNION
- Simple for operators like selection and projection
- More complex for operators like sort, aggregation, and joins

**Operators:**

- **Trivial to parallelize**: Selection, projection
- **Requires coordination**: Sort, aggregation, join

**2. Data Shuffling (Re-Partitioning)**

**Core Concept:**

- Key mechanism to enable parallel execution of complex operators
- Implemented via send/receive operators that redistribute data across nodes
- Makes relational operators "unaware" of distributed execution

**Shuffle Types:**

- **Range-based N:M**: Partition by value ranges (e.g., age 0-40, 41-99)
- **Hash-based N:M**: Partition by hash function h(k)
- **Replicate N:M**: Broadcast data to all nodes
- **N:1**: Gather all data to single node (no partitioning function)

**3. Distributed Sort**

**Three-Step Process:**

1. **Sort partitions locally** (e.g., sort by age on each node)
2. **Re-partition on sort key** using range-based shuffling
3. **Sort re-partitioned data** (can use merge-sort on sorted runs)

**Result:** Globally sorted data distributed across nodes

**4. Distributed Aggregation**

**Without GROUP BY:**

- Aggregate locally on each partition
- Shuffle using N:1 (gather to single node)
- Post-aggregate on collected results

**Aggregate Function Handling:**

- **SUM, MIN, MAX**: Direct application
- **COUNT**: Rewrite to use SUM for post-aggregation
- **AVG**: Rewrite to SUM/COUNT locally
- **COUNT DISTINCT**: Can only eliminate duplicates locally

**With GROUP BY:**

- Aggregate locally per group
- Re-partition on group-by key using N:M shuffle
- Post-aggregate on re-partitioned data

**Shuffle Options:** Hash or range partitioning on group key

**5. Distributed Joins**

**Challenge:** Most expensive distributed operation due to large intermediate results requiring shuffling

**Three Main Strategies:**

**A) Symmetric Repartitioning (Hash Join):**

- Shuffle **both** tables on join key using same hash function
- Join locally on each node
- **Cost:** Both tables shuffled over network
- **When to use:** Tables of similar size

**B) Asymmetric Repartitioning:**

- One table already partitioned on join key
- Shuffle **only other table** to match partitioning
- **Cost:** Only one table shuffled
- **When to use:** One table already co-partitioned

**C) Broadcast Join (Fragment-Replicate):**

- Replicate **smaller table** to all nodes
- Join with local partitions of larger table
- **Cost:** Small table sent to all nodes
- **When to use:** One table much smaller than the other

**Example:** For multi-table joins (S₁⨝S₂⨝S₃):

- Symmetric: Requires multiple shuffle rounds
- Broadcast: Replicate small tables, shuffle large table once

**6. Semi-Join Reduction**

**Goal:** Reduce data transferred during joins

**Five-Step Process:**

1. Compute distinct projection on join key of remote partition
2. Ship projection to local node
3. Execute semi-join to filter local table (select only tuples with join partners)
4. Send filtered result to remote node
5. Join locally on remote node

**Result:** Only tuples that will actually join are transferred

**Trade-off:**

- **Effective** when semi-join has high selectivity (filters many tuples)
- **Inefficient** when most tuples needed anyway (extra overhead without benefit)
- **Decision:** Requires cost-based query optimization

**7. Hypercube Shuffling**

**Problem:** Multi-table joins with symmetric repartitioning require shuffling same data multiple times

**Solution: Hypercube-Based Shuffling**

- Organize workers as hypercube with one dimension per join key
- Each worker identified by coordinates (i, j, k)
- Each table shuffled **only once** to multiple nodes simultaneously

**Example:** S₁(X₁,X₂) ⨝ S₂(X₂,X₃) ⨝ S₃(X₃,X₁) with p=8 workers

- Hypercube: 3 dimensions (X₁, X₂, X₃), each with p₁=p₂=p₃=2 nodes
- S₁(x₁,x₂) sent to coordinates (h₁(x₁), h₂(x₂), ⋆)
- S₂(x₂,x₃) sent to coordinates (⋆, h₂(x₂), h₃(x₃))
- S₃(x₃,x₁) sent to coordinates (h₁(x₁), ⋆, h₃(x₃))
- Local joins execute on all nodes in parallel

**Performance:** 10-20x faster than naive reshuffling on complex join queries

**Optimal Share Allocation:**

- Must factorize p = p₁ × p₂ × ... × pₖ
- Optimal when p^(1/k) is integer (equal dimensions)
- Otherwise: Enumerate all valid factorizations, estimate network cost, choose minimum
- Tie-breaking: Prefer more evenly sized dimensions (reduces skew)

**8. Announcements from Lecture**

- **Exam registration deadline:** 18.11.2025 (noted as "TODAY" in slides)
- Lab 1 projects created for late sign-ups
- Lab 1 takes more time than Lab 0 - start early

### Key Takeaways

1. **Partition-parallelism** enables execution of relational operators across nodes
2. **Data shuffling** is the core mechanism for coordinating distributed operators
3. **Sort** requires local sort → range shuffle → merge sorted runs
4. **Aggregation** uses local aggregation → shuffle → post-aggregation pattern
5. **Joins** have three strategies: symmetric repartition, asymmetric repartition, broadcast
6. **Semi-join reduction** minimizes data transfer when selectivity is high
7. **Hypercube shuffling** optimizes multi-table joins by shuffling each table only once
8. **Trade-offs** between strategies depend on data sizes, selectivity, and network cost

## Vorlesung 6 - Query Optimization (gesehen)

### Query Optimization: Single Node & Distributed

**Overview**

This lecture covers query optimization techniques in DBMSs, focusing on cost-based optimization for both single-node and distributed systems. Query optimization is decisive for query performance.

### Key Topics Covered

**1. Query Optimization Phases**

**Two Sequential Phases:**

1. **Rule-based optimization**: Transforms logical plan using rewrite rules (e.g., selection pushdown, cross-product replacement)
2. **Cost-based optimization**: Enumerates plan alternatives and picks one with lower runtime cost

**Cost-Based Optimization Steps:**

1. **Join ordering**: Find best join order using logical plan
2. **Physical planning**: Select best physical operator for each logical operator

**2. Cardinality Estimation**

**Purpose:** Estimate intermediate result sizes without executing the plan

**Basic Selectivity Formulas:**

- **Selection**: sel(p) := |σₚ(R)| / |R|
    - sel(att=constant) = 1/|att| (uniform distribution assumption)
    - sel(att in range) = |range|/|att|
    - sel(p₁ AND p₂) = sel(p₁) × sel(p₂)
    - sel(p₁ OR p₂) = sel(p₁) + sel(p₂) - sel(p₁) × sel(p₂)
- **Join**: sel(R ⨝ S) := |R ⨝ S| / (|R| × |S|)
    - General formula: sel(R ⨝ₐ₌ᵦ S) := 1/max(|a|, |b|)
    - FK-PK join: sel(R ⨝ₐ₌ᵦ S) := |S| / (|S| × |R|)

**Limitations of Basic Estimation:**

- Assumes uniform data distribution
- Assumes all columns are independent (uncorrelated)
- Errors accumulate quickly in multi-join queries

**3. Improving Cardinality Estimates**

**Histograms:**

- Model data distributions more accurately than uniform assumption
- **Equal-width histograms**: Divide domain into equal-sized bins
- **Equal-depth histograms**: Ensure similar number of tuples per bin (better for skewed data)
- **Uniformity assumption within buckets**: Estimate selectivity by interpolation
- **Most Common Values (MCVs)**: Track heavy hitters separately to handle outliers

**PostgreSQL Statistics:**

- Stores histograms and MCVs for each column in `pg_stats`
- Uses these for more accurate selectivity estimation

**Other Techniques:**

- **Sampling**: Random sampling from tables to estimate selectivity
- **Parameterized distributions**: Model data with statistical distributions (e.g., Gaussian)
- **Learned cardinality estimation**: Use ML models to predict cardinalities (captures correlations, but requires 10Ks of training queries)

**Bigger Joins (Multi-Table):**

- Treat intermediate results as new tables
- Estimate statistics from base table statistics
- **Challenge**: Statistics on intermediate results are less accurate (no histograms available)

**4. Join Ordering (Plan Space Enumeration)**

**Problem:** Search space grows factorially with number of tables

- 3 tables: 12 possible join trees
- 4 tables: 120 plans
- 10 tables: 17.6 billion plans

**Solution: Dynamic Programming (DP)**

- Compose best plans with n tables from best plans of n-1 tables
- **Complexity**: O(3ⁿ) for bushy trees (much better than n! exhaustive search)
- **Example algorithm**:
    1. Start with single-table access plans (base case)
    2. Iteration 1: Find best 2-table join plans
    3. Iteration 2: Find best 3-table join plans (using best 2-table plans)
    4. Continue until all tables joined

**Cost Model for Join Ordering:**

- Sum of intermediate result sizes (cardinalities)
- Logical plan cost ≅ Σ all cardinalities in plan

**Example:** Customer ⨝ Orders ⨝ LineItem query

- Filter on Customer first (reduces intermediate size)
- Join with Orders, then LineItem
- Different join orders have vastly different costs

**5. Physical Operator Selection**

**Goal:** Choose physical implementation for each logical operator

**Physical Cost Model:**

- Combination of **CPU cost** and **I/O cost** (random + sequential)
- Weighted by "magical" constant factors (system-specific)

**PostgreSQL Cost Parameters:**

- `seq_page_cost = 1`
- `random_page_cost = 4`
- `cpu_tuple_cost = 0.01`
- `cpu_index_tuple_cost = 0.005`
- `cpu_operator_cost = 0.0025`

**Example Join Operator Selection:**

- Hash join vs. sort-merge join vs. nested-loop join
- Index nested-loop join (if index available)
- Choice depends on table sizes, available indexes, sort order

**6. Distributed Query Optimization**

**Two-Phase Approach:**

1. **Ignore distribution**: Find best single-node plan (using traditional optimizer)
2. **Parallelize operations**: Choose parallel operator implementations that minimize network cost

**Shuffle Cost Estimation:**

For n nodes, tables R and S:

|Join Algorithm|Total Network Cost (# tuples)|
|---|---|
|Symmetric Repartition||
|Asymmetric Repartition||
|Broadcast (Replicate)||

**Decision Heuristics:**

- **Symmetric repartition**: Tables of similar size
- **Asymmetric repartition**: One table already co-partitioned on join key
- **Broadcast**: One table much smaller than the other (avoid if result of broadcast is large!)

**Example Optimization:**

- Query: Customer ⨝ Orders ⨝ LineItem (all hash-partitioned, not on join keys)
- Best plan: Broadcast filtered Customer (small after filter), symmetric repartition Orders and LineItem
- Shuffle costs computed for each join, best alternative selected

**7. Key Challenges**

**Query Optimization is NOT Solved:**

- Traditional optimizers struggle with complex queries
- Cardinality estimation errors compound exponentially
- Learned approaches (ML models) show promise but require extensive training data

**Research Directions:**

- **Learned cardinality estimation**: Neural networks predict cardinalities (e.g., Kipf et al. 2019)
- **Adaptive query execution**: Adjust plan during execution based on actual cardinalities
- **Workload-aware optimization**: Learn from past queries to improve future plans

### Key Takeaways

1. **Cost-based optimization** enumerates plans and estimates runtime to select best plan
2. **Cardinality estimation** is fundamental - errors lead to poor join ordering
3. **Histograms and MCVs** significantly improve estimation accuracy over uniform assumption
4. **Dynamic programming** makes join ordering tractable (O(3ⁿ) vs. factorial)
5. **Physical operator selection** uses detailed cost models combining I/O and CPU costs
6. **Distributed optimization** adds network shuffle costs to decision-making
7. **Broadcast joins** win when one input is small; symmetric repartition for similar-sized tables
8. **Query optimization remains challenging** - even modern optimizers can make poor decisions

## Vorlesung 7 - OLAP (gesehen)

### DBMS Analytics: Single Node & Distributed (OLAP)

**Overview**

This lecture covers Online Analytical Processing (OLAP) systems, focusing on query processing techniques, specialized index structures, and distributed execution strategies for analytical workloads.

### Key Topics Covered

**1. OLAP vs. OLTP**

![grafik.png](attachment:4f412252-3d05-440f-a62b-b62710a6dcbe:grafik.png)

**Two Types of Database Workloads:**

- **OLTP (Online Transaction Processing)**:
    - Mix of writes and simple queries
    - Example: `SELECT address FROM customer WHERE cid=101`
    - Operational systems (e.g., online shopping, ERP)
- **OLAP (Online Analytical Processing)**:
    - Data-intensive, complex queries
    - Example: `SELECT SUM(price) FROM orders GROUP BY product ORDER BY ...`
    - Decision support (e.g., find best-selling products in 2025)

**OLAP DBMSs:** Amazon Redshift, Google BigQuery, Snowflake

- Optimized for read-only queries (table scans, join-heavy)
- Either single-node or distributed

**OLTP DBMSs:** Amazon Aurora, Google AlloyDB

- Optimized for concurrent transactions (updates + reads)
- Mainly single-node or replicated

![grafik.png](attachment:44c98c87-a166-4863-9076-aef5c4fbc0f3:grafik.png)

**2. OLAP Data Model**

**Star Schema:**

- **Fact Table**: Contains measures (e.g., revenue, price) and foreign keys to dimensions
- **Dimension Tables**: Describe aspects (e.g., Time, Location, Product, Payment)
- Star-shaped structure: Fact table at center, dimensions radiate outward

**Data Cubes:**

- use own datamodel
- Logical organization as multi-dimensional array
- Each dimension describes different aspect (products, locations, time)
- Facts are key figures for analysis (revenue, returns)

**OLAP Operations:**

![grafik.png](attachment:d6ce56ec-54c1-41f1-a5ef-d5bbc00497c2:grafik.png)

- **Slice**: Select one value from a dimension
- **Dice**: Select subset of values from multiple dimensions

![grafik.png](attachment:eb2bb3fd-2ae1-4985-a523-a41e0696c8f0:grafik.png)

- **Roll-up**: Aggregate to higher level (e.g., cities → countries)
- **Drill-down**: Disaggregate to lower level (e.g., quarters → months)

**Implementation:**

- **MOLAP**: Native multidimensional arrays (niche products)
- **ROLAP**: Relational databases with star schema (dominant approach)

![grafik.png](attachment:c01f2ab9-e38e-48df-a068-9750bac16d52:grafik.png)

![grafik.png](attachment:dfffcd42-33ce-49b4-997b-c901d0047652:grafik.png)

**3. OLAP Query Processing**

**Typical OLAP Query Pattern:**

```sql
SELECT <dimensions>, <aggregation-function(measure)>
FROM F, D1, D2, ..., Dn
WHERE <join-conditions>
  AND <filter-conditions>
GROUP BY <dimensions>
```

**Three Execution Strategies:**

**Naive Join Strategy:**

- Incrementally join fact with dimension tables
- **Problem**: Many large intermediate results
- Example: 10M fact table joined with 4 dimensions → 10M, 2M, 1M, 100K intermediates

**Cross Product Plan:**

- Create cross product of all dimension tables first, then join with fact
- Dimension tables usually much smaller than fact
- **Problem**: Cartesian products can still get large with many dimensions

**Semi-Join Plan (Best):**

- Use semi-joins to identify relevant fact table rows before joining
- Steps:
    1. Use semi-joins to get RID lists from each dimension
    2. Intersect RID lists to find matching fact table rows
    3. Select only matching rows from fact table
    4. Join with dimension tables
- **Benefit**: Minimizes intermediate result sizes

**4. Bitmap Indexes**

**Purpose:** Efficiently support multi-dimensional queries on OLAP data

**Structure:**

- One bit-vector B_v for each distinct value v of a column
- Bit-vector size = number of rows in table
- Bit at position n set to "1" if row n has value v

**Advantages:**

- **Efficient multi-dimensional queries**: Use bitwise AND/OR/NOT to combine predicates
- **Fast bitwise operations**: Modern CPUs process 64-512 bits at once (SIMD)
- **Read-optimized**: Update performance doesn't matter for read-mostly OLAP

**Optimizations:**

**Decomposed Bitmap Indexes:**

- Reduce space for large domains
- Decompose values into digits: v = v₂×10² + v₁×10¹ + v₀×10⁰
- Example: 0-999 domain needs 3×10=30 bit-vectors instead of 1000
- Trade-off: Lower space but more complex queries

**Range-Encoded Bitmap Indexes:**

- Better support for range queries
- Bit-vector B_v set to "1" if value ≥ v (not equal)
- Range query [a, b]: Compute B_a AND NOT B_{b+1}
- Reduces bit-vectors needed for range queries from many to just 2

**5. Join Indexes**

**Purpose:** Find relevant fact table rows based on dimension filters without joining

**Two Types:**

**Type 1 (RID-based):**

- Mapping: Dimension.RID → {Fact.RID}
- Input: Row ID of dimension table
- Output: Set of fact table row IDs that join with that dimension row

**Type 2 (Attribute-based):**

- Mapping: Dimension.attribute → {Fact.RID}
- Input: Attribute value from dimension table
- Output: Set of fact table row IDs matching that attribute value
- **Benefit**: Combines selection and semi-join in one operation

**Usage in Semi-Join Plan:**

- Bitmap indexes answer selections on dimensions
- Join indexes answer semi-joins with fact table
- Result: RID list for fact table without expensive joins

**6. Distributed OLAP**

**Partitioning Strategy for Star Schema:**

1. **Co-partition fact table and largest dimension** on join key
2. **Allocate co-located partitions to same servers**
3. **Replicate all other (small) dimension tables to all nodes**

**Result:** No network communication needed for fact-dimension joins!

**Example:**

- Partition Sales (fact) and Product (largest dim) by `h(product_id) mod N`
- Place Sales_i and Product_i on same Node i
- Replicate Time, Location, Payment dimensions to all nodes
- All joins execute locally in parallel

**Challenge: Multiple Large Dimensions**

- **Solution 1**: Partition all dimensions → requires distributed joins
- **Solution 2**: Use PREF (Predicate-based Reference Partitioning) for additional large dimensions

**Query Execution:**

- Semi-join plans execute in parallel on each node
- Final aggregation gathers results from all nodes
- Partition pruning skips irrelevant nodes based on filters

### Key Takeaways

1. **OLAP systems** optimize for read-heavy analytical queries over large datasets
2. **Star schema** organizes data with central fact table and dimension tables
3. **Semi-join plans** minimize intermediate results by filtering fact table first
4. **Bitmap indexes** enable fast multi-dimensional queries via bitwise operations
5. **Join indexes** precompute fact-dimension relationships to avoid expensive joins
6. **Range-encoded bitmaps** optimize range queries with minimal bit-vectors
7. **Distributed OLAP** uses co-partitioning and replication to avoid network shuffling
8. **Specialized indexes** (bitmap, join) are crucial for OLAP performance

## Vorlesung 8 - OLTP CC (gesehen)

### Summary

**Focus:** Concurrency control mechanisms for OLTP (Online Transaction Processing) systems

**1. ACID Properties & Transactions**

- **Atomicity**: All-or-nothing execution of operations
- **Consistency**: Database moves from one valid state to another
- **Isolation**: Concurrent transactions don't interfere with each other
- **Durability**: Committed changes persist despite failures

**2. Concurrency Control Problems**

- **Lost Update**: Two transactions read same value, both update, one update is lost
- **Dirty Read**: Transaction reads uncommitted data from another transaction
- **Non-Repeatable Read**: Same query returns different results within transaction
- **Phantom Read**: New rows appear/disappear during transaction execution

Types

![grafik.png](attachment:c9fedc4d-5496-4841-8b91-a861196cdfa7:grafik.png)

![grafik.png](attachment:0a5788cb-6c01-4f97-b85e-0946f096fd2b:grafik.png)

**3. Serializability**

- **Conflict Serializability**: Schedule equivalent to some serial execution of transactions
- **Precedence Graph**: Directed graph to test serializability (cycle = not serializable)
- **View Serializability**: Weaker condition based on final database state

**4. Locking Mechanisms**

![grafik.png](attachment:efca76e3-0458-48fe-b5b0-12cab6650943:grafik.png)

**Two-Phase Locking (2PL):**

- **Growing Phase**: Acquire locks, cannot release any locks
- **Shrinking Phase**: Release locks, cannot acquire new locks
- Guarantees conflict serializability but can cause cascading aborts

**Strict Two-Phase Locking (S2PL):**

- Hold all exclusive locks until commit/abort
- Prevents cascading aborts and dirty reads
- Most common protocol in commercial DBMSs

**5. Lock Types & Granularity**

- **Shared Lock (S)**: Multiple transactions can read simultaneously
- **Exclusive Lock (X)**: Only one transaction can write, blocks all others
- **Intention Locks (IS, IX, SIX)**: Hierarchical locking for multi-granularity (table/page/row)

**6. Deadlock Handling**

**Detection:**

- Wait-for graph: Nodes are transactions, edges indicate waiting for locks
- Cycle in graph = deadlock detected
- Resolution: Abort victim transaction (lowest cost or youngest)

**Prevention:**

- **Wait-Die**: Older transaction waits, younger aborts
- **Wound-Wait**: Older transaction forces younger to abort, younger waits

**7. Optimistic Concurrency Control (OCC)**

- **Read Phase**: Transaction reads data into private workspace
- **Validation Phase**: Check for conflicts with other transactions
- **Write Phase**: If validated, apply changes to database
- **Advantage**: No locking overhead, good for read-mostly workloads
- **Disadvantage**: High abort rate with write-heavy workloads

**8. Multiversion Concurrency Control (MVCC)**

- Maintain multiple versions of each data item with timestamps
- Readers access appropriate version without blocking writers
- Writers create new versions without blocking readers
- Used by PostgreSQL, Oracle, MySQL InnoDB

**9. Isolation Levels (SQL Standard)**

- **Read Uncommitted**: Allows dirty reads (weakest)
- **Read Committed**: Prevents dirty reads
- **Repeatable Read**: Prevents dirty and non-repeatable reads
- **Serializable**: Prevents all anomalies (strongest)

**10. Snapshot Isolation**

- Each transaction sees consistent snapshot of database at start time
- Write-write conflicts detected at commit time
- Prevents most anomalies but allows write skew
- Popular in modern distributed databases

### Key Takeaways

1. **ACID properties** ensure reliable transaction processing in OLTP systems
2. **Serializability** is the gold standard for isolation but comes with performance cost
3. **2PL/S2PL** are fundamental locking protocols that guarantee serializability
4. **Deadlock detection** uses wait-for graphs; prevention uses timestamp ordering
5. **MVCC** enables high concurrency by avoiding reader-writer conflicts
6. **Isolation levels** provide trade-off between consistency and performance
7. **Snapshot isolation** balances strong consistency with good performance
8. **Lock granularity** (row vs. table) affects concurrency and overhead

## Vorlesung 9 - OLTP Logging (gesehen)

### Summary

**Focus:** Recovery mechanisms and logging protocols for OLTP (Online Transaction Processing) systems

**1. Transaction States & Recovery**

- **ACTIVE**: Transaction is executing
- **PARTIALLY COMMITTED**: Final statement executed, but not yet committed
- **COMMITTED**: Transaction successfully completed
- **FAILED**: Normal execution can no longer proceed
- **ABORTED**: Transaction rolled back, database restored to state before transaction started

**2. Failure Types**

- **Transaction Failure**: Logical errors, system errors, or deadlocks
- **System Crash**: Power failure, hardware/software errors (volatile storage lost, stable storage survives)
- **Disk Failure**: Physical damage to storage media (requires backups/replication)

**3. Write-Ahead Logging (WAL) Protocol**

- **Core Principle**: Log records must be written to stable storage before corresponding data pages
- **Rule 1**: Before a data page is written to disk, all log records describing changes to that page must be on stable storage
- **Rule 2**: Before commit acknowledgment, all log records for the transaction must be on stable storage
- **Benefit**: Enables both REDO (reapply committed changes) and UNDO (rollback uncommitted changes)

**4. Log Record Types**

- **Update Log Record**: Contains transaction ID, data item, old value, new value
- **Commit Record**: Marks successful transaction completion
- **Abort Record**: Marks transaction rollback
- **Checkpoint Record**: Contains list of active transactions (for efficient recovery)
- **Compensation Log Record (CLR)**: Describes undo actions during rollback

**5. ARIES Recovery Algorithm**

**Three Phases:**

1. **Analysis Phase**: Scan log forward from last checkpoint to determine which transactions committed/aborted and which pages were dirty
2. **REDO Phase**: Scan log forward from earliest dirty page, reapply all changes (even for aborted transactions)
3. **UNDO Phase**: Scan log backward, undo changes of uncommitted transactions

**Key ARIES Features:**

- **Repeating History**: REDO all changes to restore database to exact state at crash
- **Logging Changes During UNDO**: CLRs ensure UNDO is idempotent (can be repeated safely)
- **Physiological Logging**: Physical page identification with logical operation description

**6. Checkpointing**

- **Purpose**: Reduce recovery time by periodically flushing committed changes to disk
- **Fuzzy Checkpointing**: Non-blocking checkpoint that records dirty pages and active transactions without stopping system
- **Checkpoint Record Contains**: List of active transactions, dirty page table (DPT)
- **Recovery Starts From**: Last successful checkpoint (not from beginning of log)

**7. Log Sequence Numbers (LSN)**

- **Monotonically Increasing**: Each log record gets unique LSN
- **pageLSN**: Stored on each page, indicates LSN of last update to that page
- **recLSN**: First log record that made page dirty since last flush
- **Usage**: Determines which log records must be REDOne during recovery

**8. Dirty Page Table (DPT)**

- Tracks which pages have been modified in buffer but not yet written to disk
- Maps page ID to recLSN (recovery LSN - when page first became dirty)
- Used during REDO phase to determine starting point for recovery

**9. Transaction Table (TT)**

- Tracks active transactions during normal operation
- Contains transaction ID, status, lastLSN (most recent log record for transaction)
- Used during recovery Analysis phase to identify uncommitted transactions

**10. Shadow Paging (Alternative to Logging)**

- **Mechanism**: Maintain two page tables - current and shadow
- **Updates**: Copy-on-write creates new pages, leaving old versions intact
- **Commit**: Atomically switch current pointer to new page table
- **Disadvantages**: Fragments storage, poor for concurrent transactions, high overhead
- **Usage**: Rare in modern systems; logging dominates

### Key Takeaways

1. **WAL protocol** is fundamental to crash recovery in OLTP systems
2. **ARIES** is the standard recovery algorithm used in most commercial databases
3. **Checkpointing** reduces recovery time by limiting log scanning
4. **LSNs and DPT** enable efficient determination of what needs to be REDOne
5. **REDO is physical** (page-level), **UNDO is logical** (operation-level)
6. **CLRs ensure idempotent UNDO** - can safely repeat undo operations
7. **Analysis phase** reconstructs system state at time of crash
8. **Logging overhead** is acceptable because sequential writes to log are fast

## Exercise

### Exercise Sheet 1: Storage Management

3 x 4 + 128 = 140 pro Tuple oder 4 (offset) + 4 (size) + 3 x 4 (integer) + 100/120 (string average size) = 120/140

**Topics Covered:**

- **Slotted Pages**: Calculating bytes per tuple and tuples per page for fixed-sized vs. variable-length storage
- **LRU Eviction Policy**: Determining eviction sequence for buffer manager with 6 frames
- **Clock Algorithm**: LRU approximation with reference bits and circular buffer hand
- **Clock Algorithm with Pinning**: Handling pinned pages that cannot be evicted

**Key Concepts:**

- Fixed-sized slots waste space but are simpler; slotted pages use offset+length for variable-length data
- LRU evicts least-recently-used pages based on access timestamps
- Clock algorithm approximates LRU with lower overhead using reference bits
- Pinned pages are skipped during eviction (hand moves over them without resetting reference bit)

### Exercise Sheet 2: Indexing

**Topics Covered:**

- **Index Types**: Clustered vs. unclustered, sparse vs. dense indexes
- **B+ Tree Operations**: Insert with node splitting, handling overflow
- **B-Tree Operations**: Insert with node splitting, delete with rotation/merging (M=2)

**Key Concepts:**

- Sparse indexes only work with clustered indexes (data physically sorted)
- B+ trees keep data only in leaves; internal nodes just for navigation
- Insert algorithm: Add to leaf, split if overflow, push middle key up to parent
- Prefer rotation over merging to maintain 50% occupancy

### Exercise Sheet 3: Distributed Storage Management

**Topics Covered:**

- **Amdahl's Law**: Calculating speedup from parallelization with overhead
- **Fragmentation & Allocation**: Horizontal vs. vertical fragmentation, partitioning schemes (round-robin, range, hash)
- **Co-partitioning**: Enabling local joins without network shuffling
- **PREF (Predicate-based Reference Partitioning)**: Controlled replication to maximize join locality

**Key Concepts:**

- Overall speedup S = 1/((1-p) + p/s) where p = parallelized fraction, s = speedup factor
- Co-partitioning requires tables partitioned on same join key with same function
- Range partitioning enables pruning but can cause skew
- PREF replicates tuples strategically to enable co-partitioning for multiple join keys

### Exercise Sheet 4: Query Processing (Single-Node)

**Topics Covered:**

- **Join Operator Costs**: I/O cost comparison for Block NLJ, Hash Join, Sort-Merge Join
- **Buffer Requirements**: Memory frames needed for each join algorithm
- **Pipeline Breakers**: Identifying operators that block execution (Hash Join) vs. non-blocking (Nested Loop Join)

**Key Concepts:**

- Block NLJ cost: N + M×N pages (requires 2 frames)
- Hash Join cost: M + N pages (requires hashtable size + 1)
- Sort-Merge Join cost: (ceil(log₃(N)) + 1) × 2 × N + M + N for 3-way merge sort
- Hash Join is pipeline breaker (must build hashtable); NLJ is not

### Exercise Sheet 5: Distributed Query Processing

**Topics Covered:**

- **Parallel Join Strategies**: Symmetric repartitioning, asymmetric repartitioning, broadcast join
- **Network Cost Calculation**: Tuple transfer costs for each join strategy
- **Semi-Join Reduction**: Reducing data transfer by filtering tuples before shipping

**Key Concepts:**

- Symmetric repartition cost: (|A| + |B|) × (nodes-1)/nodes tuples
- Asymmetric repartition cost: |B| × (nodes-1)/nodes tuples (A already partitioned)
- Broadcast cost: |A| × (nodes-1) tuples
- Semi-join effective when it eliminates >50% of tuples; otherwise overhead not worth it

### Key Takeaways

1. **Cost-based optimization** enumerates plans and estimates runtime to select best plan
2. **Cardinality estimation** is fundamental - errors lead to poor join ordering
3. **Histograms and MCVs** significantly improve estimation accuracy over uniform assumption
4. **Dynamic programming** makes join ordering tractable (O(3ⁿ) vs. factorial)
5. **Physical operator selection** uses detailed cost models combining I/O and CPU costs
6. **Distributed optimization** adds network shuffle costs to decision-making
7. **Broadcast joins** win when one input is small; symmetric repartition for similar-sized tables
8. **Query optimization remains challenging** - even modern optimizers can make poor decisions

## Storage Management
#### Database Files
* Wie die eigentlichen Tabellen auf Festplatte abgelegt werden
	* Unsorted := Neue Tabellen einträge werden einfach angehängt
	* Clustered := Die File ist sortiert (Faster access aber höhere maintnance)
* Kann fixed-sized oder slotted sein siehe unten
## Indexing
Trade-off := slower isnert,update delete (higher maintenance); more storage space; indexing takes time
Clustered Index := Pages (Speicherblöcke auf Festplatte) reorganized as part of the index structure
Non-Clustered Index := There is a layer of indirection between index and pages
Sparse Index := A clustered index is sparse if the index only contains one entry for each data page
Dense Index := A clustered index is dense if the index contains an entry for every data entry
#### Hash Index
* Not ordered mapping
* efficient point lookup
#### (Balanced)B-Tree Structure
B+-Tree := tree struct on top of sorted order; nur leaf nodes haben die eigentlichen elemente; point und range lookup efficiently; leaf nodes often linked
B-Tree := alles sind elemente
##### Insert
1. In Node inserten als wäre nix (mit overfill halt)
2. Wenn Node übefüllt, dann splitten und 2 elemente nach links und 3 elemente nach rechtss
3. das erste element der rechten node nach oben einsetzen und alles wiederholen wenn nötig
4. !!! Im leaf wird nix gelöscht aber ansonsten können propagierte lemente gelöscht werden (gilt nur im B+-Tree)
## Distributed Data
* Verteilung auf mehrere Server für resillienzm geringere Zugriffszeiten, legale Gründe
* Verteilung innerhalb Servern für Parallelisierung, fault-tolerance, load-balancing
* SHARED-NOTHING (data partitioned accross workers) := each worker can run query on therr share of data; low latency; simple to implement; - load imbalance + node failure
* SHARED-DATA := workers can run queries on any part of data, + load balancing; + fault tolerant; higher latency (data access over network)
#### Partitioning Scheme sollte haben
* Support co-partitioning
* Enable pruning
* avoid data-distr skew (one node has more data than another)
	* Attribte-value skew (manche values kommen einfach öfter vor)
	* parition skew (schlecht gewählte range oder so)
#### Predicate-based reference partitioning
![[Pasted image 20260312114252.png]]




## Query Procession
![[Pasted image 20260312121439.png|600]]
![[Pasted image 20260312122004.png|600]]
## Equi-Joins
![[Pasted image 20260312123518.png|600]]
![[Pasted image 20260312122850.png|600]]
![[Pasted image 20260312123138.png|600]]
![[Pasted image 20260312123203.png|600]]
Needs 2 Frames
![[Pasted image 20260312123224.png|600]]
![[Pasted image 20260312123357.png|600]]
## Distributed Join
![[Pasted image 20260312135518.png|600]]
![[Pasted image 20260312135541.png|600]]
![[Pasted image 20260312135619.png|600]]
![[Pasted image 20260312135925.png|600]]

## Parallel Joins
#### Networkcost
Symmetric Repartitioning (random initial partition)
|TableA| * (1 - (1 / # nodes)) + ...

Asymmetric Repartitioning
Wie symmetric aber eben nur für Table X das repart. muss

Replication/Broadcast: Replicate A
A muss repl daher:
|A| * (# nodes - 1)


## 2 Steps Datenverteilung = Fragmentation + Allocation
Fragmentation := Divide Table in pieces (data to large, parallel computing, pruning)
Replication := Replicate fragemnts to multiple nodes (avoid hot spots, fault tolerance, better load balancing, higher update cost)
Allocation := decide where fragments go (round robin, range-partitioning, hash partitioning)

## OLAP (Online Analytical Processing)
OLAP-Cube := Multidim array of data
Slice/Dice := Aus Cube slice oder dice-abschnitt bekommen
Roll-Up := Eine dimension gröber machen (Städte -> Länder)
Drill-Down := Eine dimension feiner machen (Quartale -> Monate)
![[Pasted image 20260313155835.png|600]]

### Variants of Slotted pages
#### Fixed-sized tuple page
Bytes per Tuple: Alle Attribute mit max Länge (also wenn VarChar mit max Länge X dann X nehmen und nicht die durchschnittliche Länge)
Tuples per Page: (Pagesize - Header) / Bytes per Tuple
#### Variable-sized tuple slotted page
Bytes per Tuple: Alle Attribute mit average size + Offset + Slot Length
Tuples per Page: (Pagesize - Header) / Bytes per Tuple

---
### Eviction Policys
LRU:
Simple

CLOCK:
1. Hand start at X
2. If buffer full check at current hand index
    a) if pin/ref bit = 0 then replace page in frame with new page (pin/ref bit set to 1) and advance hand to next frame 
    b) if pin/ref bit = 1 then set pin/ref bit to 0 and repeat 2. till eviction
---
### Bitmaps
Normal Bit Map
* For every distinct value create a Bitmap (Vector) that indicates where this value is present in the table
Range-Encoded
* Like normal but every bit indicates Value <= X and not only Value = X
* For value v, bit n in bitmap B_v is 1 if tuple(n) ≥ v
Decomposed
* Like normal but for numeric values e.g. the bitmap is for each digit. Numeric ranges like 0-999 in base 10 can be represented with just 30 bitmaps and not 1000

Bitmaps can be combined to query specific tuples.

How many Bitmaps for:
* Base 2 0-9999 | Normal 10000 Bitmaps | Decomposed log2(10000) = 14; 2^14 groß genug lol -> 14 * 2 Bitmaps
* Base 10 0-9999 | Normal 10000 Bitmaps | log10(10000) * 10 = 4 * 10
* Base 16 0-9999 | Normal 10000 Bitmaps | log16(10000) * 16 = 4 * 16

---
### Cost Comparison of JOIN operators
#### NLJ
* Naive := m + m * n (Every Tuple Read ist eine page request)
* Block := M + M * N (Only two frames required)
* Index := M + m * (ceil(log_fanout(n)) + 1)
#### The Rest
* Sort-Merge :=  M + N (Only two frames required)
* Hash-Join := M + N ( Number Frames = N (smaller relations) + 1)

---
### Fragmentation & Allocation **

#### Parallel Join Operators (Network cost)


Symmetric Repartitioning (random initial partition)
|TableA| * (1 - (1 / # nodes)) + ... (repeat für alle tables)

Asymmetric Repartitioning (random initial partition)
|TableA| * (1 - (1 / # nodes))

Replication/Broadcast/Fragment Replication Join: Replicate A
|A| * (# nodes - 1)

Semi-Join Reduction (Table A auf node 1 und B auf node 2; wir wollen Table A reducen und zu Table B schicken)
BytesOfJoinKey * |B| + |A| * Bytes * Selectivity

Semi-Join Reduction (Table A und B round-robin partition; A reducen und replizieren)
|B| * BytesOfJoinKey * (# node - 1) + |A| * Bytes * Selectivity * (# node - 1)


---
### Selectivity Estimation
T() := Anzahl Tuple in Tabelle
V() := Anzahl distinct values
$T(S\Join T)$ ist immer die größe der Tabelle mit dem foreign key

$\text{sel}(R.a = constant) = 1 / V(R, a)$
$\text{sel}(R.a = constant1 ~ OR ~ R.b = constant2) = 1 / V(R, a) + 1 / V(R, b) - 1/ V(R, a) * 1 / V(R, b)$
$\text{sel}(R.a = constant1 ~ AND ~ R.b = constant2) = 1/V(R, a) * 1/V(R, b)$
$\text{sel}(S\Join_{S.c=T.c}T) = T(S\Join T)/T(S\times T)$
$\text{sel}(S\Join_{S.c=T.c}T) = 1/max(V(R,b),V(S,b))$ (nur wenn keine primary/foreign key relation)


---
### Query Optimisation
$\text{Cardinality} = |R_A \Join R_B| = |R_A| \times |R_B| \times sel(R_A \Join R_B)$

Fill out blank spaces in table with cardinallity, cost and join diagram  
selectivity of joins were given

---
### Map Reduce
map := emits (key, value) pair
reduce := consumes results of map with all the same keys

---
### Multiple Granularity Locking
5-Types: S (Shared), X (Exclusive), IS (Intention Shared), IX (Intention Exclusive)

| New ↓ \| Existing → | IS  | IX  | S   | X   |
| ------------------- | --- | --- | --- | --- |
| IS                  | ✓   | ✓   | ✓   | X   |
| IX                  | ✓   | ✓   | X   | X   |
| S                   | ✓   | X   | ✓   | X   |
| X                   | X   | X   | X   | X   |

Workflows:
Update line: Table(IX) -> Page (IX) -> Line (X)
Read line: Table(IS) -> Page (IS) -> Line (S)

---
## Conflict Graph
* Conflict exists if R->W; W->R or W->W of different transactions on same data. R -> R is fine. 
* Only look into the future
* Each node is a transaction number and each vertice is a conflct
* If acyclic (no loop)  a serial executions is possible
	* In a possible execution a Transaction can only be executed when every transaction of the incoming vertices was executed

---
## DB Logging
Steal := Allow to write uncomitted changes to disk
Force := Instantly write comitted cahnges to disk

|          | No Steal          | Steal          |
| -------- | ----------------- | -------------- |
| No Force | Redo + No Undo    | Redo + Undo    |
| Force    | No Redo + No Undo | No Redo + Undo |
Active Transaction Table := Keep track of which transactions where completed 

```
WAL (Write Ahead Log)
001:<CHECKPOINT-BEGIN>
002:<CHECKPOINT-END>
003:<T1, A → P5, 1, 2>
004:<T2, B → P3, 2, 3>
005:<T3, C → P1, 4, 5>
006:<T2, D → P5, 6, 7>
007:<T3 ABORT>
008:<T3 TXN-END>
009:<T1 COMMIT>
010:<T4, E → P1, 6, 7>
```

| TXId   | Status | lastLSN (last line where transaction active) |
| ------ | ------ | -------------------------------------------- |
| T1     | C      | 009                                          |
| T2     | U      | 006                                          |
| ~~T3~~ | ~~U~~  | ~~008~~                                      |
| T4     | U      | 010                                          |

---
## SQL-Star-Query

```
SELECT m.id , m.name , SUM( cf.billedPrice) AS revenue
FROM CinemaFacts cf , MovieDimension m, DateDimension d
WHERE cf.date_id = d.id AND cf.movie_id = m.id
AND d.year = 2017 AND m.genre=”sciencefiction”
GROUP BY cf.movie_id
HAVING revenue >= 2000000
ORDER BY revenue DESC;


SELECT m. genre , COUNT( DISTINCT m. i d )
FROM CinemaFacts c f JOIN MovieDimension m ON c f . movie_id = m. i d
WHERE m. i d NOT IN
(SELECT c f . movie_id
FROM CinemaDimension c JOIN CinemaFacts c f
ON c . i d = c f . cinema_id
WHERE c . c o u n t r y = ” Germany ” )
GROUP BY m. genre ;
```
---
## Snowflake Metadata

| Timestamp:                | 1            |
| ------------------------- | ------------ |
| Added:                    | [1]          |
| Deleted:                  | []           |
| Stats: Column0<br>Column1 | 70-90<br>D-V |
Wenn Daten in page geupdated werden dann werden diese pages gelöscht in in einer neuen zusammengefügt

| Timestamp:                | 5            |
| ------------------------- | ------------ |
| Added:                    | [5]          |
| Deleted:                  | [1,3]        |
| Stats: Column0<br>Column1 | 10-90<br>A-W |

---
## Dynamic Programming
PK-FK Relationships
Input
* Tablesize A + Tablesize B
Output Size
* Bei nomralen join größe table mit FK
* Ansonsten Produkt |A| * |B
Kosten
* Input + Output

1. Join two tables
2. Join three tables
3. Join four tables

---
## Questions
* What are the key characteristics and trade-offs of a shared-nothing DBMS architecture?
	* Core concept: Each node own data, own dbms
	* Local execution (min network latency)
	* No direct data sharing between nodes
	* Simple implementation (each node is independent)
	* Good horizontal scalability
	* - Susceptible to data skew and load imbalance
	* - Node failures can make data inaccessible
	* - Data redistribution needed for load balancing
* What are the key characteristics and trade-offs of a shared-data DBMS architecture?
	* Core concept: Multiple compute servers access shared data storage over network
	* Centralized data storage
	* Compute nodes can access any part of the data
	* Storage and compute layers are separated
	* Better load balancing (any node can process any data)
	* Higher fault tolerance (data remains accessible if compute nodes fail)
	* Flexible resource allocation
	* - Higher latency due to network data access
	* - Network bandwidth can become a bottleneck
	* - More complex coordination required

* What is a Buffer Pool
	* Cache with fixed Framesize
	* And page table that maps pageID to frame location
* What is the advantage of using Multiple Granularity Locking?
	* Allow Locks at different levels (DB, Table, Page, Row)
	* Reduces number of locks for large operations, early conflict detection, increased concurency, decreases lock management overhead

* Why using shared-storage in cloud SDMS instead of using shared-nothing. Explain one disadvantage of shared-nothing and one advantage of using shared-storage.
* Name two features, which are achieved by using metadata in Cloud DBMS (Snowflake-like)
	* Query optimization / pruning
	* Time travel / versioning
* What is the purpose of log shipping?
	* support **recovery after failures**
	* enable **replication and failover**,
* What is the purpose of quorum? Why is it helpful for high-performance?
	* A quorum is a rule that an operation must be confirmed by a sufficient subset of replicas (for example, a majority) before it is accepted. This helps maintain **consistency** and avoid conflicting decisions during failures or partitions.
	* You do **not** need to wait for _all_ replicas. Waiting only for a quorum reduces latency and lets the system continue operating even if some replicas are slow or unavailable. That improves throughput and availability while still preserving correctness.
* Definition of PREF.
	* Predicate-based Reference Partitioning
* What is a database index? Why is it used?
	* A database index is a data structure used for efficient retrieval of data from disk. It’s used to minimize the number of I/O operations.
* What is the difference between a clustered index and an unclustered index?
	* In a clustered index, data are sorted on disk by the same attribute that the index uses.
* What is the difference between a sparse index and a dense index?
	*  sparse index does not contain an entry for each record of the database. In a dense index, we have an entry for each possible record.
* When is it possible to use a sparse index?
	* A sparse index is usually used if the index is clustered, since we know that the underlying data are sorted.
* What are fragmentation and replication and what are their purposes?
	* Fragmentation: Divides a table into smaller fragments. Why needed: Data may be too large to store it on one node; Enable parallel query processing on multiple nodes; Individual partitions can be pruned Replication: Assign a fragment to multiple servers. Why needed: Avoid hot-spots; i.e., if one node needs to do more work than other nodes; Enable fault-tolerance (other servers can take over), Trade-off: better load-balancing vs. higher update cost
* What is the difference between horizontal and vertical fragmentation?
	* Horizontally fragmentation: split table by rows Vertically fragmentation: split table by columns
*  Name common partitioning schemes.
	* Round Robin, Range-partitioning, Hash-partitioning
* What is allocation? Why is finding a good allocation a hard task
	* Allocation: Decide on which server to put each fragment. The challenge is to allocate partitions/fragments that are often accessed together on the same node (co-partitioning). I.e., an optimal allocation depends on the workload.
* Briefly describe IaaS, PaaS and Saas.
	* IaaS: the user is provided with basic compute resources (e.g., virtual machines) and needs to manage multiple aspects of them (Operating System, apps etc.). PaaS: the user is provided with a platform to build and deploy applications. Basic resources are managed by the cloud provider. SaaS: the user is provided with a complete software ready to be used (e.g., Google Drive).
* List and explain the four promises of Cloud Computing.
	* Scalability: illusion of having infinite resources available. Elasticity: resources can be allocated/de-allocated based on the current workload. Fault Tolerance: when a node fails, it can be quickly and seamlessly replaced (high redundancy). Pay-As-You-Go: users pay only for resources that they use. No ”fixed” upfront investment is needed
* What are the advantages of a Shared-Data architecture for Cloud Databases?
	* With a Shared-Data architecture it’s easier to decouple compute and storage layers. Scalability and fault tolerance are simpler to achieve.
* TWO-PHASE LOCKING (2PL)
	* Grow-phase (aqquire locks)
	* shrink phase (unlock)
	* no new locks when in shrink phase
* Why is STEAL + NO-FORCE advantageous for performance?
	* The combination of steal and no-force policies is most efficient during normal database processing. 
	* NO-FORCE creates fewer I/O operations than FORCE because it is not necessary to write all changed pages before commit. This means that many changes to the same page can accumulate before it is written. Writing a WAL for recovery creates less I/O than writing full changed pages
	* STEAL is advantageous over NO-STEAL because NO-STEAL effectively reduces the buffer size with every concur- rently active transaction that changes pages. This can lead to stalls, where no pages can be evicted because all pages are still in use by active transactions. Stalls like this cannot occur if stealing is allowed.
* How can atomicity and durability be guaranteed under STEAL + NO-FORCE?
	* By writing a Write Ahead Log (WAL) and forcing the log, i.e.
	* Forcing all log entries of a transaction to disk before committing.
	* Forcing all log entries of changes to a page to disk before writing that page
* Recall the different physical operators for the JOIN operator. Is the JOIN operator a pipeline breaker? Give an example for a join implementation that is a pipeline breaker and one for an implementation that is not. Explain your answers and reasoning.
	* Pipeline breaker: A Hash-Join is a pipeline-breaker since it needs to build a hashtable on one (usually the smaller) relation and materialized the hashtable. Until the hashtable is built, the Hash-Join blocks the execution. However, after the hashtable has been built the Hash-Join can probe tuples from the other table into the hash table in a pipelined fashion.
	* Non-Pipeline breaker: The Nested Loop Join implementation, for example, is not a pipeline breaker, since it does not block the execution to materialize or buffer an intermediate result. New result tuples are pipelined to the next operator as they are computed
* Briefly explain the following three parallel join strategies:
	* Symmetric repartitioning join: Both tables are re-partitioned (shuffled) on the join-key, such that tuples from each table with the same join-key can be joined locally on each node.
	* Asymmetric repartitioning join: Table A is already partitioned based on the join key, thus we only need to partition B based on the same key.
	* Replication/Broadcast join: Replicate A: Each node will send its own local partition of table A to all other nodes. The join can then be done in parallel on each node, since all nodes have the complete A table.
* What is a data warehouse?
	* A data warehouse is a type of database that is heavily optimized for read-only queries. It integrates data from multiple other databases, leveraging ETL (Extract, Transform, Load) operations. Such integration allows us to answer queries that require a holistic view of the information contained in multiple, distributed sources.
* Name the four basic operations on multi-dimensional data
	* Slice/Dice := Aus Cube slice oder dice-abschnitt bekommen
	* Roll-Up := Eine dimension gröber machen (Städte -> Länder)
	* Drill-Down := Eine dimension feiner machen (Quartale -> Monate)
* What issue can arise when joining the fact table and dimension tables together following a classic database approach? Why can the cross-product plan be a better alternative?
	* The classic database join-strategy has to join the very big fact table first (since it is the only table containing foreign keys to the dimension tables) and will therefore produce very big intermediate results, resulting in an increased query runtime. The cross-product join is a better alternative, since we (theoretically) avoid having large intermediate results by performing the cartesian product between the dimension tables first (which are usually much smaller than the fact table).
* What are the possible issues of a cross-product join? Is there a more efficient technique? If so, describe it.
	* Since a cross-product join plan uses cartesian products of the dimension tables, the intermediate results can, insituations where the selectivity of selections over the dimension table is high, cause very big intermediate results. A better technique is the semi-join plan. This algorithm will first semi-join the dimension tables with the fact table and produce RIDs of the qualifying tuples in the fact table. The fact table is then joined with the intersection/union of the qualifying RIDs from the semi-joins. Thereby, it only selects the tuples in the fact table that are actually included in the join result.
* Bitmap optimization
	* Only (b − 1) different possible digits need to be encoded per digit position, because the last digit can be determined by the negation of all other digits. The issue of this optimization is the increased number of bitmaps that need to be read.
	* If the first digit is not used fully by the value range, some of the bit vectors representing higher digits are not required.
* Define a straggler with your own words.
	* A Straggler is either a map or a reduce task that takes an unusually long time to complete.
* Describe how fault tolerance is achieved in a Hadoop cluster in 1 - 5 sentences.
	* Regarding data: Multiple replicas are stored on different DataNodes (and across different racks). NameNode High Availability (using a pair of NameNodes in active standby) enables fast recovery from NameNode failures. With regard to execution: JobTracker detects failure of TaskTracker node via periodic heartbeats, JobTracker re-assigns tasks to a new node if failure is detected, A TaskTracker can also be blacklisted
* Can you start reducers while a mapper is still running?
	* Simple Solution: No. To sort and group by the input for reducers, we have to wait until all mappers finish. The last mapper could theoretically produce a key that should have been consumed by a running reducer. Complex Solution: The reduce step has 3 phases: shuffle, sort, and reduce. Shuffle is the stage where the reducer collects data from each mapper. This can happen while mappers are generating data. On the other hand, sort and reduce can only start once all mappers have finished. Shuffling starts based on a threshold of the percentage of mappers that have finished. You can change the parameter to get shuffling to start sooner or later.
* Shortly explain the WAIT DIE strategy for deadlock prevention in traditional locking schemes.
	* To prevent deadlocks the transaction that is “younger” will be aborted and the “older” transaction will wait if conflicts occur.
* What is “First-committer-wins” in Multi Version Cincurrency Control
	* This means, that a transaction checks the version chain at commit time, making sure that no other transaction has committed a version that would be in conflict with its own.

| cat | Round-Robin         | Range                 | Hash                                   |
| --- | ------------------- | --------------------- | -------------------------------------- |
| +   | balanced            | pruning by range      | balanced if good hash function is used |
| -   | no pruning possible | might not be balanced | pruning only by hash key posible       |
