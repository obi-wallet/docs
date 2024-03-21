# Obi Passport

Obi Passport enables **multi-chain account abstraction** for the first time: with one secure account and one flexible set of rules, users can manage addresses, apps, and assets on any chains they wish.

With Obi Passport, Obi Accounts on any chain can control addresses on any other chain, even without IBC connection. This can even allow an Obi extension or app to pretend to be any other wallet extension.

A transaction for a destination chain can be submitted by an actor to an Obi account, regardless of the smart account’s home chain. Account abstraction rules (see [Flex Accounts](https://www.notion.so/Flex-Accounts-5fb118a1929d452f80246c066c3eef7b?pvs=21)) are checked by the smart account. If an active rule is matched, including but not limited to these examples:

* the actor is the account owner, using multi-factor authentication
* the actor is an active session key
* the actor has an active budget

then the transaction is signed and broadcasted to the destination chain (e.g. Ethereum or Neutron). In many cases, this can be resolved via query so that there is no added block time delay or fee on the account home chain.

From Ethereum’s (or Neutron's) perspective in this example, an EOA private key signed a simple transaction. However, account abstraction rules were applied on a different layer, saving gas and enabling functionality which is not yet natively available on Ethereum.

From the user’s perspective, they simply submit an Ethereum (or Neutron) transaction in a dapp, using a normal address and normal Ethereum/Neutron assets. The smart account layer’s participation as account abstraction rule enforcer does not need to be visible to the user.

#### Version 1

A private key is created with shares $k\_1$ … $k\_4$, in a 2-of-4 setup. Factors of the Multikey are used to encrypt shares $k\_1$, $k\_2$, and $k\_3$, which are stored encrypted both on user device and on remote server.

Meanwhile, $k\_4$ is stored with a **share signer contract** on a network that supports private data and computation. Currently, Secret Network is used for this purpose. In the future, a bespoke chain can be used, with Secret and other networks as backups.

This key is not directly retrievable, but it can be used to sign or to help rotate shares.

The share signer smart contract knows to ask its associated User Account if the transaction is authorized before signing with signature $sig\_{k4}$. This requires any of the following:

1. User Account has a contract presence on the share signer's network.
2. The Secret Signer can query the account via ICQ (interchain query), with ownership proven by a signed message to exclude malicious relayer behavior.

This covers the following cases:

* Common usage: The user processes a transaction via their User Account. The account returns $sig\_{k4}$ (fees are appended to the final transaction, either by the application or by the contracts themselves). The user then can calculate $sig\_{k1}$ (or $sig\_{k2}$ or $sig\_{k3}$) and submitted the final signed transaction to the end chain: Bitcoin, Lightning, Ethereum, Optimism, Neutron, Atom, etc.
* Common recovery: The user loses some keys. Using the available shares, they rotate to new $k\_1...k\_4$. The Secret Network $k\_4$ must now be replaced, and the other keys are re-encrypted and re-stored locally and remotely. This can also apply if keys are stolen or if SGX is compromised.

#### **Version 2**

The second version of Obi Passport adds an **additional network** which does not rely on the same secure hardware. This provides additional resilience against network downtime or failure or trusted execution environment exploits, even in the inheritance case. This second network holds a new $k\_{5}$ and is able to provide $sig\_{k5}$. Unlike Version 1, there are 2 network shares available.

Additionally, to enable inheritance of Obi Passport keys, encrypted versions of $k\_1$ are stored in contract state (on both networks) and are retrievable, but are each encrypted by one of the beneficiaries’ pubkeys, or by the user’s pubkey. When any beneficiary is added later, $k\_1$ will also be stored for them, encrypted by the new beneficiary’s pubkey.

Network copies of $k\_1$ encrypted by beneficiary pubkeys are not immediately retrievable: they will be provided to beneficiaries only if the inheritance dormancy period has passed.

In version 2, the following additional cases are covered:

* Emergency recovery: SGX or the share signer's home network suffers a negative event which compromises $k\_4$ or renders it unavailable for use. The alternate network can be used.
* The user is incapacitated or killed. After the dormancy period passes, a beneficiary can now:

1. Retrieve $k\_1$ and decrypt it by the private key.
2. Request the share signer to produce $sig\_{k4}$, or the alternate network to produce $sig\_{k5}$, which are now allowed since inheritance has been activated.
