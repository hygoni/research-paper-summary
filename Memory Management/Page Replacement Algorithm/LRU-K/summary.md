# The LRU-K page replacement algorithm for database disk buffering

This is summary of [The LRU-K page replacement algorithm for database disk buffering, Elizabeth J. O'Neil, 1992](https://dl.acm.org/doi/10.1145/170036.170081). This paper tries to distinguish between frequent and infrequent buffers when searching for replacement victim buffers.

Note that this is just a summary. proofs and measurements are in the paper!  

# Buffer (Page) Replacement Problem

When program accesses its secondary memory, Operating Systems manages its copy in main memory. that's because access latency of secondary memory; it is usally much slower than main memory. when there are infinite main memory, there is no problem. the problem arises when memory lacks: "Which buffer should be dropped to make new buffer?"   

It may not be Operating Systems that manage buffers. Some applications bypass Operating Systems and manages their own buffers. Anyway, buffer replacement algorithm is important when a workload is I/O intensive; poor algorithm will harm its performance badly.

# Classical LRU

The classical LRU, which is equal to LRU-1, just drops the Least Recently Used buffer. to implement this, we need to record last access time for every buffer. Its overhead is quite small.  

But the classical LRU has a problem. What if Least Recently Used buffer is accessed more frequently, than most recently used buffer?  

The example in this paper is a database. There are two types of buffers. first type is buffer that contains B-tree nodes (access probability is .005), and second type is buffer that contains its data (access probability is .00005).  

Even if B-tree node buffers are more frequently used, classical LRU has no idea of frequency. it just drops a buffer that is least recently used, even if it is most frequently used.  

# LRU-K Algorithm

So how LRU-K algorithm solves this problem? To distinguish between frequently and infrequently used buffers, this algorithm remembers last K accessed time of every buffer. access times are not hold forever. How long are access times kept? that is **Retained Information Period.**  

# Backward-K distance

Backward-K distance is last Kth access time of a buffer. if a buffer is not accessed at least K times, it has infinite distance. The LRU-K algorithm chooses a buffer that has maximum backward-K distance for replacement victim.

That means the LRU-K algorithm drops one of buffers that are not accessed at least K times, or if all of buffers are at least accessed K times, the buffer that has smallest Kth access time.  

Note that access times are just forgotten after Retained Information Period!  

# Correlated Reference Period

But we need hold buffers for short period, even if they are not accessed K times. That's because a file is accessed more than once (In database example, it reads, calculates, writes data so it is accessed multiple times in a query). That "short period" is called **Correlated Reference Period**.

# Why LRU is better than LFU

There is another approach on this problem, called LFU (Least Frequently Used) algorithm, which drops most infrequently used buffer for replacement. But one limitation of LFU is that it does not "forget" old accesses. So it does not fit well when access patterns change. As LRU-K just forgets old accesses, it can adapt itself to evolving access patterns. But when K is high, it becomes similar to LFU.  

# Conclusion

LRU-K is better than classical LRU because it can discriminate between frequently / infrequently used buffers, and adapts itself to evolving patterns unlike LFU.
