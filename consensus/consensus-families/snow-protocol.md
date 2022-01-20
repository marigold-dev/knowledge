---
description: Variations on Proof-of-Stake
---

# Snow protocol

## Basic definition

Unlike traditional consensus protocols where one or more nodes typically process linear bits in the number of total nodes per decision, no node processes more than logarithmic bits. The efficiency of the protocols stems partly from removing the leader bottleneck: each node requires $$O(1)$$ communication overhead per round and $$O(\log n)$$ rounds in expectation.

Two big ideas are sub-sampling and transitive voting.

## Feature of snow

* probabilistically safe up to a safety threshold
* acceptance/rejection are final and irreversible and take a few seconds
* doesn’t need to have slashing

## Disavantage

* probabilistically safe (new, lack of papers)
* strong subjectivity
