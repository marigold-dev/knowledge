# Table of contents

* [Marigold Knowledge](README.md)
* [💸 Assets](assets.md)

## 🤝 Consensus

* [Consensus algorithm](consensus/consensus-algorithm/README.md)
  * [What consensus is and isn't](consensus/consensus-algorithm/need-for-consensus.md)
  * [Properties of consensus](consensus/consensus-algorithm/picking-a-consensus-algorithm/README.md)
    * [Liveness & Safety properties](consensus/consensus-algorithm/picking-a-consensus-algorithm/liveness-and-safety-properties.md)
    * [Security/Recovery properties](consensus/consensus-algorithm/picking-a-consensus-algorithm/security-recovery-properties.md)
    * [Network properties](consensus/consensus-algorithm/picking-a-consensus-algorithm/network-properties.md)
* [⚙ Consensus families](consensus/consensus-families/README.md)
  * [Proof-of-Work (PoW)](consensus/consensus-families/proof-of-work-pow/README.md)
    * [Delayed Proof-of-Work](consensus/consensus-families/proof-of-work-pow/delayed-proof-of-work.md)
    * [Delegated Proof-of-Work](consensus/consensus-families/proof-of-work-pow/delegated-proof-of-work.md)
  * [Proof-of-Stake (PoS)](consensus/consensus-families/proof-of-stake-pos.md)
  * [Proof-of-Weight (PoWe)](consensus/consensus-families/proof-of-weight-powe.md)
  * [Byzantine Fault Tolerance (BFT)](consensus/consensus-families/practical-byzantine-fault-tolerance-pbft.md)
  * [Proof-of-Authority (PoA)](consensus/consensus-families/proof-of-authority-poa.md)
  * [Snow protocol](consensus/consensus-families/snow-protocol.md)
  * [Proof-of-History (PoH)](consensus/consensus-families/proof-of-history-poh.md)
  * [Proof of Capacity/Proof of Space](consensus/consensus-families/proof-of-capacity-proof-of-space.md)
* [🔬 Details on algorithms](consensus/details-on-algorithms/README.md)
  * [Algorand](consensus/details-on-algorithms/algorand.md)
  * [Avalanche](consensus/details-on-algorithms/avalanche.md)
  * [Ripple](consensus/details-on-algorithms/ripple.md)
  * [Tendermint](consensus/details-on-algorithms/tendermint/README.md)
    * [Getting in sync](consensus/details-on-algorithms/tendermint/getting-in-sync.md)
    * [Scenarios](consensus/details-on-algorithms/tendermint/scenarios/README.md)
      * [Normal scenario](consensus/details-on-algorithms/tendermint/scenarios/normal-scenario.md)
      * [Net split](consensus/details-on-algorithms/tendermint/scenarios/net-split.md)
    * [Locking rules](consensus/details-on-algorithms/tendermint/locking-rules.md)

## 📜 Rollups

* [Optimistic Rollups (ORU)](rollups/oru-for-noobs/README.md)
  * [Tezos](rollups/oru-for-noobs/tezos/README.md)
    * [TORU](rollups/oru-for-noobs/tezos/toru.md)
    * [MORU](rollups/oru-for-noobs/tezos/moru.md)
  * [Ethereum](rollups/oru-for-noobs/ethereum/README.md)
    * [Optimism](rollups/oru-for-noobs/ethereum/optimism.md)
    * [Arbitrum](rollups/oru-for-noobs/ethereum/arbitrum.md)
* [Zero-Knowledge (zk-rollups)](rollups/zero-knowledge-zk-rollups/README.md)
  * [SNARKs](rollups/zero-knowledge-zk-rollups/snarks.md)
  * [STARKs](rollups/zero-knowledge-zk-rollups/starks.md)

## ⛓ Sidechain

* [Deku for the noobs](sidechain/sidechain-for-noobs.md)
* [Sidechain deposits and withdrawals](sidechain/sidechain-deposits-and-withdrawals.md)
* [References](sidechain/references.md)
* [Notes on PRs](sidechain/notes-on-prs.md)

## ⚡ Other Layer 2

* [State Channels](other-layer-2/state-channels/README.md)
  * [Lightning Network](other-layer-2/state-channels/lightning-network.md)
  * [Raiden Network](other-layer-2/state-channels/raiden-network.md)

***

* [👾 Dapps](dapps/README.md)
  * [🆒 Marigold Trainings](dapps/marigold-trainings.md)
* [🔠 Vocabulary](vocabulary/README.md)
  * [Aggregation (transaction)](vocabulary/aggregation-transaction.md)
  * [Baker](vocabulary/baker.md)
  * [Cryptoeconomics](vocabulary/cryptoeconomics.md)
  * [Distributed Denied of Service](vocabulary/distributed-denied-of-service.md)
  * [Endorser](vocabulary/endorser.md)
  * [Finality/Instant finality](vocabulary/finality-instant-finality.md)
  * [Forking](vocabulary/forking.md)
  * [Leader/Leaderless](vocabulary/leader-leaderless.md)
  * [Network partition/Synchronicity](vocabulary/network-partion-synchronicity.md)
  * [Overlay network](vocabulary/overlay-network.md)
  * [Permissioned](vocabulary/permissioned.md)
  * [Plagiarism](vocabulary/plagiarism.md)
  * [Signer](vocabulary/signer.md)
  * [Sharding](vocabulary/sharding.md)
  * [Subjectivity](vocabulary/subjectivity.md)
  * [Sybil attacks](vocabulary/sybil-attacks.md)
  * [Validator](vocabulary/validator.md)

## 🧮 FAQ

* [Attacks](faq/attacks.md)
* [Benchmark](faq/benchmark/README.md)
  * [Compare 2 snoop benchmarks](faq/benchmark/compare-2-snoop-benchmarks.md)
* [🐫 OCaml stuff](faq/ocaml-stuff/README.md)
  * [🆒 Marigold Trainings](faq/ocaml-stuff/marigold-trainings.md)
  * [Learn OCaml 🐫](faq/ocaml-stuff/learn-ocaml.md)
  * [Coding style](faq/ocaml-stuff/coding-style.md)
  * [\_\[> \`And\_clear\]](faq/ocaml-stuff/\_-greater-than-and\_clear.md)
  * [!'a t](faq/ocaml-stuff/a-t.md)
  * [Switching types](faq/ocaml-stuff/switching-types.md)
* [Tezos-related stuff](faq/tezos-related-stuff/README.md)
  * [Baking](faq/tezos-related-stuff/baking.md)
  * [FA2 NFTs vs ticket-based NFTs](faq/tezos-related-stuff/fa2-nfts-vs-ticket-based-nfts.md)
  * [Handling forks](faq/tezos-related-stuff/handling-forks.md)
  * [Hashing](faq/tezos-related-stuff/hashing.md)
  * [Plagiarism](faq/tezos-related-stuff/plagiarism.md)
  * [Serialization](faq/tezos-related-stuff/serialization.md)
  * [Smart contracts](faq/tezos-related-stuff/smart-contracts.md)
