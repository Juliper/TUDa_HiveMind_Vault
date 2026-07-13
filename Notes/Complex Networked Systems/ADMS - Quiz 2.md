---
title: ADMS - Quiz 2
aliases:
  - ADMS Quiz 2
tags:
  - adms
  - quiz
  - fb20
description: Collection of all quiz questions for ADMS Quiz 2 preparation (Parallelism, FPGAs/TPUs, GPUs, TEEs)
draft: false
---
# ADMS - Quiz 2

> [!info] Note
> The actual quiz is **25 points** and lasts **15 minutes**.

---

# A - Parallel Execution & Scheduling

## Task 1 - True/False

> [!question]- 1.1 Inter-query parallelism runs a single query on multiple cores to reduce its response time and is therefore most important for OLAP.
>
> **False** - That describes *intra*-query parallelism. Inter-query runs *multiple* queries in parallel to increase throughput (OLTP).

> [!question]- 1.2 A multi-threaded architecture has the advantage that all threads share the same memory address space and cause less overhead per context switch than separate processes.
>
> **True** - Shared address space + cheaper context switches are the core advantages of multi-threading.

> [!question]- 1.3 A disadvantage of the multi-threaded model is that a single crashing thread can bring down the whole DBMS process.
>
> **True** - Because threads share one process, one crashing thread can crash the whole DBMS.

> [!question]- 1.4 In the **push** model, workers independently pull tasks from a queue whenever they become idle.
>
> **False** - Push = a centralized *dispatcher* assigns tasks to workers. Pulling from a queue is the *pull* model.

> [!question]- 1.5 Pinning one worker thread per physical core (e.g. via `pthread_setaffinity_np`) is one valid worker-allocation strategy.
>
> **True** - "One worker per core" pins each thread to a core (`sched_setaffinity` / `pthread_setaffinity_np`).

> [!question]- 1.6 Assigning multiple worker threads per core leverages hyper-threading and can improve utilization, but adds overhead.
>
> **True** - Multiple workers per core = hyper-threading; better utilization but higher overhead.

---

## Task 2 - Short Answers

> [!question]- 2.1 - Inter vs. Intra: Distinguish **inter-query** and **intra-query** parallelism regarding their **goal** and the workload (OLTP/OLAP) they matter for.
>
> - **Inter-query**: run multiple queries in parallel -> goal: increase **throughput** -> important for **OLTP**.
> - **Intra-query**: run a single query in parallel (intra-operator + inter-operator) -> goal: decrease **response time** -> important for **OLAP**.

> [!question]- 2.2 - Push vs. Pull: Describe the **push** and **pull** task-assignment (scheduling) approaches. Which one is better suited for **very small tasks** and why?
>
> - **Push**: a centralized dispatcher assigns tasks to workers and monitors progress (global control).
> - **Pull**: workers pull tasks from a queue (filled by the dispatcher), process, then fetch the next (decentralized).
> - For **very small tasks**, **pull** is better: a central dispatcher would become a bottleneck, whereas workers self-serve from the queue with less coordination overhead.

> [!question]- 2.3 - Worker Allocation: Name the **two** worker-allocation strategies and give one trade-off for each.
>
> 1. **One worker per core**: each physical core gets one pinned thread (`pthread_setaffinity_np`) -> good locality, no oversubscription, but cannot hide stalls.
> 2. **Multiple workers per core**: several threads per core -> leverages hyper-threading + better utilization, but higher scheduling/context-switch overhead.

> [!question]- 2.4 - Roofline Model: What are the **IO-bandwidth roof** and the **computational roof**, and where do typical DBMS queries fall?
>
> The roofline model plots **attainable performance** against **computational intensity** (FLOPs/byte).
> - **IO-bandwidth roof** (memory-bound region): for low computational intensity, performance is limited by memory/IO **bandwidth**. Typical DBMS queries live here -> they benefit strongly from fast and large RAM/cache.
> - **Computational roof** (compute-bound region): for high computational intensity, performance is limited by the raw **compute power** (FLOPs ceiling).

> [!question]- 2.5 - Synchronization Primitives: What are **thread barriers**, **mutexes** and **semaphores**?
>
> - **Mutex**: a mutual-exclusion lock -> only one thread may be in the critical section at a time.
> - **Semaphore**: a counter controlling access to N resources (signaling) -> can admit up to N threads.
> - **Barrier**: a synchronization point where **all** threads must arrive before any of them may proceed.

