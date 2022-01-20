---
description: Quick overview of consensus algorithms
---

# Consensus algorithm

## Basic definition

Blockchains face 3 main types of problems:

1. **Correctness** (ability to make the difference between a correct and fraudulent transaction, to guarantee the transaction really comes from where it claims to be)
2. **Agreement** (maintaining a global truth)
3. **Utility** (the system has to be useful, minimize latency)

If you think of a blockchain as a data storage and management application on top of a peer-to-peer like technology, it becomes clear real quick that the method that adds a block to the blockchain without compromising data integrity is a key component to the blockchain and it’s security. This method is called a consensus algorithm.

{% hint style="info" %}
A consensus algorithm can be seen as a verification and validation protocol in the absence of an administrator. Its purpose it to bring all nodes in agreement in an environment where nodes don’t know and don’t trust each other.
{% endhint %}

## Core properties

Core problem of multi-agent systems: a number of agents of the system need to reach an agreement on some value.

Since agents may fail or lie, a consensus protocol has to be fault tolerant.

1. termination (at some point every correct agent will decide a value)
2. integrity/validity (if all correct agents propose the same value X, then any correct agent must decide X)
3. agreement (every correct agent must agree on the same value)



