---
description: Original algorithm for Proof-of-Weight
---

# Algorand

## Consensus committee&#x20;

{% hint style="info" %}
**Consensus committee**\
****small set of reprensentatives randomly selected from the total set of users to run each step of the protocole.
{% endhint %}

Consensus committee members are elected randomly among all users based on weight (_then a sufficient fraction of committee members are honest_)

Users not part of the committee observe to learn the agreed-on block.

_**Problem: creates the possibility of targeted attack against chosen committee members**_

## Cryptographic sortition

Committee members are choosen in a private and non-interactive way.

Every user in the system can independantly determine if they are chosen to be on the committee (VRF on private key and blockchain) since membership selection is non-interactive, an attacker does not know which user to target until too late.

_**Problem: the adversary might try to target the committee member**_

There are different roles (to propose a block, to be in committee at some step etc)

#### &#x20;<a href="#participant-replacement" id="participant-replacement"></a>

## Participant replacement

Once the user sends the message proving they’re on the consensus committee, the committee member becomes irrelevant since a committee is elected at each step of the protocol.

## User secret keys

_**Problem: if the network isn’t synchronous, the attacker can have control on links between users and force users to agree on empty block, so that future selection seeds can be guessed.**_

Algorand is based on weak synchrony assumption: when performing cryptographic sortition for round r, Algorand checks the timestamp included in the block for round \$$r−1−(r mod R)\$$ (R number of rounds before the seed is changed) and uses the keys/weights form the last block that was created b-time before block r−1−(r mod R)._**Problem: trade-off for b. If b**_

&#x20;_**is very large, it mitigates the risks for attackers to break weak synchronicity but generates nothing-at-stake problem**_

_Appendix analyzes the trade-off_

## Minimizing unneccesary block transmissions

The sortition hash is used to prioritize blocks.

Discard messages about blocks that don’t have teh highst priority seen by the user yet.

Gossips 2 types of messages:

* priorities and proofs of the chosen blocks (around 200 bytes) that propagates quickly
* entire block if they aren’t discarded due to low priority

## Waiting for block proposal

Impacts performance.

If on threshold there are no block proposols, then an empty block is created and it may reach consensus on it.

## Acceptable failure probability and handling forks

See [discussion in 2.5](https://arxiv.org/pdf/1607.01341.pdf)

## Sybil attacks

By associating a weight to each user, Algorand guarantees consensus as long as a weighted fraction (at least 2/3) of the users are honest.

## DDoS

The key steps are performed in one-time use committees with a thousand users and taking a committe down would seriously impact the running network.

However, members are elected at every round and the attacker can't be sure of the committee identity until the vote is cast.

## Network partition

Not possible to provoke a fork by convincing honest users to accept 2 different blocks at the same round.

## References

{% embed url="https://people.csail.mit.edu/nickolai/papers/gilad-algorand-eprint.pdf" %}

{% embed url="https://arxiv.org/pdf/1901.10019.pdf" %}



{% embed url="https://arxiv.org/pdf/1607.01341.pdf" %}