> [!question]- 2.6 - CSP / Message Passing: What is **CSP / message-passing / async programming**, and how do processes communicate?
>
> An alternative to shared-memory synchronization (barriers/mutexes/semaphores): processes do **not** share memory but communicate by passing messages over **channels**, letting each worker work on its own data.
> - **Blocking channel**: sender blocks until the receiver is ready, receiver blocks until the sender's data arrives.
> - **Non-blocking channel**: a buffer/mailbox/FIFO decouples them -> the sender is **not** blocked (but the buffer needs space).
> Leading example: **Golang**.

> [!question]- 2.7 - Costs of Parallelism: Parallelism does not come for free - name its main costs.
>
> - Overhead for **synchronizing** work.
> - Extra **power** consumption.
> - Higher **programming effort**.
> - More (nasty) **bugs**.
> -> Parallelism is **not always** useful; only parallelize where the overhead pays off.

> [!question]- 2.8 - Scheduler Decisions: Which questions must the scheduler answer when parallelizing a query?
>
> - **How many tasks** to use, i.e. how to split the query plan into tasks.
> - **Which CPU cores** the tasks execute on (multi-core and NUMA!).
> - **Which memory region** a task should store its output to.

---

# B - Memory Models, NUMA & Data Placement

## Task 1 - True/False

> [!question]- 1.1 In a NUMA system, every CPU accesses all memory regions with the same latency.
>
> **False** - NUMA = *Non-Uniform* Memory Access: local memory is faster than remote memory (reached via the interconnect).

> [!question]- 1.2 When a DBMS calls `malloc`, physical memory is allocated immediately, before the memory is ever touched.
>
> **False** - `malloc` only extends the virtual data segment; physical memory is allocated by the OS **on page fault**.

> [!question]- 1.3 With **first-touch** allocation, a page is physically placed at the CPU of the thread whose access caused the page fault.
>
> **True** - Definition of first-touch allocation.

> [!question]- 1.4 Coarse-grained partitioning gives better load-balancing, while fine-grained partitioning gives lower scheduling overhead.
>
> **False** - Swapped: **fine**-grained = better load-balancing; **coarse**-grained = lower scheduling overhead.

> [!question]- 1.5 Storing only NUMA-local partitions together with thread pinning scales better than random partition placement for a sequential scan.
>
> **True** - Local partition + `numa_alloc` + thread pinning scales near-linearly; random placement flattens out (remote accesses dominate).

---

## Task 2 - Short Answers

> [!question]- 2.1 - Partitioning vs. Placement: Explain the difference between a **partitioning scheme** and a **placement scheme**, and name the three partitioning policies from the lecture.
>
> - **Partitioning scheme**: splits tables based on a policy -> **round-robin/random**, **range-partitioning**, **hash-partitioning**.
> - **Placement scheme**: decides *where* (which socket/NUMA node) the created partitions are physically stored.

> [!question]- 2.2 - NUMA Allocation: After a page fault in a NUMA system, name the **two** main OS strategies for choosing where to place physical memory.
>
> 1. **Interleaving**: distribute allocated memory uniformly across all CPUs/nodes.
> 2. **First-touch**: allocate at the CPU of the thread that first touched (page-faulted) the memory location.

---

# C - Parallel Join Algorithms

## Task 1 - True/False

> [!question]- 1.1 In a partition-based hash join, the hash table is built on the tuples of the **larger** relation and probed with the smaller one.
>
> **False** - The hash table is built on the **smaller** relation R and probed with the larger relation S.

> [!question]- 1.2 With **shared** partitions, all threads write into one global set of partitions and must use latches to synchronize.
>
> **True** - Single global partition set -> latches needed to synchronize concurrent writers.

> [!question]- 1.3 Multi-pass (radix) partitioning is used because the number of partitions per pass is limited by the number of **TLB entries**.
>
> **True** - Fan-out per pass is limited by #TLB entries (T≈64-128); radix uses `i = log_T p` passes.

> [!question]- 1.4 A Bloom filter can produce false negatives, i.e. it may claim a key is absent even though it is present.
>
> **False** - Bloom filters have **false positives**, never false negatives.

