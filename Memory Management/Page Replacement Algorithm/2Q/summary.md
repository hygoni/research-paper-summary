# 2Q: A Low Overhead High Performance Buffer Management Replacement Algorithm

This is summary of [2Q: A Low Overhead High Performance Buffer Management Replacement Algorithm](https://dl.acm.org/doi/10.5555/645920.672996). This paper tries to minimize overhead of LRU-K algorithm, using "2Q" algorithm.


# The overhead of LRU-K Algorithm

To implement [LRU-K Algorithm](https://github.com/hygoni/research-paper-summary/blob/main/Memory%20Management/Page%20Replacement%20Algorithm/LRU-K/summary.md), there should be K priority queues to manage last Kth access time. (K will be 2 or 3 as the says) that means every access to a buffer must update the queues at complexity of O(n), where n is number of buffer in cache. This paper tries to minimize overhead to constant time by using two queues (2Q).  

So purpose of this paper is to propose algorithm that is as good as LRU-K, but more efficient, and no (less) tuning parameters.  

## What we've learned from LRU-K

# Scan-Resistent
The strength of LRU-K algorithm is the ability to distinguish buffers that are accessed only once for scanning, and buffers that are frequently accessed (hot). The traditional LRU algorithm fails to distinguish them; If a buffer that is accessed only once is most recently accessed, that cold buffer is in LRU for a long time.  As 2Q is as good as LRU-K, 2Q is scan-resistent too.

# Correlated Reference Period
Even if a buffer is accessed only once, it must be kept in LRU cache for "a short period of time" = Correlated Reference Period. It may be accessed more than once in that short period of time. So we should avoid evicting such buffers.  

# 2Q Algorithm Pseudocode

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
    page out the tail of Alin, call it Y
    add identifier of Y to the head of Alout
    if(|A1out| >Kout)
      remove identifier of Z from
      the tail of Alout
    end if
    put X into the reclaimed page slot
  else
    page out the tail of Am, call it Y
    // do not put it on Alout; it hasn’t been
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
  else if (X is in Alout) then reclaimfor
    add X to the head of Am
  else if (X is in Alin) // do nothing
  else // X is in no queue
    reclaimfor(X)
    add X to the head of Alin
  end if
end
```
![accessing buffer again](https://raw.githubusercontent.com/hygoni/research-paper-summary/main/Memory%20Management/Page%20Replacement%20Algorithm/2Q/4E8DF802-56F1-44D6-A35D-2E29019632C8.jpeg)  

## Evaluation
