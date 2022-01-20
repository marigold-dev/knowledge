# Network partition/Synchronicity

An attack in which the communication links between users are targeted, creating partitions of the network.

During a network partition, the network is asynchronous.

In some designs, if the partition lasts long enough, the adversary may convince different partitions to accept different blocks at the same height in the blockchain. Contradictory transactions are accepted, potentially leading to double-spending when the partition is resolved (if it is possible).

{% hint style="info" %}
On asynchronous/synchronous/partially synchronous models, please read [this blog article](https://decentralizedthoughts.github.io/2019-06-01-2019-5-31-models/)
{% endhint %}