> [!question]- 1.5 In the build phase, threads can insert lock-free into a hash-bucket linked list using a `compare_and_swap` (`compare_exchange_weak`) busy loop.
>
> **True** - Since the number of tuples is known, threads insert in parallel using `compare_exchange_weak` instead of locking.

> [!question]- 1.6 In a sort-merge join, both input relations must be scanned multiple times during the merge phase.
>
> **False** - After sorting, the (outer) relation only needs to be scanned **once** during the merge.

---

## Task 2 - Short Answers

> [!question]- 2.1 - Three Phases: Name and describe the **three phases** of a partition-based (parallel) hash join.
>
> 1. **Parallel Partitioning**: divide tuples of R and S into partitions via a hash on the join key; each thread takes a NUMA-local chunk (morsel).
> 2. **Parallel Build**: scan partitions of R, build one hash table on the join key per partition.
> 3. **Parallel Probe**: for each tuple of S, look up its join key in the hash table of the matching R partition; on a match, output the combined tuple.

> [!question]- 2.2 - Shared vs. Private Partitions: Compare **shared** and **private** partitions for the partitioning phase.
>
> - **Shared partitions**: a single global set of partitions all threads write to -> requires **latches** to synchronize.
> - **Private partitions**: each thread has its own set of partitions (no synchronization during writing) -> must be **combined** after all threads finish.

> [!question]- 2.3 - Why not std/boost hash tables?: Why are general-purpose hash tables (std/boost) not ideal for database joins? Name reasons and how a DB hash table optimizes the **probe**.
>
> Reasons they are unsuitable: high overhead for parallel execution, many **non-matching** probe rows (no join partner), and **skewed** distributions cause collisions.
> DB joins split into **build (write-only)** and **probe (read-only)** phases -> no mixed insert/lookup, so no locking during probing. The probe is optimized by using the **lower hash bits as a Bloom filter** (directory) to skip traversing the tuple list when the key is definitely absent.

> [!question]- 2.4 - M-WAY vs. MPSM: Distinguish the two parallel sort-merge join variants **M-WAY** and **MPSM**. What is the key benefit of MPSM?
>
> - **M-WAY (Multi-Way Sort-Merge)**: sort **both** inputs globally (local partition + local sort + global multi-way merge), then parallel merge-join.
> - **MPSM (Massively Parallel Sort-Merge)**: partition one input; sort one input globally and the other only per-partition (locally); join each locally sorted partition against the globally sorted input.
> - **Key benefit of MPSM**: it **avoids the global merge phase for one input**, which is usually the scalability bottleneck of a parallel sort-merge join.

> [!question]- 2.5 - TLB: What is the **TLB** and why does it limit the partitioning fan-out?
>
> The **Translation Lookaside Buffer** is a cache for **virtual-to-physical address translation** (addresses point to 4 KB memory pages). If a translation is in the TLB, it is fast; a TLB miss is expensive. The TLB is hierarchical (L1 TLB ≈ 64-128 entries, shared TLB up to ~thousands). Because each partition being written needs its own page translation, the partitioning **fan-out per pass is limited by the number of TLB entries** (T ≈ 64-128) - beyond that, TLB misses dominate.

> [!question]- 2.6 - Single-pass vs. Multi-pass Partitioning: Distinguish single-pass and multi-pass (radix) partitioning.
>
> - **Single-pass**: partition the input to the desired fan-out `p` in one pass. Problem: `p` can be large -> exceeds the TLB entries -> many TLB misses.
> - **Multi-pass (radix hash join)**: use several passes with a smaller fan-out per pass (limited by T TLB entries), needing `i = log_T p` passes. The better TLB efficiency compensates for the extra read/write passes.

> [!question]- 2.7 - Sort-Merge Phases: Which two phases make up a sort-merge join?
>
> 1. **Sort**: sort the tuples of R and S based on the join key.
> 2. **Merge**: scan the sorted relations and compare tuples; the outer relation R only needs to be **scanned once**.

---

# D - Accelerators: FPGAs & TPUs

## Task 1 - True/False

> [!question]- 1.1 In a modern CPU, most of the die area is spent on cache and control, while compute (ALUs) is only a fraction.
>
> **True** - CPUs are general-purpose: cache + control dominate, compute is a small fraction.

