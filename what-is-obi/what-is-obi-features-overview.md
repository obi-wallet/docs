# 🔍 What is Obi? Features Overview

Obi is a blockchain-agnostic, full-stack, non-custodial solution for user account management, permissions, recovery, inheritance, and security.

Permissions can be extended to pre-authorize intents, creating one-click products such as [non-custodial-fast-travel.md](non-custodial-fast-travel.md "mention").

Obi is:

* **seedless**: no seed phrases ever need to be backed up or inputted by the user
* **non-custodial**: all keys are held by the user, or generated on demand from information held by the user, with the optional exception of convenience or recovery keys which can be custodied by business clients
* **disaster-proof**: user can lose multiple keys, have multiple keys stolen, or be incapacitated  – and still the user or their beneficiaries can recover assets
* **upgradeable**: user account components can, with the user’s authorization, be updated
* **blockchain-agnostic**: Obi accounts can control addresses and assets on any chain with [Obi Passport](../smart-account-architecture/multichain/obi-passport.md) and can interact directly with apps on those chains without installing more wallets or setting up more rules
* **secure**: account-specific Rust smart contract instances secure Obi accounts. Special security modules, health checks, and security notifications provide additional failsafes
* **attack and loss resistant**: [Seedless Multikey](broken-reference) prevents loss or compromise of 1 or 2 keys (or shares) from compromising the entire account. Phishing resistance is provided by [Threshold Escalation](../smart-account-architecture/flex-accounts/threshold-escalation.md). Some contexts also allow for early quantum attack resistance, even before networks integrate quantum-resistant signing algorithms
* **flexible**: allowance, inheritance, session key, allow/blocklist, mandatory delay, subscription, and other rules can be set, authorizing other users to act if they follow the rules
* **extensionless**:
  * UX improves and onboarding completion rates increase when users do not need to install an app or extension to use Obi
  * Obi features can also be integrated into existing wallet applications
  * Obi is not vulnerable to being taken down by app stores, which often happens with wallet applications
  * even when used without an extension or Obi app, Obi accounts can still be universal due to the coincidence of multiple signing factors: create an account in one web app, use it in another
* **feeless** experience: although transactions do cost native network fees, these are covered or abstracted away for Obi users in various ways
* **easy**: users use diverse but familiar web2 patterns to generate or store their non-custodial keys
