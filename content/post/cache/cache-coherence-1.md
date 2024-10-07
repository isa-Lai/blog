---
title: "Cache Coherence (1) - Introduction"
description: "What is cache coherence and cache consistency?"
date: 2024-10-07T07:50:47-04:00
image: cache/pipeline-coherence-interface.png
math: 
license: 
hidden: false
comments: true
categories:
    - Cache
tags:
    - Cache Coherence
    - Cache
    - Computer Architecture
---

## What is Consistency?

Consistency (a.k.a., memory consistency or memory model) is a property of a system that ensures all cache entries are consistent with the main memory. In other words, it is the process of ensuring that all copies of a memory location are updated to reflect the same value.

## What is Coherence?

Coherence (a.k.a., cache coherence) is a mechanism to support consistency models in systems with caches.

## How Incoherence Happens

A core is updating a cache line in its own cache, while this write is not yet propagated to other cores' caches.

For example in this figure, assuming that A is 42 in main memory and all cores' local caches. Core C1 updates the cache line with A = 43. However, this update has not been propagated to cores C2 yet, so C2's A will be stale value 42, and tracked in loop forever.

![Example of Incoherence](cache/example-of-incoherence.png)

## Coherence Interface

### Consistency-agnostic coherence

- Write is visible to other cores immediately before returning.
- Synchronously.
- Assume it is interacting with an atomic memory system with no caches present. Like cache is movoed and only memory is contained within the coherence box, like this figure.

![pipeline-coherence-interface](cache/pipeline-coherence-interface.png)

#### Coherence Invariants

- **Single-writer–multiple-reader (SWMR)**:
    - At one moment, at one location:
        - One core can wrire and read.
        - Other cores can only read.
- **Data-value invariant**:
    - The value at the start of an epoch is the same as that at the end of its last read-write epoch.
    - epoch: a block of time when a core is reading or writing.

#### Maintaining Invarients:

- When read:
    - Check if other cores have read-write state. 
    - Send message to end any read-write state.
- When write:
    - Send message to let other cores to obtains current value. 
    - Message ends any read-write or read-only, and new next read-write.

### Consistency-directed coherence

- Write can be visible to other cores after returning.
- Asynchronously.
- Need conherence protocol to ensure the order of writes.


## References

Sorin, D. J., Hill, M. D., Wood, D. A., & Nagarajan, V. (2020). *A primer on memory consistency and cache coherence* (2nd ed., pp. 1-16). Springer Nature. https://doi.org/10.1007/978-3-031-01764-3