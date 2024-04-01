# Draft Signet Whitepaper

Signet works by allowing account abstraction logic to be applied gaslessly and immediately at the **signing** step of the transaction flow, rather than at the target chain transaction step. Account abstraction rules are checked by the smart account without adding additional target chain execution cost or additional latency. If an active account abstraction rule is matched, including but not limited to these examples:

* the actor is the account owner, using multi-factor authentication
* the actor is an active session key ([safe-sign-in](../safe-sign-in/ "mention"))
* the actor has an active budget ([party-members](../party-members/ "mention"))
* the actor is an inheritor, and inheritance is active ([extra-life.md](../extra-life.md "mention"))

then the transaction signature is finalized and can broadcasted to the destination chain (e.g. Ethereum or Cosmos Hub).

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-31 at 5.01.01 PM.png" alt=""><figcaption></figcaption></figure>

From the user’s perspective, they simply submit an Ethereum (or Cosmos Hub) transaction in a dapp, using a normal address and normal Ethereum/Cosmos Hub assets. The smart account layer’s participation as account abstraction rule enforcer does not need to be visible to the user.

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-31 at 5.01.41 PM.png" alt=""><figcaption></figcaption></figure>

From Ethereum’s (or Cosmos Hub's) perspective in this example, an [EOA](../../glossary.md#eoa) private key signed a simple transaction. However, account abstraction rules were applied on a different layer, saving gas and enabling functionality which is not yet natively available on Ethereum.

Read more in the draft [Signet Whitepaper](https://docs.google.com/document/d/1Tdc8-2bZ2DdNX\_oVD1h\_mIretjDSKZHny07W4BcG4xM/):

{% embed url="https://docs.google.com/document/d/1Tdc8-2bZ2DdNX_oVD1h_mIretjDSKZHny07W4BcG4xM/" %}
