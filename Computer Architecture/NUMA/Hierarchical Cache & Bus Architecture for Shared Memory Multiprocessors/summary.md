## Hierarchical Cache & Bus Architecture for Shared Memory Multiprocessors

This is summary of [Hierarchical Cache & Bus Architecture for Shared Memory Multiprocessors", Andrew W. Wilson Jr, 1987](https://dl.acm.org/doi/10.1145/30350.30378)

## What is the problem this paper solves?

![Von Neumann Architecture, wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Von_Neumann_Architecture.svg/1920px-Von_Neumann_Architecture.svg.png)  
In the Von Neumann architecture, memory becomes a bottleneck because memory is much slower than CPU. Even in modern computers, access latency of CPU registers is faster than its main memory (DRAM) 100 times. By introducing cache memory between CPU and main memory, the memory traffic can be reduced.  

But this papers says a single central cache controller is not enough; It proposes hierarchical architecture in cache and memory.
