##  Computer Interconnection Structures: Taxonomy, Characteristics, and Examples

As a undergraduate student, this paper was so interesting to me. There are many ways to connect computers in the world, and this paper tries to categorize them.  

## My personal notes

From personal experiences I thought computer network and multiprocessing are very different thing. But they were not. In "connecting computers" point of view, SMP (Shared Memory Processsors) and computers in my home network are not that different things. They are just a different way to connect computers. (Both are described in this taxonomy.)  

This text is my personal summary; Details are in the paper!  

## General Characteristics

### Modularity

### Connection Flexibility

### Cost of Fault Tolerance

### Logical Complexity

## Criterion For Categorization

### 1. Transfer Strategy

Does computers communicate Directly or Indirectly? If you connect two computers with a lan cable, communications in that structure is always Direct.  

Or when my smartphone and PC communicates through a wifi network, that's Indirect because communications in this structure always pass through wireless router.  

### 2. Transfer Control Method

When Transfer Strategy is Indirect, there are two choices. Is transfer control method Centralized? or Decentralized?  

For an easy example, in my home network, communications within home is always Centralized. All messages are controlled by a router. In more general term, a single centralized *switching element* controllers every *messages* in the network.  

But when the message is passed from inside to outside (e.g. when I'm googling), There is no single centralized switching element; It totally doesn't make sense. They communicate in a decentralized way.  

### 3. Transfer Path Structure

Is the path Dedicated to a computer, or Shared among computers?  

For example, in a bus network, all computers in that network shares a single bus (a path that message is passed). Sharing path is cheaper than giving computers Dedicated path. But when too many computers share a single path, it's likely to become a bottleneck.  

For another example, in a star network, a path is Dedicated to a computer. It isn't likely to become a bottleneck, but increased cost.  
