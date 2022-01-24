# Tendermint

### Overview

[Tendermint](https://tendermint.com) consensus is a [weakly synchronous](../../../vocabulary/network-partion-synchronicity.md) [BFT-like consensus](../../consensus-families/practical-byzantine-fault-tolerance-pbft.md) protocol tailored for blockchains.

Tendermint is not just a consensus protocol, however we will call Tendermint's consensus Tendermint from now on.

![Tendermint consensus algorithm](../../../.gitbook/assets/Overview\(1\).png)

### Main features

Tendermint is a 3 step algorithm:

1. proposal
2. prevote
3. precommit

Tendermint has locking rules to avoid commiting 2 different blocks at the same height.

### A word on synchronicity

Tendermint is weakly synchronous: it relies on a timeout when a round starts, otherwise it is an asynchronous consensus algorithm since validators only make progress if they hear from 2/3 of the other validators.

Prevote and precommit steps do have timeouts, however they appear to be there for practicality and the algorithm doesn't depend on them (at some point, communication happens). On the other hand, the proposal timeout is crucial and the algorithm does depend on it: without it, it is impossible to skip a proposer that left the network for good.

## External references

| Link                                                                                                                                                                                                         | Content                                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------- |
| [Tendermint Explained — Bringing BFT-based PoS to the Public Blockchain Domain (2018)](https://blog.cosmos.network/tendermint-explained-bringing-bft-based-pos-to-the-public-blockchain-domain-f22e274a0fdb) | Blog post - basic understanding                                   |
| [Correctness of Tendermint-Core Blockchains (2018)](https://drops.dagstuhl.de/opus/volltexte/2018/10076/pdf/LIPIcs-OPODIS-2018-16.pdf)                                                                       | Formalization + characterization + one-shot consensus             |
| [Dissecting Tendermint (2019)](https://hal.archives-ouvertes.fr/hal-01881212/document)                                                                                                                       | Identifying algorithmic bugs + correctness adversarial conditions |
| [Tendermint/Doc/Validators](https://docs.tendermint.com/master/nodes/validators.html)                                                                                                                        | Documentation - Validator                                         |

Correctness of Tendermint-Core Blockchains (2018)
