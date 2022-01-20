# FA2 NFTs vs ticket-based NFTs

### What's the difference between FA2 NFTs and ticket-based NFTs?

**Answer** FA2 NFTs are based on a ledger contract per the FA2 interface that records who owns which NFTs. Tickets are "reified" in a data structure that you can't duplicate. You can call `SPLIT_TICKET` to mako copies but there is an `amount` field on a ticket that should be set (to 1 for instance)  and the sum of the tickets created by `SPLIT_TICKET` must be equal to the original amount. In this example there could be only a single ticket with amount `1` and that would be the true NFT.

In principle ticket-based NFTs should be more efficient/easir to work with since you don't have to make a call to the ledger contract every time you want to tansfret it and instead simply pass the actual ticket.

As of November 2021 TZ1 accounts can't currently hold tickets and things are done via another contract.

{% hint style="info" %}
For further reading on [FA2 read here](https://medium.com/tqtezos/introducing-fa2-a-multi-asset-interface-for-tezos-55173d505e5f).
{% endhint %}
