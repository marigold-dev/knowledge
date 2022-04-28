# What is a Blockchain?

### What is a blockchain?

Blockchains are a specific form of [Distributed Hashtable](https://en.wikipedia.org/wiki/Distributed\_ledger): datas are distributed among multiple **nodes** via a **peer-to-peer network**.

Specificities of a blokchain are censorship resistence and double spend avoidance.

### A block-graph  <a href="#a-block-graph" id="a-block-graph"></a>

The blocks in the blockchain are linked together in a **directed graph** datastructure, which can be either a tree or a direct acyclic graph (DAG). The edges in the graph are implemented as hash pointers (i.e. the “cryptography” linking the blocks). This way the shape of the blockchain **cannot be forged**.

> **Note:** Hash pointers are when a piece of data is referred by its hash.

The block-graph has one vertex without any outgoing edges, which is the **genesis block**. This can be seen as the “the beginning of time” for that blockchain.

### The structure of a block

Each block has a header and a payload.

**The header** contains - at least - the following information:

* the block timestamp
* a hash-pointer to its parent block (or more pointers in case of a DAG implementation)
* the signature of the **Node** that produced the block

**The payload** is the list of transactions included in the block.

So each block is cryptographically signed by a **Node** and each transaction included in a block is also cryptographically signed by a **User** and this guarantees that a he can only act on his account.

