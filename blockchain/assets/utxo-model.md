# UTXO model

{% hint style="info" %}
The **UTXO (Unspent Transaction Output) model** is radically different and less intuitive.

A transaction has:

* an input, which is a set of UTXOs along with the signatures of each owners
* an output, which is a set of UTXOs
* where the sum of the inputs in superior or equal to the sum of the output set
{% endhint %}

### Core characteristics

* tokens are unique
* hard to make it work with smart contracts
* token movements are a 100% transparent
* since it doesn't cost much to create a new account for each new transaction, there is no breach of privacy

### About

Input UTXOs are consumed and output UTXOs are minted.

UTxO model introduces difficulties in making economic transaction when transaction fee is a concern. It is generally not free to include more UTxOs as each additional UTxO leads to a larger transaction body implying a higher transaction fee. Many heuristics are developed to select UTxOs strategically in order to lower your transaction fee, but lowest fee is not guaranteed. In addition, transaction could produce UTxOs of extremelly low value such that inclusion of such UTxOs will incur transaction costs exceeding their own values. Such UTxOs are called dusts and they are considered practically lost forever.
