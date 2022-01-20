# Optimistic Rollups (ORU)

{% hint style="info" %}
This page tries to answer the following questions:

* Why do we need Layer 2?
* What are optimistic rollups?
* What issues are they supposed to solve?
{% endhint %}

One of the biggest challenges in the blockchains is improving performances under tight resource constraints (e.g. CPU, bandwidth, memory, disk space).

Performance is measured in 2 ways:

* **Throughput**: The number of transactions the system can process per second.
* **Latency**: The time it takes for a transaction to be processed.

When you want to scale a blockchain you can either:

* **Make the blockchain itself have a higher transaction capacity**: that's the purpose of making the economical protocol of blockchain evolve (e.g. [Ethereum 2](https://ethereum.org/en/eth2/vision/) or [Tezos Tenderbake](https://blog.nomadic-labs.com/a-look-ahead-to-tenderbake.html)) but also the complete field of sharding on blockchains.
* **Change the way that you use the blockchain:** Instead of putting all activity on the blockchain directly, users perform the bulk of their activity off-chain. **Layer 2** term refers to a whole category of tactics to achieve this goal. The main chain (Layer 1) is processing deposits and withdrawals, and verifying proofs that everything happening off-chain is following the rules. There are multiple ways to do these proofs, but they all share the property that verifying the proofs on-chain is much cheaper than doing the original computation off-chain.&#x20;

Major types of layer-2 scaling are [state channels](../../other-layer-2/state-channels/), [sidechains](../../sidechain/sidechain-for-noobs.md) and **rollups** with different strengths and weaknesses.

### Optimistic Rollup (ORU)

**Rollups** is meaning that transactions are commited to main chain in bundles by an aggregator.

**Optimistic** is meaning that aggregators publish only information needed with no proofs, assuming the aggregators run without commiting frauds, and only providing proofs in case of fraud.

The principle of a ORU is having an aggregator which collect operations that will be executed in the layer-2. That aggregator compute a new state root (e.g. a [Merkle root](https://hackmd.io/@corneliuhoffman/Merkle-proofs)) and create an operation in layer-1 that contains this state root. Anyone can prove it is invalid with a fraud proof within some timeout by posting the valid state root along with the merkle proofs required to prove it. On a successful fraud proof, a part of the aggregator's bond is paid to the prover and a part is burned. If the timeout expires without a fraud proof the layer-2 transaction is considered safe at the layer-1 .

An aggregator is refered as a `rollup node`

ORUs have many desirable features:

* **Trustless**. You don't have to trust that a majority of the ORU's nodes are honest to always be able to withdraw your funds from the rollup. In actual designs, one honest node is enough.
* **Permissionless**. Anyone can aggregate operations for an ORU since all the rollup block data is posted on main chain and available.
* **Capital efficient.** Unlike channels, ORUs do not require that users lock up a bond upfront. Only node providers do.
* **Resistant to chain congestion**. Fraud is proven at the block level rather than the channel closure.

TODO: Add some scenarii
