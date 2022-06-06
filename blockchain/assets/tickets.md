---
description: Extracted from blogpost
---

# Tickets

## Tickets for the dummies

In [Tezos](https://docs.nomadic-labs.com/nomadic-labs-knowledge-center/tickets-on-tezos), _tickets_ are a built-in generic data type, with strong invariants enforced by the type system. That's a mouthful and doesn't convey much without context. Tickets: what, why, how? What makes tickets tick?

So let's talk about tickets. And let's not assume any prior knowledge about linear types\[^linear], michelson primitives\[^michelsontickets] or the edo\[^edo]\[^edoligo] period, and let's take our time. First, let's give some context.

### What is a token?

In Tezos, there is a single built-in token: the XTZ. You can own it, you can send it to someone else, use it in contracts, and so on. It fuels every transaction, every smart contract execution, the tokenomics in general, and is all around essential to the blockchain. But let's not focus on that, and think of it as a token.

All other tokens are just an ~~illusion~~ abstraction: they are not something "in your wallet", _'cause they are whatever their contract says they are_. So much so that we talk about FAxx^fa2 or ERC-xxx\[^erc20]\[^erc721]\[^ercall] tokens, but those are in fact _contract standards_:

1. a generic interface,
2. a metadata standard,
3. some guidelines about invariants to enforce (what is expected).

Basically, a token is just a row in the ledger **of a particular contract** with standardized entrypoints that, hopefully, behave nicely. We'll call it... **the token contract** (_token SC_ for short).

If you want to trade a token, you need to interact with the token contract. The same goes for exchanges, marketplaces, dapps, etc., they all need to interact with the token contract. In fact, that is the whole point of standardizing token SCs: other contracts know how to interact with token contracts because the interface is defined in advance. Otherwise, an exchange would need to create new bridges for each and every new token; that is, write new code to interact with the token contract. This is not infeasable, but it is redundant, painful, confusing, has a bad UX, and above all silly.

You own a token _only_ in the sense that this particular contract has you, _on the record_, in the ledger. The token is not in your wallet, rather, your wallet asks the token contract which tokens you have. You don't send the token, you ask the token contract to change the corresponding lines in the ledger. The properties of a token are derived from the implementation of the contract: they are not intrinsic properties of a token, but depend on the code and execution of the smart contract. A token can not be duplicated, stolen or lost, only because the token contract enforces those properties.

#### Nitty gritty

Modeling a token by a single smart contract (or set of), that requires all actions on token to transit by the token contract adds a few complications **hidden behind ill-crafted vocabulary** (_e.g. "token in your wallet"_). Here are some examples.

The token contract is a **single point of failure**. This is not a _direct_ security concern, because the contract is public, and one can check that the semantic of the token is sound (no bugs), and won't change (no trickery). Also, hopefully, it's a much smaller trusted computing base than standard software (ignoring the blockchain protocol implementation). Of course "no change" can be a problem in itself, if the original contract is not perfect. To fix that, a bit of trickery can be added (e.g. wrappers), but then, either trust is required (which limits application), or a governance model of some kind (which adds complexity).

As everything done with the token goes through the token contract, the whole ecosystem in which the token moves is heavily centralized. What one can see as a simple transaction between users, exchanging tokens, actually involves multiple transactions between both users and the token contract: checks, transfer, and on top of that transactions between the users to orchestrate the transaction, dealing with failure for instance. Of course, a real use case can get way more tricky than a bunch of direct transactions as it could involve dApps, exchanges, or a number of more complex actions. On top of the complexity of UX, there is a direct **gas consumption overhead** inherent to centralization, that is completely obfuscated by the simple abstraction of a _"token in your wallet"_.

#### Comparison between XTZ and other tokens

To recap, let's compare\[^cryptovstoken] tokens based on smart contracts with the built-in XTZ on a few key points.

| Token        | Storage       | Trust^ownership^ | Trust^value^ | Gas OH | Built in |
| ------------ | ------------- | ---------------- | ------------ | ------ | -------- |
| XTZ          | decentralized | Protocol         | Protocol     | None   | Yes      |
| FAxxx Tokens | centralized   | Token SC         | Token SC     | High   | No       |

**Storage** and **Gas OverHead**\[^nftgas]\[^fa2gas] are self explanatory: a contract call will always be more costly (in space and time) than a simple XTZ transfer.

**Built in** means _has native support in protocol_: it's statically typed, has dedicated instructions, etc.

There are two components that require **trust**:

* ownership, _e.g._ the minimum we need to trust/examine/verify to convince ourselves that a token can not be stolen (obviously, trusting a SC entails also trusting the protocol)
* token value, _e.g_ we can convince ourselves that nobody can suddenly generate a large amount of a fungible token from thin air

### What is a ticket?

In short, tickets are **tokens in your wallets, for real this time**, and as [first-class citizens](https://en.wikipedia.org/wiki/First-class\_citizen) in smart contracts. They still need to be created by a contract, and need dApps to be useful, but they can be stored outside the contract that created them, be attached to any account, and be exchanged reliably just like XTZ (almost).

#### In more details

First of all, tickets are values of the smart contract language: `'a ticket` in [CameLIGO](https://ligolang.org/docs/reference/current-reference#tickets), or `ticket cty` in [Michelson](https://tezos.gitlab.io/michelson-reference/#type-ticket), is a **built-in generic data type** with specific constructors. A value of type `t ticket` for **any comparable type `t`**:

> * is a value manipulated directly by the contract;
> * can be send by contracts to other contracts;
> * can carry information.

Tickets have strong invariants **enforced by the type system** that give any ticket a semantic and a value shared by the whole blockchain:

> * it cannot be duplicated (for a specific definition of duplicated)
> * it cannot be altered (for a specific definition of altered)
> * it cannot be forged (for a specific definition of forged)

A contract trying to do any of those things **will be rejected by the type system**. Tickets are linear types\[^linear], and so are any type containing tickets. For instance, in [LIGO](https://ligolang.org/), a variable containing a ticket can only be used once. More on that later.

For now, let's just say that the type system **does not allow duplication**, which means that if a contract sends a ticket somewhere, **it cannot keep a copy**, and everybody, users and smart contracts alike, can rely on that. That is not to say that each ticket is completely unique: the original creator of the ticket can create any number of indistinguishable tickets, but nobody else can.

A ticket **cannot be forged**, in that it's impossible to create or alter a ticket and pretend that it comes from _somewhere else_. More on that later. For now, remember that it's always possible to _reliably_ know where a ticket comes from, and to trust nobody tampered with it.

Those properties together make tickets a natural choice for implementing tokens:

> * can be sent + cannot be duplicated = ownership can be transfered
> * shared semantic + arbitrary value = generic token

Moreover, they can change the way to implement dealings with tokens. As an example, there is never a need to check that a user owned a token : it is directly provided and can be manipulated directly.

Those safeguards are reinforced by Ticket Hardening features in [Ithaca2](https://tezos.gitlab.io/protocols/012\_ithaca.html#tickets-hardening-ongoing) and [Jakarata2](https://tezos.gitlab.io/protocols/013\_jakarta.html#tickets-hardening) proposals.

#### A ticket autopsy

The information contained in a ticket are:

* the **ticketer**: the address of the contract that created the ticket;
* a **payload**: a arbitrary value of an arbitrary comparable type, given when the ticket was created;
* and the **amount**: a natural number, representing the "volume" or "weight" of a ticket. When you `join` two compatible tickets of amount `x` and `y`, you get one of amount `x + y`. When you `split` in `x` and `y` a ticket of total volume/weight `x + y` you get two tickets, of amount `x` and `y`.

The **ticketer and payload are fixed** and will never change once a ticket is created. The amount won't change, _but_ one might want to say it does. Language gets tricky very quickly (because linear type are complicated): the amount only changes when tickets are split or joined. Strictly speaking, you get new tickets, with same creator and payload, so you didn't change the amount, rather, you transformed the tickets into new ones. In other words, you burned the ticket and created two new ones, keeping the original ticketer and payload information. Indeed, as mentioned previously, ticket are linear type values, therefore they are consumed when used.

The payload gives the ticket its **type**: a ticket with a payload of `1n` is a `nat ticket`, and so is one with payload `2n`. Payload type is not restricted to `nat` obviously, it can be any comparable type. The other two embedded pieces of information have a fixed type, respectively `address` and `nat`.

> **Comparable types** in Michelson: types for which the [`COMPARE`](https://tezos.gitlab.io/michelson-reference/#instr-COMPARE) primitive is defined\[^comparable], such as, basic types (`int`, `string`, `bytes`, but also `address`, `signature`, and more), and combinaisons thereof (`option <comparable type>` or `pair ...`).

#### Type vs Key

The generic **type** is `'a ticket` where `'a` refers to the type of the payload. But tickets of the same type can only be joined if they have the same ticketer and same payload _value_. Let's take `string ticket` as an example. `TICKET(bob, "toto", 42)`, `TICKET(jim, "toto", 42)` and `TICKET(bob, "otto", 42)` have the same type (`string ticket`) but are incompatible because they have different ticketers or different payloads.

> `TICKET(bob, "toto", 42) + TICKET(bob, "toto", 69) -> TICKET(bob, "toto", 111)`
>
> &#x20;`TICKET(jim, "toto", 42) + TICKET(bob, "toto", 69) -> ERROR`&#x20;
>
> `TICKET(bob, "otto", 42) + TICKET(bob, "toto", 69) -> ERROR`

Therefore, it's useful to think in terms of "ticket **key**"": a key being a ticketer and a payload _value_. There are several keys of `string ticket` (string being the type of the payload): one for each value of the payload and each ticketer, e.g. we can have `(bob, "toto")` or `(bob, "otto")` or `(jim, "toto")` tickets. In essence, tickets of the same key can always be joined, and splitting a ticket produces 2 tickets of the same key as the original. However, tickets of the same _type_ sometimes cannot be joined: they **must** have the same ticketer and payload value.

Please note that there is no way to change the ticketer nor the payload of a ticket: there simply exists no such primitive in the language. Since ticketer and payload are **fixed** at creation, **ticket key cannot be modified**.

As the ticketer never changes, even when splitting or joining, a contract has unambiguous control over tickets of all keys attributed to him; and everybody receiving a ticket knows where it came from originally. For example, to create a fungible token, one just has to write a _minting contract_, that creates tickets with a fixed payload. Those tickets can be sent to users, without loosing track of the total amount, and there is still no risk that people could _forge_ them (i.e. create new tickets without the ticketer's knowledge/consent).

### Linear types: indistinguisable from magic?

The invariants come from and have consequences on the way they are manipulated. Writing code can get tricky, but in a strongly-typed language you can only write correct programs, _this is the way_.

Rather than diving into the philosophical intricacies of linear types\[^linear], let's examine some practical consequences.

#### Variables: use it and lose it

An easy way to see linear types, is that a variable can only be used once. Once it's been used, it's lost. For instance, the following expression cannot be typed:

```ocaml
    let ticket = ... in
    let copy = ticket in
    ticket,copy
```

It throws the following errors:

> In **LIGO**:
>
> ```
> Warning: variable "ticket" cannot be used more than once. 
> ```
>
> >
>
> In **Michelson**:
>
> ```
> Ill typed contract: type ticket nat cannot be used here because
> it is not duplicable. Only duplicable types can be used with
> the DUP instruction and as view inputs and outputs.
> ```

That means that any function that takes a ticket as an argument needs to return it otherwise it's lost. The naive vision of `read_ticket` cannot work:

```ocaml
    let ticketer,payload,amount = read_ticket ticket in 
    ...
```

Otherwise, once read a ticket would be lost/burned forever. The actual function is:

```ocaml
    let (ticketer,(payload,amount)) , new_ticket = Tesoz.read_ticket ticket in
    ...
```

#### Constructors

The **only constructors**, the only ways to obtain a new ticket, are `create_ticket`, `split_ticket` and `join_tickets`.

In LIGO\[^ligotickets] they have the following signatures

```ocaml
val create_ticket : 'value -> nat -> 'value ticket
val split_ticket : 'value ticket -> nat * nat -> ('value ticket * 'value ticket) option
val join_tickets : 'value ticket * 'value ticket -> ('value ticket) option
```

*   `create_ticket`: returns a completely new ticket _(please note that types can be infered, and only indicated here to emphasize the difference between type and key)_

    ```ocaml
        let new_ticket : string ticket = Tesoz.create_ticket "some payload" 42n in
        ...
    ```
*   `split_ticket`: transforms a ticket into new tickets of _same key_

    ```ocaml
        let old_ticket  = Tesoz.create_ticket "some payload" 42n in
        let opt  = Tesoz.split_ticket old_ticket (12n,30n) in
        let ticket_12, ticket_30   = Option.unopt opt in
        ...
    ```
*   `join_tickets`: transforms two tickets of same key into a new ticket of that key

    ```ocaml
        let ticket_12  = Tesoz.create_ticket "some payload" 12n in
        let ticket_30  = Tesoz.create_ticket "some payload" 30n in
        let opt  = Tesoz.join_tickets (ticket_12,ticket_30) in
        let ticket_42 = Option.unopt opt in
        ...
    ```

#### Finding in storage

If tickets are in a `map`, then it is not possible to `find` a ticket and leave it in the map. If you access it, you must delete it from the map. Use `get_and_update`\[^getandupdate], with `None` as new value, to obtain the searched value and the updated map in one fell swoop:

```ocaml
    let ticket,store_without_ticket = 
        Map.get_and_update addr (None : silly option) store in 
    ...
```

#### Updating in storage

While updating, be careful with `get_and_update`, if the new value is `Some ticket` the value returned for the ticket is `None`, otherwise, obvious duplication:

```ocaml
    let _ticket,store = Map.get_and_update addr (Some silly) store in 
    ...
```

The value `_ticket` returned by the function is actually `None`.

Remark: `update` can be used instead of `get_and_update` contrary to what the doc\[^getandupdate] seems to imply.

#### Views

Views\[^view1] are a built in mechanisme to provide `readonly` synchronous access to a smart contract. Views are a bit similar to endpoints, in that they take values of type `parameter * storage`, but rather than returning `operation list * storage`, views can return any value, but have no effect on the storage.

```ocaml
    let main (action,store : sc_parameter * storage) : operation list * storage = ... 
    let view_1 (parameter,store : view_parameter * storage) : view_return_value = ...
```

Parameters (`view_parameter`) and return values (`view_return_value`) can be of any type but `big_map`, `sapling_state`, `operation`, and `ticket`\[^view2].

### Comparison again: XTZ, tokens, tickets

Let's reexamine the comparison between FA tokens and XTZ, and add tickets into the mix.

| Token        | Storage         | Trust^ownership^ | Trust^value^ | Gas OH  | Built in |
| ------------ | --------------- | ---------------- | ------------ | ------- | -------- |
| XTZ          | decentralized   | Protocol         | Protocol     | None    | Yes      |
| FAxxx Tokens | centralized     | Token SC         | Token SC     | High    | No       |
| Tickets      | +-decentralized | Protocol+-SC     | SC           | Depends | Yes      |

**Storage** of tickets _can_ be decentralised, as tickets can be transfered between contracts. Moreover, creation is completely centralized, so it's still possible to store all tickets of one key in one place: just don't distribute them and hold a ledger.

Regarding **trust**, if we make the same distinction between ownership and value:

* ownership trust is simple, it's only the contract storing the ticket that needs to be trusted;
* value trust depends on the usage of the tickets, but in any case it will down to the correctness of the contracts that make use of the ticket.

**Gas OverHead** again depends on the chosen architecture for a particular use case. The less centralized, the less gas overhead. There will be michelson executed to manipulate the tickets, so there will be gas consumption, but it can be _way_ less. But again, will depend on implementation and architecture.

**Limitation**: As of May 2022, tickets can only be hold by originated addresses (a.k.a. smart contract addresses) but this limitation should be removed in a future proposal. Tezos layers 2 like TORUs, SCORUs, DEKU, or Chusai (coming soon) can already hold tickets for implicit accounts (tz1xx, tz2xx, tz4xx).

### A ticket to Tezos Layer 2

When you take a look at Layer 2 ecosystems in several blockchains you are quicky stuck by having to bridge main chain tokens to several layer 2 tokens. Passing assets between L2s is even worse.

Having tickets as first class citizen of all Tezos Layer 2 provides a lot of simplicity and avoid lot of useless fees for locking/unlocking in the main chain. It allows all Layer 2 to be "token agnostic" and manipulate tickets regardless of their origin. As long as a token is implemented using tickets, it is supported by all Layer 2 implementing tickets, for free, without any dedicated infrastructure. If it's not, a simple smart contract providing tickets for tokens (that it stores in a vault) is enough.

Imagine:

1. You could have a smart contract that mint a [cTez](https://ctez.app/) ticket for you, vaulting cTez against this ticket.
2. You will be able to deposit this ticket to a TORU rollup,
3. Then do a transaction of a specific amount,
4. Then withdraw the remaining amount of the ticket to Tezos,
5. Then deposit to DEKU Sidechain,
6. Then use the ticket with a smart contract,
7. Then withdraw to Tezos and finally burn your ticket from the initial ticketer against the remaining cTez.

**You used in Tezos, TORU and DEKU the same ticket!**

### Ways to think about tickets

To conclude, here are a few examples of (useful?) ways to think about tickets: to reason about the semantic of a contract, to experiment with new ways to implement existing functionality, to communicate concepts.

* An unforgeable and traceable piece of data
* Cash, it's in your pocket but it's not forgeable (heh)
* Keys to unlock functionalities
* A way for the blockchain to natively support any custom tokens
* Tokens working as intended
* ~~A synchronization artefact to deal with concurrency~~
* A tool to write data in the global ledger: the place it's stored in doesn't change the meaning/value of the ticket
* Data that can be reasoned on at the level of the whole chain, not merely at the level of the contract
* A generic Smart Contract data type with very strong invariants

### References

Original blogpost : [Tickets for the dummies](https://www.marigold.dev/post/tickets-for-dummies)

Proposal for strengthening ticket handling in the Tezos Protocol https://hackmd.io/lutm\_5JNRVW-nNFSFkCXLQ?view

ticket Hardening in [Ithaca2](https://tezos.gitlab.io/protocols/012\_ithaca.html#tickets-hardening-ongoing) and [Jakarata2](https://tezos.gitlab.io/protocols/013\_jakarta.html#tickets-hardening) proposals.

Tickets For More Efficient & Secure DeFi https://xtz.news/governance-news/tezos-tickets-amendment-upgrade/

Tickets https://docs.nomadic-labs.com/nomadic-labs-knowledge-center/tickets-on-tezos

\[^cryptovstoken]: Comparisons between coins and tokens \
https://developers.rsk.co/guides/get-crypto-on-rsk/cryptocurrency-vs-token/ https://economictimes.indiatimes.com/markets/cryptocurrency/crypto-class-difference-between-crypto-coin-token/articleshow/88947666.cms \
https://www.wired.com/story/nfts-dont-work-the-way-you-think-they-do/

\[^fa2gas]: FA2 gas consumption tracking \
https://better-call.dev/stats/mainnet/fa2

\[^nftgas]: NFT Gas fee https://learn.bybit.com/nft/nft-gas-fee-explained/ https://allthings.how/what-are-gas-fees-for-nfts/

https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-7/tzip-7.md

\[^fa2]: FA2 \
https://tezos.b9lab.com/fa2\
https://gitlab.com/tezos/tzip/-/blob/master/proposals/tzip-12/tzip-12.md

\[^erc20]: ERC-20: Token standard \
https://ethereum.org/en/developers/docs/standards/tokens/erc-20/

\[^erc721]: ERC-721: Non fungible token standard https://ethereum.org/en/developers/docs/standards/tokens/erc-721/

\[^ercall]: ERC: \
https://yos.io/2019/04/14/erc-standards-you-should-know-about/ http://blockchainers.org/index.php/2018/02/08/token-erc-comparison-for-fungible-tokens/

\[^linear]: Linear types https://en.wikipedia.org/wiki/Substructural\_type\_system#:\~:text=it%20was%20introduced.-,Linear%20type%20systems,transitioned%20to%20a%20different%20state.

\[^edo]:MR edo doc in ligo \
https://gitlab.com/ligolang/ligo/-/merge\_requests/929

First-class citizen definition: \
https://en.wikipedia.org/wiki/First-class\_citizen

\[^edoligo]:How to use tickets with Ligo \
https://news.ecadlabs.com/how-to-use-tickets-with-ligo-e773422644b7 https://medium.com/tqtezos/tickets-on-tezos-part-1-a7cad8cc71cd

\[^michelsontickets]: Tickets in Michelson \
https://tezos.gitlab.io/active/michelson.html#operations-on-tickets

\[^comparable]: Comparable types, see - [michelson doc: generic comparaison](https://tezos.gitlab.io/active/michelson.html#generic-comparison) - [michelson doc: grammar](https://tezos.gitlab.io/active/michelson.html#full-grammar)&#x20;

```
<comparable type> ::=
  | unit
  | never
  | bool
  | int
  | nat
  | string
  | chain_id
  | bytes
  | mutez
  | key_hash
  | key
  | signature
  | timestamp
  | address
  | option <comparable type>
  | or <comparable type> <comparable type>
  | pair <comparable type> <comparable type> ...
```



\[^view2]: Views (Ligo) \
https://ligolang.org/docs/protocol/hangzhou/#on-chain-views \[^view1]: \
Views (michelson) \
https://tezos.gitlab.io/active/michelson.html#operations-on-views \
\
\[^ligotickets]: tickets in Ligo (camligo): \
https://ligolang.org/docs/reference/current-reference/#tickets \
\
\[^getandupdate]: get\_and\_update: \
https://ligolang.org/docs/reference/current-reference#linearity
