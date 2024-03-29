# 2Q: A Low Overhead High Performance Buffer Management Replacement Algorithm

This is summary of [2Q: A Low Overhead High Performance Buffer Management Replacement Algorithm](https://dl.acm.org/doi/10.5555/645920.672996). This paper tries to minimize overhead of LRU-K algorithm, using "2Q" algorithm.  

This is a summary of the paper; All details are in paper!

# The overhead of LRU-K Algorithm

To implement [LRU-K Algorithm](https://github.com/hygoni/research-paper-summary/blob/main/Memory%20Management/Page%20Replacement%20Algorithm/LRU-K/summary.md), there should be K priority queues to manage last Kth access time. (K will be 2 or 3 as the says) that means every access to a buffer must update the queues at complexity of O(log(n)), where n is number of buffer in cache. This paper tries to minimize overhead to constant time by using two queues (2Q).  

So purpose of this paper is to propose algorithm that is as good as LRU-K, but more efficient, and no (less) tuning parameters.  

## What we've learned from LRU-K

# Scan-Resistent
The strength of LRU-K algorithm is the ability to distinguish buffers that are accessed only once for scanning, and buffers that are frequently accessed (hot). The traditional LRU algorithm fails to distinguish them; If a buffer that is accessed only once is most recently accessed, that cold buffer is in LRU for a long time. 2Q is scan-resistent too, like LRU-K.

# Correlated Reference Period
Even if a buffer is accessed only once, it must be kept in LRU cache for "a short period of time" = Correlated Reference Period. It may be accessed more than once in that short period of time. So we should avoid evicting such buffers.  

# 2Q Algorithm Pseudocode

The parameters in here are Kin (length of A1in queue) and Kout (length of A1out Queue).

## Reclaiming for new buffer X
```bash
// If there is space, we give it to X.
// If there is no space, we free a page slot to
// make room for page X.
reclaimfor(page X)
begin
  if there are free page slots
    then put X into a free page slot
  else if(|A1in| > Kin)
    page out the tail of A1in, call it Y
    add identifier of Y to the head of A1out
    if(|A1out| > Kout)
      remove identifier of Z from
      the tail of A1out
    end if
    put X into the reclaimed page slot
  else
    page out the tail of Am, call it Y
    // do not put it on A1out; it hasn’t been
    // accessedfor a while
    put X into the reclaimed page slot
  end if
end
```
![new buffer](https://raw.githubusercontent.com/hygoni/research-paper-summary/main/Memory%20Management/Page%20Replacement%20Algorithm/2Q/2EFA8C20-546D-491A-82AA-7494F219C662.jpeg)  

## Accessing buffer X

```bash
begin
  if X is in Am then
    move X to the head of Am
  else if (X is in A1out) then reclaimfor
    add X to the head of Am
  else if (X is in A1in) // do nothing
  else // X is in no queue
    reclaimfor(X)
    add X to the head of A1in
  end if
end
```
![accessing buffer again](https://raw.githubusercontent.com/hygoni/research-paper-summary/main/Memory%20Management/Page%20Replacement%20Algorithm/2Q/4E8DF802-56F1-44D6-A35D-2E29019632C8.jpeg)  

# Evaluation

It's a bit weird that the paper shows performance data only in form of hit rate, because hit rate does not show actual time spent. So the data does not explain anything about its overhead. (But yeah, I can't imagine 2Q has more overhead than LRU-K.)  

The performance data on synthetic experiments (based on statistical distribution), and real data (DB / windowing / ...etc) shows that hit rate of 2Q is overally, slightly higher than LRU-K.  

# Parameters of 2Q Algorithm

There are two parameters in 2Q: Kin and Kout.  

Author of the paper did some experiement and thought about storing whole pages or tags (pointers) of buffer. storing whole pages does not cause page fault when referencing, but it borrows buffers from Am. The author concluded that storing tags in A1out is better approach because it was not sensitive to size of A1. And the paper says Kin should be 25% of total pages and length of Kout should be 50% of A1in.

## Responsiveness

The access pattern of buffers change as time passes. How are LRU, LRU-2, 2Q responsive to changes in locality? The paper says that data shows LRU is most responsive (but this is too responsive.) to change, and LRU-2 sacrifies responsiveness to some degree for better hit rate.  

And responsive of 2Q is determined by Kout. when Kout is low (5% of Kin), it was less responsive than LRU-2. but when increased to 50%, it was very similar to LRU-2.
