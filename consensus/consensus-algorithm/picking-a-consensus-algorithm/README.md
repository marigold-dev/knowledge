---
description: AKA oh no I've been tricked into (moral) philosophy
---

# Properties of consensus

## Censorship resistance versus selective censorship

Nodes should be able to submit operations, and to make an analogy with real life, people should be able to express LGBT-stance online even if their surroundings are utterly homophobic or transphobic or political critism from activists in a totalitarian regime.

This is why,  a blockchain (actually, any system really) is, ideally, censorship-resistant: users should be able to submit any and all operations to the network.

However, complete neutrality is not something that is inherently good or desirable: it's not because someone has an idea that this idea isn't shitty, morally doubtful or fraudulent. Indeed, most groups of people deem certain views as taboo and forbidden, for instance genocide denial point of views or pro-pedopornography opinions are often banned. This constitutes selective censorship.

The ability for a node to perform selective censorship is desirable in order to prevent one's instance from hosting hate-speech.

## Permissioned versus permission-less

Traditionally, consensus algorithms assume that the set of nodes is fixed: a prior configuration process has permissioned a mole or group of nodes to participate.

This assumption prevents a very simple Sybil attack that consists in creating enough virtual participants so that the network is overwhelmed by attackers and their proportion is way above the fault tolerance threshold.

A permission-less consensus protocols allows anyone to join dynamically the network and participate without prior permission/clearance. In place of permission to mitigate the Sybil attack threat, an "entry cost" or "barrier to entry" is set up. For instance, nodes may have to solve cryptographic hash puzzles like in Bitcoin, so that they are incentivized to behave properly.

## Leaderless versus leader(s)

Classical synchronous consensus algorithms are leaderless: agents exchange their proposals across the network, vote and decide to make the decision final at some point.&#x20;

However, consensus algorithms who operate on weak-synchronicity assumption ("indulgent consensus") are usally leader-based. Having a leader (or leaders) intuitively seems like introducing a weakness since a slow leader (intentional or not) can delay every decision. This concern is usually addressed through enhanced leader election and/or replacement and by using committees instead of a single leader.

## Objectivity versus subjectivity

{% content-ref url="../../../vocabulary/subjectivity.md" %}
[subjectivity.md](../../../vocabulary/subjectivity.md)
{% endcontent-ref %}

Objectivity/Subjectivity is linked to the **ability to support light-clients**: objective and weakly-subjective blockchains may have light-clients, strongly-subjective blockchains can't.&#x20;

## Liveness

## Tolerance to poisoning



## Recovery

### … on network partition

### … on sybil attacks

### … on DDoS attacks

## Light-client

## Overhead

