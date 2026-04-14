---
aliases:
  - SDMS
tags:
  - fb20
  - master
  - pflichtmodul
  - semester-1
  - 6CP
  - klausur
  - master-informatik
  - status-in-bearbeitung
description: ""
---
## Überblick

## Kerninhalte

## Zusammenfassung

## Prüfungsvorbereitung

## Altklausuren


Backlog:

Übung 6 wiederholen
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
