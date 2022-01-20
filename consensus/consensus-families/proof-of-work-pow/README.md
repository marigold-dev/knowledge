---
description: A solution that is difficult to find but is easy to verify (Bitcoin)
---

# Proof-of-Work (PoW)

## Basic definition

The general idea of this consensus algorithm: _**A solution that is dificult to find but is easy to verify**_.

To add a new block (linking a newly crafted block to the last block in the valid blockchain) a miner has to find the right solution to _hard-to-solve mathematical problem_.

The _hard-to-solve mathematical problem_ is of the sort: given entry data `A`, find a number `x` such as `append(hash(x), A) < target_hash`

The blockchain is **protected from tampering** since modyfing a block can only be done by crafting a block a new block with the same predecessor which requires to regenerate all sucessors **and** redoing all the contained work which is practically impossible.

Common cryptographic protocols used in PoW:

* SHA-256
* Scrypt
* SHA-3

## Features of PoW

* hard to find a solution for the mathematical problem
* easy to verify the correctness of the solution

## Mains issues

* 51% risk (if controlling 51% or more of the nodes in the network, the blockchain can be corrupted)
* time consuming (miners check many nonce value to find the right solution to the mathematical problem)
* resource consuming (high amounts of computing power so water, energy, mineral, space, etc)
* high transaction confirmation time
