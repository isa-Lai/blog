---
title: "Cache Coherence (3) - Coherence Protocols"
description: Cache Coherence States | Snooping Protocol | Directory Protocol | MOESI/MSI
date: 2024-10-09T14:00:00-00:00
image: cache/cache-coherence-controller.png
math: true
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

## Finite State Machine

AKA *coherence controller*.

![Cache Coherence Controller](cache/cache-coherence-controller.png)

## Coherence Protocols

### Specifing Protocols

- **State**: For example, Not readable or writable (N), Read-only (RO), Read-write (RW). These is the state of the cache.
- **Events**: For example, Load, Store, Incoming Coherence request to optain read-write state.
- **Transitions**: Actions

|    | Load                    | Store                   | Incoming Coherence request to optain read-write state |
|----|-------------------------|-------------------------|-------------------------------------------------------|
| N  | Issue request to get RO | Issue request to get RW | NA                                                    |
| RO | Give data               | Issue request to get RW | NA/N                                                  |
| RW | Give data               | Write data              | Send **Block** to requestor/N                         |

### States

Implemented ststes shoudl consider:

- **Validity**: Has the up-to-date value. Can read, but can write if it is also exclusive.
- **Dirtiness**: Write to up-to-date, but not yet push to lower memory.
- **Exclusivity**: No other private cache has a copy of the block.
- **Ownership**: Owner is responsible for responding to coherence reqeust for that block. 

#### MOESI/MSI

- **Modified**: Valid, exclusive, owned, and maybe dirty. Can read and write.
- **Owned**: Valid, and owned, and maybe dirty. Read-only. Other core also have read-only copy but not owners. 
- **Exclusive**: Valid, exclusive, and clean. Read-only.
- **Shared**: Valid and clean. Read-only.
- **Invalid**: Invalid.

![MOESI/MSI States](cache/MOESI-states.png)

#### Transiten States

States that is inbetween two states. ie.,  $IV^D$ (in Invalid going to Valid, waiting for DataResq).

### Transactions

| Transaction | Goal of Requestor |
|-------------|-------------------|
| GetShared (GetS) | Obtain block in Shared (read-only) state |
| GetModified (GetM) | Obtain block in Modified (read-write) state |
| Upgrade (Upg) | Upgrade block state from read-only (Shared or Owned) to read-write (Modified); Upg (unlike GetM) does not require data to be sent to requestor |
| PutShared (PutS) | Evict block in Shared state* |
| PutExclusive (PutE) | Evict block in Exclusive state* |
| PutOwned (PutO) | Evict block in Owned state |
| PutModified (PutM) | Evict block in Modified state |

*Some protocols do not require a coherence transaction to evict a Shared block and/or an Exclusive block (i.e., the PutS and/or PutE are "silent").


| Event | Response of (Typical) Cache Controller |
|-------|----------------------------------------|
| Load | If cache hit, respond with data from cache; else initiate GetS transaction |
| Store | If cache hit in state E or M, write data into cache; else initiate GetM or Upg transaction |
| Atomic read-modify-write | If cache hit in state E or M, atomically execute RMW semantics; else GetM or Upg transaction |
| Instruction fetch | If cache hit (in I-cache), respond with instruction from cache; else initiate GetS transaction |
| Read-only prefetch | If cache hit, ignore; else may optionally initiate GetS transaction* |
| Read-Write prefetch | If cache hit in state M, ignore; else may optionally initiate GetM or Upg transaction* |
| Replacement | Depending on state of block, initiate PutS, PutE, PutO, or PutM transaction |

*A cache controller may choose to ignore a prefetch request from the core.

### Major Protocal Design Options

Directory vs. Snooping
- **Directory protocol**: A directory is used to track the state of each block. Cache controller send request to the *home* of that block.
- **Snooping protocol**: A shared bus is used to broadcast the state of each block. Assume requests arrive in totol order. 

Invalidate vs. Update
- **Invalidate protocol**: Write will invalidate the block, so other core cannot read. 
- **Update protocol**: Write update all copies of the block. 

