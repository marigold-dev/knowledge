---
description: This is Tezos-flavored
---

# Token & currencies

Tokens are quite important when it comes to blockchains (surprising right?) and are what is used to pay bakers.

Several models exists.

### Account model

{% hint style="info" %}
Tezos, Ethereum
{% endhint %}

The **account model** is the one users are, usually, most familiar with since it's close to the bank account model:

* a client has an amount of money (a balance is assigned to an address in the blockchain)
* money is transferred in and out of the account under the bank's watch (the blockchain witnesses transactions and stores them in a ledger)

The balance is computed through add/sub operations from what is in the ledger.

{% content-ref url="account-model.md" %}
[account-model.md](account-model.md)
{% endcontent-ref %}

### UTXO

{% hint style="info" %}
Bitcoin
{% endhint %}

The **UTXO (Unspent Transaction Output) model** is radically different and less intuitive.

A transaction has:

* an input, which is a set of UTXOs along with the signatures of each owners
* an output, which is a set of UTXOs
* where the sum of the inputs in superior or equal to the sum of the output set

### Tickets

There are efforts to emulate the account and UTxO models in smart contracts in order to introduce more features, since the introduction of smart contracts and concepts of programmable money. The most widely emulated model is the account model. We will see later how Tezos enables emulation of UTxOs and further generalizes this concept with the introduction of tickets in its native smart contract language.

#### ERC-20 and FA2 <a href="#erc-20-and-fa2" id="erc-20-and-fa2"></a>

Ethereum Request for Comments-20, or ERC-20 for short, is ABI standard specifying required interface and semantics of a smart contract aiming to support operations of a token on the Ethereum blockchain. An ERC20 token user can expect the contract to mint, send, or refund the tokens when appropriate contract functions are called as defined in the standard. Similarly, Financial Application 2, or FA2 for short, is the analogue of ERC-20 to the Tezos blockchain. Both standards define a contract ABI that keeps a ledger in the contract storage and completes transactions by modifying account balances, effectively emulating the account model as described earlier.

Note, however, that the problem for the account model exacerbates for ERC-20 and FA2 tokens, since calls to the contracts need to be serialized sequentially. Transaction costs and latency has been a great problem for users of these tokens.

#### Tezos Tickets <a href="#tezos-tickets" id="tezos-tickets"></a>

Tezos tickets is a generalization of FA2 by capturing a subset of key characteristics of UTxOs, which is the capability to split and merge financial assets as well as the association of value. A Tezos ticket comprises of three key pieces of information: the creator of this ticket, coined as `ticketer`; the value associated to this ticket, which is used to emulate the value of a UTxO; and the associated data of a designated type to support token operations.

{% content-ref url="tickets.md" %}
[tickets.md](tickets.md)
{% endcontent-ref %}
