# Overlay network

{% hint style="info" %}
A network that exists on top of another network. Here, a set of storage node which all maintain a set of links to other nodes.

Nodes pick their neighbors according to a specific topology.
{% endhint %}

In a DHT (Distributed Hash Table), overlay networks are defined by a set of nodes $$N = \{n_0 , \dots n_j\}$$ such as for any key $$k$$, the node $$n_i$$ either has a node ID that owns $$k$$ or as a link to an node whose node ID is _closer_ (according to the keyspace distance metric) to $$k$$.

{% hint style="info" %}
**Keyspace partitioning** method to split a keyspace into sensical "clusters" that make finding a key easy and efficient.

Many different algorithms exist. Keyspace partitioning as used in DHT has a core property: adding or removing of a node only changes the set of keys owned by adjacent IDs (all other nodes are unaffected).
{% endhint %}

In addition to correctness of the routing technique, some constraints are essential for an overlay network to be usable.

For requests to complete in a decent amount of time:

1. the route length must be low (maximum number of hops in a route has to be reasonable);
2. the node degree must be low (maximum number of neighbors of any given node).

| Maximum node degree     | Maximum route length                   | Algorithms                        |
| ----------------------- | -------------------------------------- | --------------------------------- |
| $$\mathcal{O}(1)$$      | $$\mathcal{O}(\log n )$$               | Koorde (with constant degree)     |
| $$\mathcal{O}(\log n)$$ | $$\mathcal{O}(\log n )$$               | Chord, Kademlia, Pastry, Tapestry |
| $$\mathcal{O}(\log n)$$ | $$\mathcal{O}(\log n / \log(\log n))$$ | Koorde (with optimal lookup)      |