> [!question]- 1.2 On the hardware-specialization spectrum, moving from CPUs towards dedicated hardware (ASICs) trades flexibility for energy efficiency.
>
> **True** - Left = more flexible (CPUs), right = more efficient (dedicated HW), up to 10x-100x energy efficiency.

> [!question]- 1.3 A superscalar CPU can issue multiple instructions in a single clock cycle; hyper-threading builds on this technique.
>
> **True** - Superscalar = multiple instructions per cycle; hyper-threading relies on it.

> [!question]- 1.4 A TPU spends a much larger fraction of its die on control logic than a CPU does.
>
> **False** - Opposite: TPU control is only ~2% of the die (compute ~30%); CPU control is much larger and harder to design.

> [!question]- 1.5 FPGAs typically run at much higher clock frequencies (3-5 GHz) than CPUs, which is why they are so efficient.
>
> **False** - FPGAs run at *low* clock (200-300 MHz) vs. CPUs (3-5 GHz); efficiency comes from custom parallel dataflow, requiring parallelism.

> [!question]- 1.6 In the Parquet parser, null values are not stored in Parquet but occupy physical space in the Arrow representation.
>
> **True** - Parquet does not encode nulls; converting to Arrow decodes RLE validity bits and pads the data so nulls occupy physical space.

---

## Task 2 - Short Answers

