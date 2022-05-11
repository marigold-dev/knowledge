# Account model

{% hint style="info" %}
The **account model** is the one users are, usually, most familiar with since it's close to the bank account model:

* a client has an amount of money (a balance is assigned to an address in the blockchain)
* money is transferred in and out of the account under the bank's watch (the blockchain witnesses transactions and stores them in a ledger)

The balance is computed through add/sub operations from what is in the ledger.
{% endhint %}

### Core characteristic

* account balances need to be stored in state
* intuitive
* light clients can request the last state and retrieve information easily
* since adding a new account costs (since it will be stored), a given account will be used several times by its user which can lead to transaction tracking and some level of breach of privacy
* transactions must have a nonce (to avoid double-spend)

### About

The account model works by using a **dedicated ledger**.

At each new validated block (= chain height), the included transactions contained in it are applied which triggers changes in balances of several accounts in the network. Those new balances are recorded and the state has to be altered.

Transactions moving funds from the source account needs to **prove** that the source account has sufficient balance. To prove such, the account owner typically needs to also attach the latest state of their account on top of various transaction details. This proof may vary between blockchain specifications, but it usually points to _the_ last outbound transaction from this account, also known as the **account nonce**.



| Block height | Included transactions                                                                                    | State                                                                                                                                                                   |
| ------------ | -------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| $$n$$        | $$A \xrightarrow{10}  B$$                                                                                | <p>A: <span class="math">B(A) - 10</span><br>B: <span class="math">B(B) + 10</span></p>                                                                                 |
| $$n + 1$$    | <p> <span class="math">A \xrightarrow{2} B</span><br> <span class="math">C \xrightarrow{20} B</span></p> | <p>A: <span class="math">B(A) - 2</span><br>B: <span class="math">B(B) + 2 + 20</span><br>C: <span class="math">B(C) - 20</span></p>                                    |
| $$n + 2$$    | <p><span class="math">A \xrightarrow{2} C</span><br><span class="math">A \xrightarrow{1} D</span></p>    | <p>A: <span class="math">B(A) - 2 - 1</span><br>B: <span class="math">B(B)</span><br>C: <span class="math">B(C) + 2</span><br>D: <span class="math">B(D) + 1</span></p> |
| $$n + 3$$    | $$C \xrightarrow{5} A$$                                                                                  | <p>A: <span class="math">B(A) + 5</span><br>B: <span class="math">B(B)</span><br>C: <span class="math">B(C) - 5</span><br>D: <span class="math">B(D)</span></p>         |

Typically, transactions that affect the same account must be applied in order and sequentially.



