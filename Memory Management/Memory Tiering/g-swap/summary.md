# Software-Defined Far Memory in Warehouse-Scale Computers

This is summary of [Software-Defined Far Memory in Warehouse-Scale Computers](https://dl.acm.org/doi/10.1145/3297858.3304053). This paper tries to save Total Cost of Ownsership on Warehouse-Scale Computers by compressing cold memory and tuning parameters in ML-based way.  

# Far Memory

Slowdown in DRAM technology and increasing demand of more memory, makes it more expensive to build a system that requires lots of memory. and the DRAM make up a large part of the price when building a infrastructure.  

So it's not surprising recent reasearches try to reduce cost of memory. One approach to this problem is to introduce hierarchy (tier) to memory.
For exapmle, one can put less used memory to State-Of-The-Art NVMe SSDs instead of expensive DRAMs. Then DRAM is Near and Fast memory, NVME SSD is Far and Slow memory.  

To summary, "Far Memory" is introducing such a hierarchy to memory. It may not be SSDs. Far Memory may be memory from other servers connected with network, or anything.  

# Software-Defined Far Memory

Unlike SSDs or network approach, this paper uses compression to reduce cost of memory. In this approach, the kernel proactively compresses cold memory (less used memory) to save money. The end result is compressed memory whose price is 67% cheaper than DRAM, and provides one-digit microseconds latency. (6~9us).  

The paper demonstrates this approach can save 4-5% of total cost for Warehouse-Scale Computers and does not hurt its performance badly.  

# Characteristics of Warehouse-Scale Computers

1) WSCs should provide good performance to some degree. If far memory hurts its performance too much, we need more hardware to fill the gaps.  
2) Various types of applications makes it impractical to tune parameters manually  
3) As memory behavior changes dynamically it should be able to react to the change.  

This paper solves 2) 3) by using ML-based tuner. and demonstrates it doesn't hurt too badly.  

# Design Overview

## kstaled

## kreclaimd

## node agent

## ML-based autotuner
