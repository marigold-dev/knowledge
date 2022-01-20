# Smart contracts

### How do Tezos smart contracts work internally? How contract addresses are derived?

**Answer** "You should read Tezos' code base which is the Single Source of Truth" (GA). Check out:

* [contract\_repr.ml](https://gitlab.com/tezos/tezos/-/blob/master/src/proto\_alpha/lib\_protocol/contract\_repr.ml)
* [apply.ml](https://gitlab.com/tezos/tezos/-/blob/master/src/proto\_alpha/lib\_protocol/apply.ml#L676)
* [contract\_storage.ml](https://gitlab.com/tezos/tezos/-/blob/master/src/proto\_alpha/lib\_protocol/contract\_storage.ml#L473)
