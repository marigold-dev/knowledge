---
description: >-
  Consensus algorithms are often described as the key component of blockchain.
  This is wrong.
---

# What consensus is and isn't

### How the need emerged

First, let’s focus on the reason why consensus algorithms exist since they are quite a recent addition to the slew of algorithm families and buzzwords.

A long time ago, in a galaxy far far away, people designed their systems in a very centralized way. Clients were all connected to a central server who stored data and user information. This makes things easy to code, simple to deploy, affordable to maintain and overall practical. Sure, this raised a number of security and privacy issues for users on the network, and everything was prone to drastic failures, and access time for users far away from the central owner was a nightmare, but it was convenient.

Since convenience is not an excuse for flaws\[2], two improvements to centralized systems were made: decentralized systems (roughly speaking they address security and privacy issues) and distributed systems (who mainly address failures and access time problems).

The typical distributed system problem is to have distributed database amongst a number of servers that is resilient to a server being offline (rebooting after an upgrade, network issues) or a server sending faulty messages (might not be running the good version of the software). This created a new set problems for nodes around the question “which value should I use?”\[3].

However distributed system can do more than allow data distribution: they can allow computing power distribution. Adding decentralization to this lead to the golden age of peer-to-peer (the rise of [Napster](https://en.wikipedia.org/wiki/Napster) or [BitTorrent](https://en.wikipedia.org/wiki/BitTorrent)) quickly followed with a whole new bunch of problems:

* defining trust, trust levels and distrust in the system;
* sending a “wrong” or corrupted file (solved through the use of Merkle trees);
* people cheating and/or being unreliable. For instance nodes in a peer-to-peer gaming systems would delay their actions to see what other nodes do before announcing their actions, it’s the look-ahead cheating problem\[4].

Nodes that misbehave by being offline, faulty or plain adversarial (people managing the node want to cheat and/or want other people to fail) are referred to as “byzantine” nodes.

### Consensus problem definition

Many of those new problems are the same thing: _**“how do we make a bunch of nodes agree on a single value in an environment where some might be byzantine?”**_\
This is the consensus problem, and is why we need and have consensus algorithms.

### Consensus problem definition in a blockchain context

If you define a blockchain as a data storage and management application on a top of a peer-to-peer like technology, the relevance of consensus algorithm becomes obvious (and consensus can be defined as a method that adds blocks to the blockchain without compromising data integrity).

### Consensus core properties

Key properties for consensus algorithms appear from the previous description:

1. fault tolerance (it operates under the assumption that some nodes are byzantine)
2. termination (at some point every correct node decides on some value)
3. validity (if the decision is the value X, then X was proposed by some correct node)
4. integrity (no correct node decides twice)
5. agreement (no 2 correct nodes decide differently)

Combining the _termination property_ and the _integrity property_ ensures that every correct node decides exactly once. The _validity property_ ensures that the consensus cannot invent a decision value on its own. The _agreement property_ is the main feature of consensus: two correct nodes that decides something decide on the same value. The _fault tolerance property_ is self-explanatory.

### What consensus should not be doing

With those properties and this context in mind, you’ll agree that _blockchains cannot be reduced to their consensus algorithm_.

Consensus algorithms are about making supposedly adversarial nodes cooperate to reach an agreement on a value and that’s it.

A blockchain has many features that are in no way or shape related to the consensus algorithm it works with, such as:

* assessing data availability which is the purpose of the _**data availability layer**_;
* incentivizing participation and good behavior, which is _**cryptoeconomics**_\[5];
* making sure a transaction is not malicious, does not perform double spending and basically ensuring that the transaction is legal, which is a _**transaction validation problem**_ (consensus is agreeing on the ordering of validated transaction);
* specifying the acceptance of smart contracts or transactions, that’s a _**computing feature issue**_;
* deciding how nodes should not spam one another, that’s the purpose of the _**network layer problem**_\[6].

### Conclusion

A blockchain is a function of a number of parameters. However, we haven’t fully reached consensus on how many their are, nor what they are.

_$blockchain = f(consensus,network,data\_availability,validation,cryptoeconomics)_

‍

Unfortunately, those parameters are not independant\[7]: _everything parametrize everything else_ but blockchain is a brand new field, people will figure things out eventually.

We hope you are convinced that:

1. a blockchain cannot be reduced to its consensus algorithm
2. consensus is not that important

Our next blog post will focus on the huge number of properties you need to consider while choosing a consensus algorithm, and how much this is critical for your blockchain\[8].

‍

1. look at us being strongly opinionated right from the start
2. motto of a dreaded invasive specie you might have heard of, they are called “computer science nerds”
3. an easy solution would be to choose the most recent value but it’s a terrible idea since you can’t trust clocks (we will circle back on that idea at some point)
4. this problem is solved by lockstep protocol that has drawbacks: everything is slowed down to the speed of the highest latency, which in itself, is a whole new class of problems (computer science in a nutshell).
5. cryptoeconomics is a fancy new field that studies the economics interactions in adversarial environments. Here, we mean specifying the incentives to make actors willing to contribute positively to the network and the make systems thrive in the presence of adversaries.
6. for folks who read things about optimistic roll-ups, it’s not up to the consensus to aggregate valid transactions so that multiple transactions from or to one person are seen as a single transaction, that’s a _**transaction aggregation problem**_.
7. even if network and consensus can seem to be pretty independant in a theoretical point of view, implementing spam protection ties them together (the protocol can minimize the number of messages)
8. if you think this is a show of contradictory sprit, wait for the next post on consensus…

##

##

##

