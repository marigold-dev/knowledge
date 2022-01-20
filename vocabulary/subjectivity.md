# Subjectivity

A blockchain often presents more than one valid chain: there are multiple possible paths from the genesis block to the most recent block who can all be considered as valid.

Depending on the blockchain design, nodes aren't always able to find out quickly which one is the active chain.

In a objective chain, the new nodes that join the network are expected to quickly choose the active/longest chain (such as in Bitcoin with the chain with the most accumulated work).

In a strongly subjective chain, finding out which one is the active chain is not as simple because the consensus algorithm relies on the interaction between nodes (and not a simple rule such as "longest chain"). Subjectivity is linked to the fact that nodes need to receive information from others when they try to determine the current state.

Weak subjectivity (requirement for Proof-of-Stake) happens when nodes don't have a subjectivity problem when they are continuously on line but have one when they join for the first time or after a long disconnection.
