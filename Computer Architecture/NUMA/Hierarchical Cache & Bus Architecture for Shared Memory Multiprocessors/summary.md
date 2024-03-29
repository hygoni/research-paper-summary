## Hierarchical Cache & Bus Architecture for Shared Memory Multiprocessors

This is summary of [Hierarchical Cache & Bus Architecture for Shared Memory Multiprocessors", Andrew W. Wilson Jr, 1987](https://dl.acm.org/doi/10.1145/30350.30378). I think this paper is first attempt to introduce multi-level caches and hierarchical bus architecture, what we call NUMA (Non-Uniform Memory Access) nowdays.    

This text is a summary; Details are in the paper!

## What is the problem this paper solves?

![Von Neumann Architecture, wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Von_Neumann_Architecture.svg/1920px-Von_Neumann_Architecture.svg.png)  
In the Von Neumann architecture, memory becomes a bottleneck because memory is much slower than CPU. Even in modern computers, access latency of CPU registers is 100x faster than its main memory (DRAM). By introducing cache memory between CPU and main memory, the memory traffic can be reduced.  

But this papers says a single central cache controller is not enough; It proposes hierarchical architecture in cache and memory. Both hierarchical cache and bus architectures reduces much of global bus traffic, allowing the computer to have more than 128 processors.

## Hierarchical Cache Architecture

![Hierarchical Cache Architecture, wikipedia](https://upload.wikimedia.org/wikipedia/commons/e/e8/Shared_private.png)

The simple way to reduce bus traffic is introducing hierarchical cache architecture. As lower level caches can be slower and cheaper, it does not increase price seriously but reduces bus traffic. But to see good performance gain lower level caches should be much larger than higher level cacaches.

p.s.  
note that in the paper, "higher level" caches are faster and more expensive, "lower level" caches are slower and cheaper.  

## Hierarchical Bus Architecture

![images/NUMA.png](images/NUMA.png)

Distributing memory and buses using hierarchical architecture greatly reduces traffic of global bus. as bus traffic is distributed to many local buses, this architecture is scalable with number of processors. Nowdays, this architecture is NUMA (Non-Uniform Memory Access) and broadly used in high performance computers.  

One consideration in this architecture is memory allocation algorithm and policy. [This paper is nice introduction to NUMA](https://queue.acm.org/detail.cfm?id=2513149)

## Conclusion

- By introducing hierarchical cache architecture, its cache coherency algorithms can be used in multiple cluster architecture.
- In the simulation results, even in larger systems the multicache coherency algorithm's cost is quite small.
- Hierarchical cache reduces global bus traffic and decreases access latency.
- If cache miss and remote cluster (remote node) accesses are so high, it can be a problem in large systems.

## Further Readings

### Computer Interconnection Structures: Taxonomy, Characteristics, and Examples

In higher level view, NUMA is one of ways to connect computers (processors). There are other ways. [This paper](/Computer%20Architecture/Computer%20Interconnection/Computer%20Interconnection%20Structures:%20Taxonomy%2C%20Characteristics%2C%20and%20Examples/summary.md) is a nice taxonomy for ways to connect computers.  

### I haven't read yet but...

As accessing from remote cluster slows down access to memory and requires overhead to synchronize between clusters, There will be papers that introduces NUMA-aware memory allocation policies/algorithms.  
