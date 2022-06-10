---
description: Serialization related questions.
---

# Serialization

### Why do we serialize things like operations and keys?

**Question:** The `Operation` module uses `Data_encoding` to convert between bytes and normal data structures. Why do we serialize everything (operations, keys)? What does serializing this things let us do that we wouldn't be able to do otherwise?

**Answer**: [Irmin](https://irmin.org/) is the backend used by all of Tezos to store data. [Irmin](https://github.com/mirage/irmin) is a bytes based data store so everything needs to be serialized into bytes before storage. Moreover, things are sent as bytes on the network so one needs to serialize data before sending it to the network.

{% hint style="info" %}
Irmin is bytes-based. Any information not defined by protocol itself such as transaction data, hashes, account info, etc needs to be serialized in order to be sent out or stored and deserialized to be useful upon arrival.
{% endhint %}

