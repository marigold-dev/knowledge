---
description: >-
  blockchain version of kidnappers taking picture of the victim with a newspaper
  (Solana)
---

# Proof-of-History (PoH)

## Basic definition

the idea is to create a historical record to prove that an event has occured at a specific moment in time.

Verifiable delay function = function that takes a prescribded time to compute, even on parallel computation and whose output can be quickly and publicly verified

## Solana

Solana’s implementation uses a sequential pre-image resistant hash that used the previous step output as the next step input. For a SHA256 functio, the process cannot be parallelized without a bruteforce attack of 2128 cores. Also uses Tower BFT

## References

[https://github.com/solana-labs/solana](https://github.com/solana-labs/solana)
