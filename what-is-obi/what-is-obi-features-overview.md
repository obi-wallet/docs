# 🔍 What is Obi?

Obi is a blockchain-agnostic (modular) non-custodial solution for user account management, [permissions](../glossary.md#abstraction-rule), recovery, [inheritance](../glossary.md#inheritance), [intents](../glossary.md#intent), and security.

Permissions can be extended to pre-authorize [intents](../glossary.md#intent) with , creating one-click non-custodial products such as [non-custodial-fast-travel.md](non-custodial-fast-travel.md "mention").

Obi is:

* **seedless**: no seed phrases ever need to be backed up or inputted by the user
* **non-custodial**: all keys are held by the user, or generated on demand from information held by the user (with the hypothetical exception of custom convenience or recovery keys which could be custodied by ecosystems)
* **disaster-proof**: a user can lose multiple keys, have multiple keys stolen, or be incapacitated  – and still the user or their beneficiaries can recover assets
* **upgradeable**: user account components can, with the user’s authorization, be updated
* **blockchain-agnostic**: Obi accounts can control addresses and assets on any [target chain](../glossary.md#target-chain) with [Obi Passport](../smart-account-architecture/multichain/obi-passport.md) and can interact directly with apps on those chains without installing more wallets or setting up more rules
* **secure**: account-specific Rust smart contract instances secure Obi accounts. Special security modules, health checks, and security notifications provide additional failsafes
* **attack and loss resistant**: [Seedless Multikey](broken-reference) prevents loss or compromise of 1 or 2 keys (or shares) from compromising the entire user account. Phishing resistance is provided by [Threshold Escalation](../smart-account-architecture/flex-accounts/threshold-escalation.md). Some contexts also allow for early quantum-resistant cryptography
* **flexible**: [allowance](../glossary.md#spendlimit), [inheritance](../glossary.md#inheritance), [session key](../glossary.md#sessionkey), [allow](../glossary.md#allow-list)/[blocklist](../glossary.md#block-list), mandatory [delay](../glossary.md#delay-list), [subscription](../glossary.md#spendlimit), and other rules can be set, authorizing other users to act if they follow the rules
* **extensionless**:
  * UX improves and onboarding completion rates increase when users do not need to install an app or extension to use Obi
  * Obi features can also be integrated into existing wallet applications, including MetaMask Account Snaps
  * Obi by default runs in a browser tab or as a progressive web app with Wallet Connect across to other tabs
  * Obi is not vulnerable to being taken down by app stores, which often happens with wallet applications
  * even in multiple contexts, Obi accounts can still be universal due to the coincidence of multiple signing factors: create an account in one web app, use it in another
* **feeless** experience: although transactions do cost native network fees on [target chains](../glossary.md#target-chain), these are covered or abstracted away for Obi users in various ways
* **easy**: users use diverse but familiar web2 patterns to generate or store their non-custodial keys
