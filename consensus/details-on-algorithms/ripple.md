---
description: >-
  Ripple Protocol Consensus Algorithm (RPCA) is a consensus algorithm allowing
  up to 20% of faulty nodes.
---

# Ripple

RCPA achieves consensus at each ledger-close and the trivial consensus will only be reached with a known probability. Only one consensus can be reached amongst all nodes, thus preventing a fork in the network. RCPA can achieves this in the presence of $$(n−1)/5$$ failures.

Each server, `s` maintains a unique node list (UNL) which is a set of other servers that `s` queries when determining consensus. Only the votes of the other members of the UNL of `s` are considered.

## Consensus definition

Reducing the validation of a transaction to a binary decision problem, consensus is defined according to:

1. every nonfaulty node makes a decision in a finite time
2. all nonfaulty nodes reach the same decision value
3. 0 and 1 are both possible values for all nonfaulty nodes

## Protocol definition

At each round:

1. each server creates a _candidate set_ from valid transactions (_**HOW???**_)
2. each server amalgamates the _candidate sets_ of all servers on its UNL
3. votes on veracity of the transactions
4. transactions that reach quorum are passed to the next round if there is one (other transactions are either discarded or included in the candidate set for the next ledger)
5. repeat 3-4 for a number $t$ of steps, until consensus requires at least 80% approval of a server UNL
6. all transaction meeting the requirement are applied to the ledger
7. the ledger is closed and becomes the new last-closed ledger
8. nodes with suspicious behavior are flagged

> _Note:_ how are the candidate sets created, in what order are the transactions applied

### Correctness

Since a transaction is only approved if 80% of the UNL of a server agrees with it, as long as 80% of the UNL is honest, no fraudulent transaction will be approved.

Thus, for a UNL with $n$ nodes in the network, the protocol will maintain correctness as long as: $$f \leq (n - 1) / 5$$ with $f$ the number of byzantine failures.

> Note: the protocol will fail but still not validate a fraudulent transaction until it reaches $$(4n + 1) / 5$$ byzantines failures

If a user tries to double-spend funds and both transactions are confirmed, when the first transaction is applied, the second will fail as the funds are no longer available.

Let $$p_c$$ be the probability of any node to join a colluding organization. The probability of correctness  is: $$p^* = \sum_{i=0}^{\lceil \frac{n-1}{5} \rceil} \binom{n}{i} p_c^i (1 - p_c)^{n-1}$$

UNL are chosen with the intent to minimize $$p_c$$. Since the nodes are not anonymous, nodes for a UNL can be selected from a mixture of backgrounds and opposed ideologies.

### Agreement

All nonfaulty nodes must reach consensus on che same set of transactions regardless of UNL.

The network cannot be separated into two cliques with low connectivity otherwise a fork might happen.

The upper bound on the connectivity is:

$$| \text{UNL}_i \cap \text{UNL}_j| \geq \frac{1}{5} \max(|\text{UNL}_i|, |\text{UNL}_j|) ~\forall i, j$$

## References

* [The Ripple protocol consensus algorithm. David Schwartz, Noah Youngs and Arthur Britto. 2014](https://ripple.com/files/ripple\_consensus\_whitepaper.pdf)
* [Analysis of the XRP Ledger Consensus Protocol. Brad Chase and Ethan MacBrough. 2018](https://arxiv.org/abs/1802.07242)