## Snooping Protocol

Usually using a bus to broadcast the requests, but not necessarily has to use a bus. 

![MSI: Transitions between stable states at cache controller](cache/MSI-for-cache.png)

### SIMPLE SNOOPING SYSTEM MODEL: ATOMIC REQUESTS, ATOMIC TRANSACTIONS

Simple snooping for cache controller, labeled “(A)” denotes that this transition is impossible because transactions are atomic on bus:

<table>
  <thead>
    <tr>
      <th rowspan="3">States</th>
      <th colspan="3" rowspan="2">Processor Core Events</th>
      <th colspan="7">Bus Events</th>
    </tr>
      <th colspan="4">Own Transaction</th>
      <th colspan="3">Other Transaction</th>
    </tr>
    <tr>
      <th>Load</th>
      <th>Store</th>
      <th>Replacement</th>
      <th>Own-GetS</th>
      <th>Own-GetM</th>
      <th>Own-PutM</th>
      <th>Data</th>
      <th>Other-GetS</th>
      <th>Other-GetM</th>
      <th>Other-PutM</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>I</td>
      <td>Issue GetS /I<sub>S</sub><sup>D</sup></td>
      <td>Issue GetM /I<sub>M</sub><sup>D</sup></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
    <tr>
      <td>I<sub>S</sub><sup>D</sup></td>
      <td>Stall Load</td>
      <td>Stall Store</td>
      <td>Stall Evict</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Copy data into cache, load hit /S</td>
      <td>(A)</td>
      <td>(A)</td>
      <td>(A)</td>
    </tr>
    <tr>
      <td>I<sub>M</sub><sup>D</sup></td>
      <td>Stall Load</td>
      <td>Stall Store</td>
      <td>Stall Evict</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Copy data into cache, store hit /M</td>
      <td>(A)</td>
      <td>(A)</td>
      <td>(A)</td>
    </tr>
    <tr>
      <td>S</td>
      <td>Load hit</td>
      <td>Issue GetM /S<sub>M</sub><sup>D</sup></td>
      <td>- /I</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>- /I</td>
      <td></td>
    </tr>
    <tr>
      <td>S<sub>M</sub><sup>D</sup></td>
      <td>Load hit</td>
      <td>Stall Store</td>
      <td>Stall Evict</td>
      <td></td>
      <td></td>
      <td></td>
      <td>Copy data into cache, store hit /M</td>
      <td>(A)</td>
      <td>(A)</td>
      <td>(A)</td>
    </tr>
    <tr>
      <td>M</td>
      <td>Load hit</td>
      <td>Store hit</td>
      <td>Issue PutM, send Data to memory /I</td>
      <td></td>
      <td></td>
      <td></td>
      <td></td>
      <td>Send Data to req and memory /S</td>
      <td>Send Data to req /I</td>
      <td></td>
    </tr>
  </tbody>
</table>

- Atomic request: Issue request ensures that another core's request will not ordered ahead of its, when this cache controller seeks to upgrade permission (I->S, S->M, or I->M). Thus, controller transition immediately to state $IS^D$, $IM^D$, or $SM^D$.
- Atomic transaction: No subsequent requests from a block will occur until the current transaction completes. Resquest always comes with reponse in pair. 

BASELINE SNOOPING SYSTEM MODEL: NON-ATOMIC REQUESTS, ATOMIC TRANSACTIONS

### MESI

- Rely on atomic transactions.
- Use `E` instead of `S`: when GetS occurs when no other cache has access to the block. 
- Upgrade from `E` to `M` is silent. No transactions needed. Elinimate half of the transactions. 

![MESI at cache controller](cache/MESI-for-cache.png)

Note: in the figure when it says, "mem in I", it means in the lower level memory (ie,. LLC or DRAM), that cache block is in `I` which states that no private cache has a copy of that block. It does not mean the cache in the private cache is in `I` state. 

### MOSI

