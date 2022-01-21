# ⚙ Consensus families



| Algorithm | Proof of Work (PoW)                                         | Proof of Stake (PoS)                                                             | Delayed Proof of Work                                                       | Delegated Proof of Work                                                    | Proof of Authority       | Proof of Weight                            | Practical Byzantine Fault Tolerance        | Federated Byzantine Agreement (FBA)  |
| --------- | ----------------------------------------------------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------ | ------------------------------------------ | ------------------------------------------ | ------------------------------------ |
| Type      | competitive algorithm                                       | competitive algorithm                                                            | collaborative algorithm                                                     | collaborative algorithm                                                    | collaborative algorithm  | competitive                                | byzantine                                  | byzantine                            |
| Pros      | tested and steady                                           | resource efficient, attack very expensive, not susceptible to economies of scale | resource efficient, increased security (?), adds value to other blockchains | resource efficient, fast                                                   | resource efficient, fast | resource efficient, customisable, scalable | fast, scalable                             | fast, scalable, low transaction cost |
| Cons      | slow, resource consuming, susceptible to economies of scale | nothing-at-stake problem                                                         | only blockchains using PoW or PoS can use the consensus                     | a bit centralized, high stakes participants can vote themselves validators | a bit centralized        | incentivization hard                       | centralized/permissions/known participants | permissioned network                 |
| Used by   | Bitcoin, Ethereum (orig.), Dogecoin                         | Ethereum (fut.), Peercoin                                                        | Komodo                                                                      | Bitshares, Steemit                                                         | VeChain                  | Algorand                                   |                                            | Ripple, Stellar                      |