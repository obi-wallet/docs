# 🔍 Account Abstraction

**Account Abstraction** is a paradigm shift in the way blockchain user accounts are conceptualized and interacted with.

Traditional blockchain accounts on most platforms, including Bitcoin and Ethereum, are directly derived from a cryptographic keypair. The user's account address is derived from their public key, and the mathematically corresponding private key allows them to sign and authorize transactions. These are often referred to as Externally Owned Accounts (EOAs).

However, as blockchain technology evolved, the limitations of this simplistic model became evident:

1. If a private key is lost, the account is completely lost. Since the private key is mathematically in control of the account, there can be no simple account recovery.
2. Similarly, if a private key is stolen, the whole account is stolen – again, beyond recovery.
3. If a user is working directly with their private key, signing transactions with it, that user is vulnerable to catastrophic mistakes (entering the wrong number of zeroes) and to malware and phishing scams where their key, though not actually stolen, is used by them to sign transactions they do not intend.

These problems have led to the emergence of the concept of Account Abstraction.

Early blockchain-level attempts include:

* EOSIO and IOST blockchain technologies, which included a permission structure: the keys which controlled an account could be updated, and keys with action-specific permissions could be added.
* Single-user multisignature accounts. Multisig, originally designed for multiple users controlling funds, can be used for single users to reduce the risk of loss/theft by having multiple keys and a threshold (say, 3 out of 5) of those keys which must sign any transaction. However, updating a multisig if one key is lost or compromised involves creating a new account and painstakingly sending all funds and other assets from the old multisig to the new.
* Immutable (StarkWare) applied abstraction to accounts on their modified EVM chain to suit the needs of games.

Later higher level abstraction included:

* Argent, leading the way with smart account wallets. Gas cost and other issues and interests led to Argent committing to the zkSync ecosystem.
* ZenGo's MPC-driven wallets.
* Numerous other early MPC/smart account wallets.

#### Key Features of Account Abstraction:

1. **Smart Accounts:** Unlike traditional EOAs which are purely cryptographic entities, smart accounts can be contract-based. This means they can embed logic, rules, and conditions that need to be satisfied for transactions to be processed. Essentially, they offer programmability to user accounts.
2. **Off-chain Signing and Bundling:** Transactions intended for smart accounts can be signed off-chain and bundled together. This can lead to efficiency improvements, especially in congested networks. These transactions may be subject to additional checks. For example, if they are fully or partly signed by an MPC network, the network or a user may have rules on what can and what cannot be signed.
3. **Fee Delegation:** Traditional accounts require the account owner to pay for transaction fees. With account abstraction, another entity can cover these fees, improving user experience.

Notable recent account abstraction efforts include:

* Consensus-breaking changes. Cosmos SDK chains have implemented the x/feegrant and x/authz modules, which respectively allow one account to cover another's gas fees and one account to sign certain kinds of messages on behalf of another.
* Soft fork changes, not breaking consensus. The ERC 4337 standard, in particular, is widely available on EVM chains.

#### ERC 4337 and Account Abstraction:

Account Abstraction is a broad concept, but one specific implementation proposal that has gained traction is ERC 4337. Without delving too deeply into the technicalities:

* **User Account Contracts (UAC):** These are the core of ERC 4337, representing the user's smart account. They embed the logic, rules, and conditions for transaction processing. An ERC 4337 contract is _counterfactual_, meaning that its address is known before it is deployed. This has a number of benefits, including 1) a user account can be created and receive funds without paying for and waiting for a blockchain transaction to deploy it and 2) the user's 4337 address can be the same on all EVM chains.
* **Entry Points:** When a transaction is sent to a smart contract, it requires a specific function or "entry point" to be called. In the context of ERC 4337, these entry points streamline how transactions interact with UACs. The entry point contract must be known and interacted with in order to execute a 4337 transaction.
* **Paymasters:** These entities voluntarily cover the transaction fees for the user. They can be set up in various ways, either to promote a service, onboard new users, or for other business reasons.
* **Bundlers:** These can gather multiple signed transactions, bundle them, and submit them to the blockchain. This can be particularly useful to optimize transaction throughput and costs.

4337 is not the final stage of abstraction. Several other updates, such as a way to upgrade EOAs to SCAs (smart contract accounts), are on the roadmap, but will not be deployed for some time. Currently, there is no direct way to migrate an old EOA to an abstracted account. However, an EOA could, for example, become a signer for a 4337 contract's verification logic. Or, an EOA can, on a per-contract basis, approve() a 4337 to spend its tokens or approveAll() to use its NFTs.

Account Abstraction represents a pivotal evolution in blockchain account management. Obi supplies account abstraction as a service, eliminating the complexities and deploying an easy, flexible, and recoverable MPC, AA, and UI components so that optimal crypto UX can be delivered in just a few lines of code.
