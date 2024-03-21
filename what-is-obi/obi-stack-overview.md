---
description: Overview of the five modular component groups of the Obi stack
---

# 🧩 Obi Stack Overview

<figure><img src="../.gitbook/assets/Obi Stack Dark.png" alt=""><figcaption></figcaption></figure>

The Obi stack has five component groups which can be swapped out or upgraded independently, without adversely affecting users.

### Transaction Flow

A typical transaction involves:

1. The user signs the transaction request with their Multikey threshold (or with a user-authorized [allowance](../glossary.md#spendlimit) account or easy [session key)](../glossary.md#sessionkey).
2. The user’s account [allows](../glossary.md#allow-list) or [blocks](../glossary.md#block-list) the transaction based on the current [abstraction rules](../smart-account-architecture/flex-accounts/), the simplest of which is, “Is the sender/signer the account [owner](../glossary.md#owner)?”
3. The Obi [signer](../glossary.md#signer) finalizes the signature with the network share, an irretrievable share which can only sign if step 2 allowed the transaction.
4. This final signed transaction is broadcast directly or via 4337 relay/paymaster.

Step 1 is local to the client application. Under most conditions, steps 2 and 3 are gasless queries. Step 4 fees are covered by the paymaster.

The user is unaware of most of this process. They sign a transaction – sometimes automatically in the case of easy restricted [session keys](../glossary.md#sessionkey) – and then can see the results on the destination network ([target chain](../glossary.md#target-chain)).
