---
description: Overview of the five modular component groups of the Obi stack
---

# 🧩 Obi Stack Overview

<figure><img src="../.gitbook/assets/Obi Stack Dark.png" alt=""><figcaption></figcaption></figure>

The Obi stack has five component groups which can be swapped out or upgraded independently, without adversely affecting users.

### Transaction Flow

A typical transaction involves:

1. The user signs the transaction request with their Multikey threshold (or with a user-authorized allowance account or easy session key).
2. The user’s account allows or blocks the transaction based on the current [abstraction rules](../smart-account-architecture/flex-accounts/), the simplest of which is, “Is the sender/signer the account owner?”
3. Obi Passport completes the signature with the network share, an irretrievable share which can only sign if step 2 allowed the transaction.
4. This final signed transaction is broadcast directly or via 4337 relay/paymaster.

Step 1 is local to the client application. Under most conditions, steps 2 and 3 are gasless queries. Step 4 fees are covered by the paymaster.

The user is unaware of most of this process. They sign a transaction – sometimes automatically in the case of easy restricted session keys – and then can see the results on the destination network.

### [Seedless Multikey](broken-reference)

This is the most flexible and multifaceted Obi component. Some solutions will not rely on the full stack at once; key types may be updated and added as the stack matures. Most key types are non-custodial, but there are semi-custodial or custodial recovery options for certain cases.

#### **Protections**

If a key is lost or stolen, the user can replace the bad key – updating any multisig components and rerolling MPC shares in one convenient step.

_Security Notifications_ is an upcoming service which can, without holding any personal identifying information, alert current wallet users if someone has used or is attempting to use one of their Multikey keys.

#### Upgrades

Multikey services are currently managed in a centralized fashion (see [Obi Service Providers](../roadmap-features/obi-service-providers/)) and can be updated. After audits, code will begin to transition to open source and will be verifiable.

#### Failsafes

In the unlikely case of catastrophic multi-service failure of the Multikey system at the same time a user loses keys they custody without the use of services, the user is able, after a delay, to recover funds managed by their Obi Accounts via Final Recovery.

In a future version, Multikey services needed for some key types will be offered by a network of multiple service providers.

### [Obi SDK](broken-reference)

The Obi Modal can be integrated as a webview in apps, websites, and games. A native Unity solution is available. The frontend modal can communicate with the host site. Alternatively, JavaScript functions can be used directly.

#### **Protections**

iFrames are used to hinder man in the middle attacks. SES (Hardened JavaScript) is in the works for this component group. It is not yet deployed.

#### Upgrades

The Obi Modal code is managed by Obi. Eventually, the code will transition to open source, and updates will be subject to verification, additional audits, and optional deployment.

#### Failsafes

Any party could, with sufficient knowledge or with a tool built by someone with sufficient knowledge, interact with the blockchain directly and thus avoid the need for the SDK components. (Conversely, any protections which are built into the JavaScript side are not actually gatekeepers – security measures protecting user keys, accounts, and assets must be implemented elsewhere.)

In the future, the Obi standalone application will be updated to allow this functionality on any chains, giving users a power tool to access their account even if their usual application website is compromised or unavailable.

### **ERC 4337 Relay/Paymaster**

For EVM target chains, Obi accounts use standard (stock, OpenZeppelin-audited) ERC 4337 setups. Any provider can be used; we recommend [Stackup](https://www.stackup.sh/) for those developing concepts or smaller applications not wishing to incur the hassle of solution-specific infrastructure.

An application can switch to another provider or another chain without breaking user experience or requiring complicated user migration.

#### **Protections**

The ERC 4337 standard is non-custodial. A malicious party cannot reasonably attack without phishing the user’s key; the Multikey and Passport setup are designed to make this supremely impractical once a user reaches a secure key threshold.

#### Failsafes

It is trivial to switch to another paymaster. If a paymaster were to fail, the user’s MPC key (controlled by Multikey) can use another paymaster.

### [Obi Passport](../smart-account-architecture/multichain/obi-passport.md) (chain-agnostic signing)

ERC 4337 user operations, or Cosmos or other transactions, are signed with a multi-party threshold setup. “Multi-party” should not be taken to mean that parties other than the user are involved, just that multiple key shares are used rather than a single private key.

#### **Protections**

This setup is carefully designed to ensure the following:

1. The key shares are encrypted by different Multikey factors, preventing a single factor attack or loss from compromising the account. Shares can be rerolled in the event of compromise.
2. Account inheritance can be set up by distributing some shares and using a network share. The network share will only distribute inheritance keys and assist in finalize signatures if inheritance is active (i.e. the dormancy period has passed).
3. If the network share becomes inaccessible, the user can still sign with their factors.
4. If the network or the secure hardware it uses is compromised, the attacker cannot obtain enough shares to sign transactions.

Transactions are convenient thanks to the network share’s ability to verify a transaction with the account’s abstraction rules before returning a signature.

There are several well-maintained networks which support the role of “network share.” Secret Network uses Intel SGX secure hardware nodes with end-to-end transaction encryption and various other protections. Other options use the AMD equivalent. Lit Protocol is a multi-party KMS network which is similarly usable.

Dozens of similar networks are in development, and even though network shares are not exportable, thanks to the ability to reroll MPC shares, Obi accounts do not need to rely on the longevity of any of these networks.

#### Upgrades

By rerolling shares, an Obi user can move to a new network share system quickly and seamlessly. Assuming the new signer can connect to the user’s account (which may or may not require an account redeployment), the process will not affect the rest of the user’s stack. In no case will it change the user’s final address.

#### Failsafes

As mentioned just previously, a user can still sign with their Multikey shares if any or all of the network shares are unavailable.

Convenience (such as session keys) may be reduced in the downtime, and inheritance functions may not be available during the downtime. For these reasons, Obi’s goal is to enable alternate network shares in the next release.

In the case of sustained failure, the user can deploy network shares to a different network. If inter-network communication is not available between the user’s account network and the share network, the account can be redeployed as well, without affecting user addresses or assets.

### **Obi Smart Accounts**

Obi accounts are upgradeable multi-contract Rust programs.

They can be deployed directly using a precompile solution such as Ink!, or – more cheaply and commonly – they can run on networks with direct support for Rust contracts. Obi Accounts are designed to be able to sign (manage assets and addresses) on chains other than their home chain.

Obi Smart Accounts offer account abstraction solutions.

#### **Protections**

Administrative actions cannot be taken by authorized keys other than the owner, which is designed to be a user’s Multikey. Updates of this owner must be authorized by the owner and then accepted by the new owner so that users cannot accidentally transfer ownership to a non-existent account.

#### Upgrades

Upgradeability applies to Obi account components in different ways:

* The simple `user_entry` contract cannot currently be upgraded without redeployment. Native migration may be a possibility in the future.
* The `user_state` contract **can** be upgraded, but as it is simple state storage, upgrade is unexpected. The usual migration path upgrades the rest of the account without touching `user_state`.
* The `user_account` logic contract can be upgraded by pointing `user_entry` to a new deployment.
* The `gatekeeper` contracts are shared logic, and so can be upgraded by Obi, or eventually by governance. Users need to approve the upgrade.

All of these are generally combined into a quick and simple `NewAccount` → `UpdateUserAccountAddress` flow.

#### Failsafes

Even in the case that a bug, governance attack, network downtime, or something else disables Obi Account functionality for a time, users can complete signing with their Multikey-controlled MPC shares. The convenience and recoverability of their MPC setup will be reduced, as they will have to meet threshold without a network share and will be unable to use advanced account abstraction.

In the case of sustained failure, the user can deploy their account to another network without disrupting their addresses or assets.