> [!question]- 2.1 - When to specialize?: According to the lecture (Google TPU story), when does building specialized hardware make sense?
>
> Specialization makes sense when it **significantly improves a significant portion** of the computation. (Google's example: voice-search DNNs would have required doubling datacenters on CPUs, motivating a custom ASIC for inference with a 10x cost-performance goal over GPUs.)

> [!question]- 2.2 - Systolic Arrays: What is a **systolic array** and why is it well-suited for TPU-style workloads?
>
> A systolic array is a homogeneous, specialized architecture with a tensor as the basis of computation and **data-driven control** (data flows through a grid of processing elements producing partial sums). It offers **better scalability**, **more efficient use of resources**, and **higher performance per Watt** than general-purpose Von Neumann architectures. It is used e.g. in the TPU's Matrix Multiply Unit.

> [!question]- 2.3 - FPGA vs. CPU Pipeline: Contrast a **CPU** and an **FPGA** with respect to their pipeline/dataflow. Name one trade-off of FPGAs.
>
> - **CPU**: fixed pipeline, dataflow determined by instructions; custom logic must be composed from a set of fixed functions.
> - **FPGA**: custom pipeline, dataflow tailored to the application; custom logic implemented directly (free choice of architecture, fine-grained pipelining, distributed memory).
> - **Trade-off**: all "code" occupies physical chip space, and FPGAs run at a low clock frequency, so **parallelism is required** for good performance.

> [!question]- 2.4 - FPGA Toolflow: List the steps to program an FPGA from an algorithm to a running design.
>
> 1. **Code**: hardware-definition languages or high-level languages.
> 2. **Synthesis**: produce a logic-gate-level representation (target-independent).
> 3. **Place & Route**: map the circuit onto a *specific* FPGA's resources.
> *(ASIC flow is similar, but the circuit is mapped onto silicon instead of FPGA resources.)*

> [!question]- 2.5 - Parquet Parser Architecture: How does the FPGA Parquet parser exploit parallelism, and why is an FPGA a better fit than a GPU for this task?
>
> - **Column-Chunk-level parallelism**: multiple Compute Units (CUs) process different column chunks in parallel.
> - **Page-level parallelism**: a pipeline (Fetch -> Frontend -> Decompress -> RLE -> Decoder -> Writeback), each stage a streaming HLS kernel.
> - **FPGA over GPU**: Parquet parsing has an "iterative" memory-access pattern, potentially complex control flow, and encoding complexity - a poor fit for GPUs. An FPGA offers a custom hardware architecture matching exactly the required computation. Result: throughput comparable/better than CPU and superior energy efficiency (up to ~3.4x).

> [!question]- 2.6 - Data/Compute Gap: What is the **Data/Compute Gap** and what two responses does it motivate?
>
> Data volume grows exponentially (exabytes), while single-core CPU performance (frequency) has **stagnated** (roughly since ~2005) - the number of logical cores rises only slowly. This opens a growing gap between the data to process and the available compute. Two responses:
> - **More parallel compute** (distribution, many-cores).
> - **More efficient compute** (specialization -> GPUs, TPUs, FPGAs, ASICs).

> [!question]- 2.7 - Subscalar vs. Superscalar: What is a **subscalar** and what is a **superscalar** CPU?
>
> - **Subscalar CPU**: executes **one instruction at a time** (no implicit parallelism), needing several cycles to complete even a few instructions.
> - **Superscalar CPU**: **issues multiple instructions per clock cycle** (instruction-level parallelism). Modern hyper-threading builds on this technique.

> [!question]- 2.8 - TPU Programming Workflow: How is a TPU programmed?
>
> A TPU is programmed through the **TensorFlow** library; the whole management stack (StreamExecutor API, user-space driver, kernel driver) is **hidden from the user**. Key point: specialized hardware does not exist in a vacuum - it must be **integrated with the rest of the software stack** (the Achilles heel of many research projects).

> [!question]- 2.9 - Parquet vs. Arrow: Contrast the **Parquet** and **Arrow** formats.
>
> Both are **columnar**.
> - **Parquet** = **storage** format, focuses on **compression** (pages are compressed, organized as column chunks, small footprint; **nulls are not encoded**).
> - **Arrow** = **in-memory** format, focuses on **access speed** (O(1) access within chunked arrays; **nulls occupy physical space** / are materialized as zeros).
> Converting Parquet -> Arrow requires decoding the RLE-encoded validity values and **padding** the data so nulls take physical space (plus decompression + decoding).

---

# E - GPU Acceleration

## Task 1 - True/False

> [!question]- 1.1 All threads within a CUDA **warp** (32 threads) execute the same instruction, similar to SIMD.
>
> **True** - A warp = 32 threads all executing the same instruction (SIMD-like).

> [!question]- 1.2 A GPU has fewer but heavier-weight threads than a CPU and each thread typically runs different code.
>
> **False** - GPUs have **many lightweight** threads scheduled in warps running the **same** code; CPUs have few heavyweight threads.

> [!question]- 1.3 A **warp** must be declared explicitly by the programmer in the kernel launch configuration.
>
> **False** - A warp is the smallest *physically scheduled* unit (always 32 threads); it is **not** explicitly declared.

> [!question]- 1.4 There is no guarantee that one CUDA block finishes before another; synchronization between blocks is achieved via separate kernel calls.
>
> **True** - No global ordering inside a kernel; inter-block sync = separate kernels.

> [!question]- 1.5 GPU HBM bandwidth (few TB/s) is much higher than the PCIe bandwidth to CPU memory (~tens of GB/s).
>
> **True** - HBM ≈ TB/s vs. PCIe ≈ 16-60 GB/s -> the PCIe bus is the bottleneck.

> [!question]- 1.6 With GPU-Direct Storage (GDS), data is copied directly from the SSD into GPU memory without going through CPU memory, though the CPU still initiates the I/O.
>
> **True** - GDS bypasses CPU memory (SSD -> GPU directly), but the CPU still executes a kernel to initiate/move data.

---

## Task 2 - Short Answers

> [!question]- 2.1 - Grid / Block / Warp: Define **Grid**, **Block** and **Warp** in the CUDA execution model.
>
> - **Grid**: the bulk of all threads launched on a device by a kernel.
> - **Block**: a group of threads executed together on **one SM** (e.g. 512 threads); ideally #blocks × #threads/block ≥ problem size.
> - **Warp**: the smallest physically scheduled unit of threads, always **32 threads**, not explicitly declared; all threads in a warp run the same instruction.

> [!question]- 2.2 - Parallel Selection: Describe how a **selection/filter** (`SELECT * FROM R WHERE p`) is parallelized on a GPU using prefix-sums.
>
> 1. **Flag array**: each thread evaluates the predicate on its element, writing `flags[i] = 1` if it qualifies, else `0`.
> 2. **Prefix sum**: compute the (exclusive) prefix sum `ps` over `flags` -> gives each qualifying element its **write position**.
> 3. **Scatter**: threads write `val[i]` to position `ps[i]` in the result array.
> This precomputes write locations so threads can write without conflicts.

> [!question]- 2.3 - Reduction vs. Prefix-Sum: What is a **binary reduction tree**, and why is a prefix-sum "more than a reduction"?
>
> - A **binary reduction tree** reduces `n` elements to a single value in `log(n)` steps; one thread per two elements, and after every step half of the threads go inactive.
> - A **prefix-sum** needs two phases: a **sweep-up** phase (the reduction tree computing partial sums) *plus* a **sweep-down** phase that pushes the partial sums back down to compute the final per-element prefix sums.

> [!question]- 2.4 - Overlapping Transfer & Compute: Why does naive batch execution on a GPU suffer, and how is it mitigated with CUDA streams?
>
> DB operations are not compute-intensive, so **data transfer (CPU->GPU) dominates** runtime. Mitigation: **overlap transfer and execution**. CUDA supports asynchronous memory copies, but multiple **CUDA streams** are needed - within one stream all kernels run sequentially, but across streams the GPU can overlap a copy in one stream with compute in another.

> [!question]- 2.5 - GOLAP Compressed Scan: Explain the idea of the **compressed GPU table scan** in GOLAP and why the GPU (not the CPU) enables it.
>
> Column chunks are stored **heavy-weight compressed** on SSD once. At query time, the (smaller) compressed chunks are loaded directly into GPU memory (GPU-Direct Storage), then **decompressed and materialized on the GPU**, overlapping I/O and decompression. The **CPU lacks the compute** to decompress at the optimal bandwidth (= SSD BW × compression ratio); the GPU's massive parallelism can decompress *and* execute the query at that bandwidth, pushing effective bandwidth past the raw flash read bandwidth. Key steps: opportunistic pruning, direct I/O, on-the-fly decompression, GPU-CPU co-execution.

> [!question]- 2.6 - Where to Store the Data? GPU memory is small - where can the data (tables + intermediates) live?
>
> - **Alternative 1 - CPU RAM (host memory)**: store all data in CPU RAM and copy to the GPU as needed (via run-to-finish or batch processing). **Problem**: the PCIe bus (~tens of GB/s) is the bottleneck vs. HBM (~TB/s).
> - **Alternative 2 - SSDs**: store all data on SSDs and copy to the GPU as needed - via the naive path (SSD -> CPU -> GPU) or, better, **GPU-Direct Storage** (SSD -> GPU directly).

> [!question]- 2.7 - Query Execution Models: Distinguish the **run-to-finish** and **batch-processing** GPU query execution models.
>
> - **Run-to-finish**: copy the complete input to the GPU from CPU memory, execute all kernels, then copy the output back. Still limited by the GPU's global memory, but it helps run multiple queries and does not require the whole DB in GPU memory.
> - **Batch processing**: execute the kernel on blocks/batches of data. **Problem**: what if intermediates (e.g. hash tables) don't fit? **Alternatives**: Nvidia unified memory (seamless shared memory between CPU & GPU) or paging data in/out (= a buffer manager on the GPU).

---

# F - Secure Cloud DBMSs (TEE / Intel SGX)


## Task 1 - True/False

> [!question]- 1.1 A Trusted Execution Environment protects an application even from privileged code such as the OS or hypervisor.
>
> **True** - The whole point of a TEE: isolate the app from untrusted privileged code.

> [!question]- 1.2 In an Intel SGX enclave, code can directly perform system calls, DMA, storage and network access.
>
> **False** - Enclaves have **no direct** access to HW DMA, syscalls, storage or network; access is via *enclave transitions* / OCalls.

> [!question]- 1.3 Enclave memory (the EPC) is transparently encrypted in RAM and only decrypted inside the CPU cache.
>
> **True** - EPC pages are encrypted in RAM (confidentiality + integrity), decrypted only in the CPU cache.

> [!question]- 1.4 Intel SGX has the **largest** Trusted Compute Base (TCB) among Nitro Enclaves, Confidential VMs and SGX.
>
> **False** - SGX has the **smallest** TCB (only CPU + app); Nitro/CVMs include more (guest OS etc.).

> [!question]- 1.5 An enclave exit/transition (context switch) is far cheaper than a regular system call on Intel CPUs.
>
> **False** - An enclave exit + re-enter costs ~7,000-14,000 cycles vs. ~250 cycles for a regular syscall.

> [!question]- 1.6 In SGXv2, the EPC capacity was increased dramatically (up to 512 GB per socket) compared to the ~128 MB of SGXv1.
>
> **True** - SGXv2: EPC up to 512 GB (×4000), multi-socket up to 1 TB total.

---

## Task 2 - Short Answers

> [!question]- 2.1 - What can go wrong in the cloud? Also name the attack surfaces.
>
> When operations are outsourced to the cloud, the **provider is untrusted**. The attack surface is huge: the **App**, **OS** and **Hypervisor** (millions of lines of privileged code) can all be attacked. Two things can go wrong:
> 1. **Confidentiality**: data breaches (secrets are read).
> 2. **Data Integrity**: data manipulation (values are tampered with).

> [!question]- 2.2 - What is Intel SGX? Give the process-level and system-level view.
>
> **SGX = Software Guard eXtensions** - an instruction-set extension of the Intel CPU.
> - **Process level**: allows processes to create **enclaves**; an enclave ≈ a **secure shared library** in an isolated memory region. It has **no direct access** to HW DMA, system calls, storage or network; access happens via **Enclave Transitions**, communication via shared memory.
> - **System level**: an **isolated and encrypted RAM region**; the **EPC (Enclave Page Cache)** is limited in size and therefore needs **swapping** (with a context switch + integrity check on each swap).

> [!question]- 2.3 - TEE Properties: Name and briefly describe the **three** properties of a Trusted Execution Environment.
>
> 1. **Isolation**: code and data are isolated from (untrusted) software outside the enclave.
> 2. **Confidentiality**: enclave memory is transparently encrypted.
> 3. **Attestation**: the code and data inside the enclave can be authenticated.

> [!question]- 2.4 - Secure Application Flow: Describe the four steps to build a secure TEE application (attestation-based key provisioning).
>
> 1. **Attestation**: the enclave contacts a Key Management Service (KMS) over an encrypted (TLS) channel and attests itself.
> 2. **Check**: the KMS verifies the attestation - is it a real enclave? does it have the expected hash?
> 3. **Key deployment**: if successful, the KMS sends the data key.
> 4. **Work**: the enclave uses the key to decrypt inputs and encrypt outputs.

> [!question]- 2.5 - Enclave Transitions: Contrast **Normal Mode** and **Enclave Mode** regarding access to enclave data and OS services.
>
> | | Normal Mode | Enclave Mode |
> |--|-------------|--------------|
> | Enclave data | **No** access | **Access** |
> | OS services | **Access** | **No** access |
> | Non-enclave data | Access | Access |
>
> Switching between the modes uses special CPU instructions ("Enclave Transition").

> [!question]- 2.6 - Performance Factors: List the four main performance factors of Intel SGX for databases.
>
> 1. **Enclave creation time** (correlated with enclave memory size, ~3 s for 1 GB; amortizes over runtime).
> 2. **Enclave transitions** (context switches, ~7,000-14,000 cycles).
> 3. **Memory access overheads** (LLC misses, EPC paging ~40,000 cycles page-in/out, TLB misses).
> 4. **Side-channel mitigation overheads** (e.g. data-dependent write positions up to 5x slower).

> [!question]- 2.7 - What did SGXv2 add? Name the main improvements over SGXv1.
>
> - **Bigger enclaves**: EPC increased from ~128 MB (v1) to **up to 512 GB** per socket (×4000).
> - **Multi-socket support**: up to **1 TB** total EPC capacity across sockets.
> This removes SGXv1's severe paging bottleneck at larger data sizes (though remote-NUMA and paging effects are still visible).

> [!question]- 2.8 - SGXv2 Root Causes & Fix: In SGXv2, hash-based joins still slow down significantly. Name the **two root causes** and the fix used to restore DB performance.
>
> - **Root cause 1 - Random main-memory access**: random reads/writes to large arrays are up to ~3x slower than without SGX.
> - **Root cause 2 - Side-channel mitigation**: read-dependent write positions + microcode mitigation against Spectre v4.
> - **Fix**: manual **loop unrolling + instruction reordering** restores most of the throughput.

> [!question]- 2.9 - SGX Usage Models: Distinguish the **two** usage models for running a DBMS in Intel SGX.
>
> 1. **Enclave-native DBMS**: the DBMS is written for the enclave and calls the host application via ECalls/OCalls.
> 2. **Enclave DBMS using Gramine (LibOS)**: an unmodified DBMS runs on a Library OS inside the enclave (syscalls handled by the LibOS via a platform adaptation layer). Measured overhead for a full DBMS (Hyrise, TPC-H): ~-33% throughput from side-channel mitigation and ~-15% from SGX + Gramine.
