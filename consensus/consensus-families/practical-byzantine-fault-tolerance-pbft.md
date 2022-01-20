---
description: Paxos, Ripple, Tendermint
---

# Byzantine Fault Tolerance (BFT)

## Byzantine Fault Tolerance problem

Byzantine Fault Tolerance (BFT) is a feature of a distributed network to reach consensus (agreement on a value) even if some nodes in the system fail to respond or respond incorrect information (on purpose or not).

A BFT safeguard mechanism aims to reduce influence of faulty nodes by using collective decision making.

2 categories of byzantine failures exists:

1. fail-stop (a node fails, stops operating)
2. arbitrary-node failure (node doesn’t return an answer, responds incorrect result, responds deliberate misleading result, responds different things to differents part of the system, …)

No solution to the the Byzantine Generals problem (which assumes synchronicity and known participants) can tolerate more than `(n-1)/3` byzantine faults (33% of the system acting maliciously).

## Comparison



| Algorithm           | Bizantine fault | Details                                                           |
| ------------------- | --------------- | ----------------------------------------------------------------- |
| Theoretical         | (n-1)/3         | Synchronicity, known participants                                 |
| Paxos               | 20%             | Asynchronous                                                      |
| Attiya, Doyev, Gill | (n-1)/4         | Asynchronous                                                      |
| Alchieri _et al_    | (n-1)/3         | Asynchronous, unknown participants with connectivity restrictions |
| Ripple consensus    | (n-1)/5         | Asynchronous                                                      |

## Core properties

Nodes are sequentially ordered with one node being the leader node and others backup nodes. Nodes can transition from backup node to leader node:

* during every view (round)
* at view change protocol (if a predefined amount of time has passed without broadcasting a request)
* if a majority of nodes vote on the legitimacy of the current leading node.

In PBFT all honest nodes in the system help reaching a consensus on the state of the system using a majority rule.

A PBFT can only function if, given `m` the number of malicious nodes in the system, there are `3m + 1` honest functional nodes (Lamport).

The phases of a PBFT consenus with at most `m` faulty nodes allowed:

1. client sends a request to leader node
2. leader node broadcasts request to backup nodes
3. nodes (leader and backup) perform requested operation and send reply to teh client
4. request considered successful if at least `m+1` replies with the same result from different nodes

## Features of PBFT

* resource efficienty (no complex mathematical computations)
* transaction finality (transactions do not require multiple confirmations from every node)
* low reward variance (every node takes part in responding to the request so every node can be incentivized)

## Downsides of PBFT

* sybil attacks (one entity controls several others)
* scalibility (communication overhead due to communication with all other nodes)

## References

[https://lamport.azurewebsites.net/pubs/byz.pdf](https://lamport.azurewebsites.net/pubs/byz.pdf)