- Rely on atomic transactions.
- Eliminate extra data to update LLC when a cache receives a GetS request in the M/E state. 
- Using dirty bit, eliminate unnecessary write to LLC (if block is written again before write back to LLC). 
- Owner is used to reduce the access latency. Without owner, even a core's private has a copy in `S`, it cannot forward the copy to other because no one know who is the owner. Only the defined owner can forward the copy. 

![MOSI at cache controller](cache/MOSI-for-cache.png)

### Non-atomic bus

- Send request without waiting for previous response. 
- Pipelined bus: response in same order as request.
- Split transaction bus: response in random order depending on latency.

```
Atomic bus:
Address Bus:  Request 1 ----------- Request 2 ------------ Request 3
Data Bus:               Response 1 ----------- Response 2 ----------- Response 3

Pipelined (non-atomic) bus:
Address Bus:  Request 1 Request 2 Request 3
Data Bus:               Response 1 Response 2  Response 3

Split transaction (non-atomic) bus:
Address Bus:  Request 1 Request 2 Request 3
Data Bus:               Response 2 Response 3  Response 1
```

- non-atomic system model: 
    - can use FIFO queue to buffer messages. 

## Directory Protocol

- Directory: a global view of the coherence state of each block. 
- Forwarding, the directory controller can forward the request to the owner of the block.

A directory entry can be like (N: number of nodes):

|state|owner|starer list (one-host bit vector)|
|----|-----|------------------------------|
|2-bit| $Log_2(N)$-bit | $N$-bit |

![MSI Directory Protocal](cache/MSI-directory-protocal.png)

### Avoiding Deadlocks

- Deadlock: Event `A` causes event `B` and both require resource allocation. Deadlock can occur when the resources are both not available until one of the event completes. For example, `GetS` can causes `Fwd-GetS` which uses the same resources. 
```
    Full
    | Queue | ------> C1 ----->
       ^                       |
       |                       |
       |                       |
       |                       |
       -----C2<--------------| Queue |
                                Full
```

To avoid deadlock, we can use different netwroks for different calss of messages. This avoid dependence between different messages. ie,. response and request. 

### Detailed Protocal Specification

MSI Directory Protocol - directory controller
|       | GetS                                             | GetM                                              | PutS-NotLast                                    | PutS-Last                                      | Put M+data from Owner                                      | PutM+data from Non-Owner                                  | Data                         |
|-------|--------------------------------------------------|--------------------------------------------------|------------------------------------------------|------------------------------------------------|------------------------------------------------------------|------------------------------------------------------------|------------------------------|
| I     | Send data to Req, add Req to Sharers/S           | Send data to Req, set Owner to Req/M              | Send Put-Ack to Req                            | Send Put-Ack to Req                            |                                                            | Send Put-Ack to Req                                           |                              |
| S     | Send data to Req, add Req to Sharers             | Send data to Req, send Inv to Sharers, clear Sharers, set Owner to Req/M | Remove Req from Sharers, sent Put-Ack to Req   | Remove Req from Sharers, send Put-Ack to Req/I |                                                            | Remove Req from Sharers, send Put-Ack to Req                 |                              |
| M     | Send Fwd-GetS to Owner, add Req and Owner to Sharers, clear Owner/S<sup>D</sup> | Send Fwd-GetM to Owner, set Owner to Req         | Send Put-Ack to Req                            | Send Put-Ack to Req                            | Copy data to memory, clear Owner, send Put-Ack to Req/I      | Send Put-Ack to Req                                           |                              |
| S<sup>D</sup> | Stall                                            | Stall                                            | Remove Req from Sharers, send Put-Ack to Req   | Remove Req from Sharers, send Put-Ack to Req   |                                                            | Remove Req from Sharers, send Put-Ack to Req                 | Copy data to memory/S         |

## References

Sorin, D. J., Hill, M. D., Wood, D. A., & Nagarajan, V. (2020). *A primer on memory consistency and cache coherence* (2nd ed., pp. 91-191). Springer Nature. https://doi.org/10.1007/978-3-031-01764-3

