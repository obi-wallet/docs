# 🥇 Obi's Unique Advantages

Several Obi concepts such as account abstraction, multi-party threshold signing, seedless Passkey experience, and all-chain unified user experience are being deployed by other solutions. Obi's architecture – with components perpetually licensed from Secret Labs and audited in early versions by Halborn – offers unique advantages unavailable with other solutions:

### Multichain: With Obi, one unified account, with unified recovery and rules, works on all blockchain networks.

Unlike other smart account solutions, Obi accounts are not just chain-agnostic or chain-compatible; they are multichain accounts – where one account can act on all chains, without needing any cross-chain messaging or intermediary infrastructure. This means that one set of simple factors – such as two devices, a phone number, an email, and a passport – becomes a recoverable, updatable key for all your accounts, on all chains.

Obi accounts are automatically available on EVM chains (with the same user address), Bitcoin, and Cosmos SDK chains. Solana and Aptos/Sui are coming soon. Users can create additional, unique accounts if they wish, but all accounts have the same multi-factor security.

### Abstraction Standard Agnostic: Obi abstraction works together with abstraction standards such as ERC-4337 – and also works without any native smart contract support, on chains such as Bitcoin and Atom.

Thanks to Obi Accounts applying abstraction rules and verification at the [signature finalization](../glossary.md#signer) step, rather than at the on-chain verification step, smart accounts can operate on any chain with a supported encryption algorithm. This even includes Bitcoin, Atom (without CosmWasm support), and any other chain which operates with [EOA](../glossary.md#eoa)s or SCAs.

Future chains are automatically supported without the user needing to do any additional deployment or upgrading.

### Cost and Time Savings: Obi saves you money by doing the heavy lifting before spending any transaction fees, without waiting for any additional block times.

By performing transaction checking and signing as a free (no gas) view function/query, Obi accounts can quickly verify items such as rule matching and cryptographic signing without spending gas.

The actual final transaction is submitted with this complex work already complete, so gas cost is minimal. A smart account transaction that needs to ask “Is the owner a session key, spending under their limit, on an allowed contract?” would normally be an expensive transaction, but this work is quickly and seamlessly done ahead of time.

### Flexible Privacy: Obi lets you choose who sees your account rules, keeping your business private.

Obi accounts can have private rules, with updatable and revocable viewing keys that allow parties (individuals, banks, lawyers) to view them if the user allows. Not everyone will want their inheritance accounts and terms to be plainly visible on chain! Obi encrypted state, secured by Secret TEE, allows smart account parameters to be private.

### MEV/Frontun Shielding: Obi Fast Travel transactions, while multi-step, do not need to broadcast the final step early.

Thanks to encrypted communication when the client queries for transaction signatures, the last step of a multi-step transaction does not need to be known publicly when the transaction begins.&#x20;

This can minimize frontrunning opportunities which would otherwise be a disadvantage when compared with traditional non-intent processes.

### Multichain Monetization: Obi transactions pay standard microfees across all blockchains.

Obi smart accounts can impose the current fees on transactions, refusing to sign actions which try to avoid the Obi fee. This applies to all chains: if an Obi account user executes a Bitcoin transaction which sends funds, they must attach the relevant Obi fee. Obi clients such as the Obi modal automatically do this.

These native chain fees accumulate, providing rewards back to Obi nodes and stakers without relying on token inflation and incentivizing further adoption of Obi.

### Your ID is Your Account: With Obi, your existing personal life is your private, unique key for all apps and chains.

Obi accounts are _privately_ built on the parts of a person's ID they chose to use – not just a Google login, a new retina scan by a crystal ball, or some new kind of identity standard which is yet to be widely adopted. Pieces of your life and identity – phone, email, your devices, ID cards, social logins, friends, etc. – can be used to authenticate you privately, whatever app and chain you're on. With enough keys, this approaches bank-grade authentication standards, with or without a custodial element.

### Inheritance and Recovery: Obi ensures your assets are safe and can be recovered or inherited.

Obi accounts can have failsafes at every step of an account’s lifecycle. Even if a user has multiple parts of their identity authentication destroyed, conditional recovery paths can kick in after a delay. This ultimate recovery can also ensure that accounts are passed on in the event that the user passes away. Human-written escrow-like contracts and special rules (such as proportional, incremental, or conditional distribution of inheritance) provide maximum flexibility – making Obi the first scalable, non-custodial, multi-chain solution for insurance companies and trust attorneys. Disclosed inheritance service fees can be contributed back to Obi from inheritance amounts when inheritance is activated.

### Standardization and Insurability: Obi components meet industry standards and is creating new standards, making it trustworthy and insurable for big organizations.

The application of modern web standards such as WebAuthN and ePassports, and the creation of new aggregate standards from these, will make Obi accounts a fully standardized account solution. Meeting NIST/FIPS standards will allow accounts to be insured and adopted by organizations.

### Resilience: Even if something happens to Obi or any part of its technical stack, your accounts are safe and can continue to be used.

Many solutions rely on a specific entity in a specific jurisdiction. They are one action away from being crippled or disabled, whether by a regulator, by a Web2 service provider, or by a bad actor from within or without.

Obi accounts are currently recoverable even if something happens to Obi, and Obi has a roadmap to make _every_ part of the stack – from multi-chain accounts, to Multikey services, to monetization – decentralized and resilient.

The Obi signer (currently on Secret Network) does assist with transaction finalization, in a decentralized and isolated way. But even if the signer's network is down, account [owners](../glossary.md#owner) can finish signatures even if the network is inaccessible or down. Since ordinary user signatures are queries, other authorized parties can also act, as long as a node is available to service queries.

Even a potential catastrophic leak of encrypted state due to an Intel SGX vulnerability can never expose enough information to lose control of user funds. The network never has enough shares to act alone.&#x20;

Obi is resilient, not just by ensuring uptime and security, but by architecting to avoid user loss even if downtime or vulnerabilities are encountered.

On the frontend side, Obi is implementing jails (sandboxes) to defend against supply chain/dependency attacks. Firewall and notification layers can prevent attacks even in the event of unknown exploits.
