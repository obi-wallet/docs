---
description: Overview of the modular component groups of the Obi stack
---

# 🧩 Obi Stack Overview

<figure><img src="../.gitbook/assets/Obi Stack Dark.png" alt=""><figcaption></figcaption></figure>

The Obi stack has multiple component groups which can be swapped out or upgraded independently, without adversely affecting users.

### Depending on your experience with various technologies, you may find it helpful to think of Obi's core technology as:

🧩 a **modular accounts blockchain** which quietly integrates with all chains, without requiring backend integration work or cross-chain messaging

🛠️ a robust **all-chain permission system,** allowing existing use cases such as [spend limits](../glossary.md#spendlimit), [inheritance](../glossary.md#inheritance), subscriptions, budgets, [session keys](../glossary.md#sessionkey), [gasless](../glossary.md#gasless-mpc) [MEV-shielded](../glossary.md#mev-shielded-intent) cross-chain [intents](../glossary.md#intent), and purpose-bound "worker addresses" – in addition to new use cases not yet deployed

🔑 a near-zero-latency gasless **MPC helper network** – like a Ledger hardware wallet adding to your security, but as a network – where even nodes, downtime, or secure hardware vulnerabilities do not jeopardize user funds or access

🔒 a **security network** bringing standardization to user accounts across blockchains

😄 an all-chain, seamless, recoverable, hack-resistant **user account experience**

### Transaction Flow

A typical transaction involves:

1. The user signs the transaction request with their Multikey threshold (or with a user-authorized [allowance](../glossary.md#spendlimit) account or easy [session key)](../glossary.md#sessionkey).
2. The user’s account [allows](../glossary.md#allow-list) or [blocks](../glossary.md#block-list) the transaction based on the current [abstraction rules](broken-reference), the simplest of which is, “Is the sender/signer the account [owner](../glossary.md#owner)?”
3. The Obi [signer](../glossary.md#signer) finalizes the signature with the network share, an irretrievable share which can only sign if step 2 allowed the transaction.
4. This final signed transaction is broadcast directly or via 4337 relay/paymaster.

Step 1 is local to the client application. Under most conditions, steps 2 and 3 are gasless queries. Step 4 fees are covered by the paymaster.

The user is unaware of most of this process. They sign a transaction – sometimes automatically in the case of easy restricted [session keys](../glossary.md#sessionkey) – and then can see the results on the destination network ([target chain](../glossary.md#target-chain)).
