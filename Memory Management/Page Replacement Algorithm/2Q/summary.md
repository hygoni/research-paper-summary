# 2Q: A Low Overhead High Performance Buffer Management Replacement Algorithm

This is summary of [2Q: A Low Overhead High Performance Buffer Management Replacement Algorithm](https://dl.acm.org/doi/10.5555/645920.672996). This paper tries to minimize overhead of LRU-K algorithm, using "2Q" algorithm.

# The overhead of LRU-K Algorithm

To implement [LRU-K Algorithm](https://github.com/hygoni/research-paper-summary/blob/main/Memory%20Management/Page%20Replacement%20Algorithm/LRU-K/summary.md), there should be K priority queues to manage last Kth access time. (K will be 2 or 3 as the says) that means every access to a buffer must update the queues at complexity of O(n), where n is number of buffer in cache. This paper tries to minimize overhead to constant time by using two queues (2Q).  

