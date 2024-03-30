---
description: One account for ALL chains. No extra gas, no latency, no hassle.
---

# 🔍 Signet

Obi Signet enables **multi-chain account abstraction** for the first time: with one secure account and one flexible set of rules, users can manage addresses, apps, and assets on any chains they wish.

With Signet, Obi Accounts on any chain can control addresses on any other chain, even without IBC connection. This can even allow an Obi extension or app to pretend to be any other wallet extension.

A transaction for a destination chain can be submitted by an actor to an Obi account, regardless of the smart account’s home chain. Account abstraction rules (see [party-members](../party-members/ "mention")) are checked by the smart account. If an active rule is matched, including but not limited to these examples:

* the actor is the account owner, using multi-factor authentication
* the actor is an active session key
* the actor has an active budget

then the transaction is signed and broadcasted to the destination chain (e.g. Ethereum or Cosmos Hub). In many cases, this can be resolved via query so that there is no added block time delay or fee on the account home chain.

From Ethereum’s (or Cosmos Hub's) perspective in this example, an EOA private key signed a simple transaction. However, account abstraction rules were applied on a different layer, saving gas and enabling functionality which is not yet natively available on Ethereum.

From the user’s perspective, they simply submit an Ethereum (or Cosmos Hub) transaction in a dapp, using a normal address and normal Ethereum/Cosmos Hub assets. The smart account layer’s participation as account abstraction rule enforcer does not need to be visible to the user.
