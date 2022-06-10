# Sidechain deposits and withdrawals

The sidechain is connected to the main chain via a smart contract. The smart contract is responsible for three things:

1. Publishing a state root hash to the main chain every so often (say every 10 minutes)
2. Coordinating deposits (mainchain -> sidechain transfers)
3. Coordinating withdrawals (sidechain -> mainchain tranfers)

### The state root hash

The state root hash is a hash of the current state of the sidechain. It’s essentially the hash that corresponds to the root node of a merkle tree storing all the operations that happened on the sidechain. (It actually will probably be a patricia-merkle tree for performance reasons.) This is just a hash a few bytes big, so it can be cheaply stored on the main chain.

![](<../.gitbook/assets/image (6).png>)

(A merkle tree. Image released into the public domain [here](https://commons.wikimedia.org/wiki/File:Hash\_tree.png).)

Because of the nature of merkle-tree-like data structures, if you have a copy of the actual tree, you can prove the presence of a particular node in the tree to someone has the hash of any node that is an ancestor of your node.

**The smart contract regularly publishes the state root hash to the Tezos mainchain.** The state root hash is critical for facilitating withdrawals and for ensuring the security of the sidechain.

### Deposing (mainchain -> sidechain transfers)

#### Short version

Deposits work by making a transfer to the sidechain smart contract.

#### Long version

The smart contract facilitates deposits. You deposit by making a transfer to the sidechain smart contract (with a memo indicating the recipient’s sidechain wallet address).

The validators watch the main chain for such transfers, and obligate the current block producer to include a corresponding “deposit” transaction within a certain time. If the block producer doesn’t include the deposit, the validators should refuse to sign any block the block producer produces. (However, if the blocks somehow still get signed, they should still be validated and applied like normal.) This reduces the chances of censorship by a lone validator. Also, the block producer should be rotated at certain intervals, to further reduces the chance of censorship (see [properties of consensus algorithms](consensus/consensus-algorithm/)).

(The validators also need to refuse to sign any block that contains a deposit transaction they didn’t see happen on the main chain.)

This means that all the funds being managed on the sidechain are stored in the smart contract’s reserve.

### Withdrawing (sidechain ➜ mainchain transfers) <a href="#withdrawing-sidechain-mainchain-transfers" id="withdrawing-sidechain-mainchain-transfers"></a>

#### Short version

Withdrawals work by “burning” tokens on the sidechain, unlocking them to be withdrawn back to the mainchain.

#### Long version

Withdrawals work with a special `Transfer_to_tezos(wallet_address, amount_to_transfer)` operation on the sidechain. When the block producer gets the operation and writes it to the sidechain, they also include the current value of a global counter that is incremented every withdrawal. (This value is called the withdrawal handle, and is used later.)

Once the operation is written, the tokens are gone (as far as the sidechain is concerned). Actually withdrawing the tokens from the smart contract’s reserve happens by calling a function on the smart contract, and is only possible once a new state root hash is written.

To withdraw, you call the smart contract with a transfer handle, a wallet address, and a proof that a `Transfer_to_tezos` operation with that handle and wallet address was included in the state. The contract checks whether it has already processed a withdrawal using that handle, and if not it transfers the tokens to the wallet address.
