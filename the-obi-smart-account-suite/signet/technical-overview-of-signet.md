# Technical Overview of Signet

Signet works by allowing account abstraction logic to be applied gaslessly and immediately at the **signing** step of the transaction flow, rather than at the target chain transaction step. Account abstraction rules are checked by the smart account without adding additional target chain execution cost or additional latency. If an active account abstraction rule is matched, including but not limited to these examples:

* the actor is the account owner, using multi-factor authentication
* the actor is an active session key ([anti-cheat-sign-in](../anti-cheat-sign-in/ "mention"))
* the actor has an active budget ([party-members](../party-members/ "mention"))
* the actor is an inheritor, and inheritance is active ([extra-life.md](../extra-life.md "mention"))

then the transaction is signed and broadcasted to the destination chain (e.g. Ethereum or Cosmos Hub).

From Ethereum’s (or Cosmos Hub's) perspective in this example, an [EOA](../../glossary.md#eoa) private key signed a simple transaction. However, account abstraction rules were applied on a different layer, saving gas and enabling functionality which is not yet natively available on Ethereum.

From the user’s perspective, they simply submit an Ethereum (or Cosmos Hub) transaction in a dapp, using a normal address and normal Ethereum/Cosmos Hub assets. The smart account layer’s participation as account abstraction rule enforcer does not need to be visible to the user.

### Version 1

A private key is created with shares $k\_1$ … $k\_4$, in a 2-of-4 setup. Factors of the Multikey are used to encrypt shares $k\_1$, $k\_2$, and $k\_3$, which are stored encrypted both on user device and on remote server.

Meanwhile, $k\_4$ is stored with a **share signer (Signet) contract** on a network that supports private data and computation. Currently, Secret Network is used for this purpose. In the future, a bespoke chain can be used, with Secret and other networks as backups.

This key is not directly retrievable, but it can be used to sign or to help rotate shares.

The Signet smart contract knows to ask its associated User Account if the transaction is authorized before signing with signature $sig\_{k4}$. This requires any of the following:

1. User Account has a contract presence on the share signer's network.
2. The Signet can query the account via ICQ (interchain query), with ownership proven by a signed message to exclude malicious relayer behavior.

This covers the following cases:

* Common usage: The user processes a transaction via their User Account. The account returns $sig\_{k4}$ (fees are appended to the final transaction, either by the application or by the contracts themselves). The user then can calculate $sig\_{k1}$ (or $sig\_{k2}$ or $sig\_{k3}$) and submitted the final signed transaction to the end chain: Bitcoin, Lightning, Ethereum, Optimism, Neutron, Atom, etc.
* Common recovery: The user loses some keys. Using the available shares, they rotate to new $k\_1...k\_4$. The Secret Network $k\_4$ must now be replaced, and the other keys are re-encrypted and re-stored locally and remotely. This can also apply if keys are stolen or if SGX is compromised.

### **Version 2**

The second version of Obi Passport adds an **additional network**. This provides additional resilience against network downtime or failure or trusted execution environment exploits, even in the inheritance case. This second network holds a new $k\_{5}$ and is able to provide $sig\_{k5}$. Unlike Version 1, there are 2 network shares available.
