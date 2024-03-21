# ‼️ glossary.md

### Abstraction Rule

A rule which allows a certain actor (public key/address) to complete transactions under certain conditions, or which prohibits/delays an actor or actors from completing transactions under certain conditions. Abstraction rule types currently available include allow/block/delay/trigger list, inheritance, owner, sessionkey, and spendlimit.

### Account

See Home Account.

### Actor

The address or public key associated with the signature of an incoming request to the user account or threshold signer contract. This is the party trying to transact on behalf of the user account, and it may be the owner or a party authorized by an abstraction rule.

### Allow/Block/Delay/Trigger List

An abstraction rule type which checks parameters of transactions, such as actor, contract address, action/function name, message type, and parameters. Transactions can be allowed, blocked, or delayed when matching, or can trigger other actions. Governed by the gatekeeper-message contract, where list entries are called Authorizations. EVM targets currently only support contract address.

### Chain ID

The unique identifier for a home or target chain. The code base and documentation uses "home chain ID" and "target chain ID" to avoid confusion.

### Entry Point

A special contract which handles user operations on EVM chains. In the smart contract code, "entry point" also refers to the various home account contract messages, such as instantiate, execute, and query.

### EOA

Externally Owned Account. A traditional blockchain account, where a private key produces signatures which can be verified to belong to the corresponding public key, and thus directly controls addresses and assets.

### Fast Travel Tunnel

A pre-authorized route across multiple chains. Due to the limitations of multi-chain messaging protocols, in most instances, a worker is used to complete subsequent steps of a fast travel transaction. However, the worker is only authorized to proceed with the Fast Travel route approved by the user – the signer will refuse to sign any other transactions.

### Flex Account

An actor authorized by an abstraction rule, such as a spendlimit account, an inheritance beneficiary, or a sessionkey. Used to distinguish authorized accounts from owners and their smart accounts.

### Home Chain, Home Account

A user's home chain is where their smart account lives – where abstraction rules are stored and enforced. In current implementations, this is also where the threshold (MPC) signer contract lives, and can sign for various target chains. In the future, multiple signers may be available. The home chain ID is currently pulsar-3 for development.

### Inheritance

A special kind of spendlimit (allowance) which has a "dormancy period" (cooldown in contract code). Beneficiaries cannot act unless the account has been dormant for this amount of time. Governed by the gatekeeper-spendlimit contract.

### Intent

In the context of distributed applications, an action where the user expresses their desire – such as obtaining a specific asset – without needing to execute the various (often complex) details needed to reach that objective.

### MEV-Shielded Intent

Decentralized intents on public blockchains often require broadcast of the intent ahead of the final transaction, exposing the user to much higher levels of frontrunning if preliminary steps are required first – such as waiting for bridging transactions to his finality. Obi intents do not require the public broadcasting of final assets before bridging.

### Modular

A design principle for distributed applications which uses specialized distributed networks for specific purposes in the stack – such as using one chain for settlement, consensus, execution, and data availability.

### Modular Accounts

Obi's play in the modular space. Unlike most other modular solutions, Obi accounts can be used seamlessly without the blockchain or application developers needing to even have knowledge of it.

### Owner

The address or public key (preferably a ) which is the ultimate owner of the user smart account; the user. The owner is the only signer authorized to take admin actions such as updating the account, updating the owner, and adding abstraction rules.

### Paymaster

The service and account which covers fees for user transactions on EVM chains.

### Sessionkey

A temporary authorization to transact. The actor for a sessionkey can sign transactions subject to the sub\_rules (of type message for allowlists and spendlimit for spending restrictions), until the expiration time is reached. A sessionkey can destroy itself or can be destroyed by the owner at any time. Governed by the gatekeeper-sessionkey contract.

### Signer

A special smart contract which can finalize signatures for transactions, regardless of their target chain, if and only if they are allowed to be signed by the associated user account, or they are signed by the full owner of the user account.

### Smart Account

A smart contract account. Transactions are only approved if they match the abstraction rules held in smart contract code/state, which may be simple ("Is the actor the owner?") or complex ("Is the actor an active session key, and does this transaction spend funds less than or equal to the session key's remaining spend limit?")

### Spendlimit

An allowance, permitting an actor to spend a user account's funds. The usual term "allowance" is avoided here to distinguish from token contract allowances, which are handled by token contracts instead of account contracts. A spendlimit can be used for a budget or subscription. On some chains, spendlimits can be unified, meaning that assets with known price sources can be converted to the spendlimit asset when verifying transactions. For example, ETH could be spent by an actor with a USDC unified spendlimit. Spendlimits are governed by the gatekeeper-spendlimit contract, where list entries are currently called PermissionedAddresses, which have params for spendlimit details and beneficiary\_params for inheritance details. A single actor/address can have both.

### Target Chain, Target Account

The destination for a transaction. Assets and addresses on various target chains (Ethereum, Arbitrum, Polygon, Bitcoin, Cosmos, Osmosis, etc.) can be controlled by the user's smart account on their home chain, thanks to threshold signer contracts.

### Threshold Signer

A special contract which can finalize a threshold signature for a transaction on a target chain if the party calling it is authorized to perform this transaction by some abstraction rule. A threshold signer contains a single share of a user's target private key.

### User Account Contract (UAC)

The target user account; an ERC4337 contract account on an EVM chain. This is different from the smart account, which is a home account. UAC is used as this is an industry standard term, but we clarify "target user account contract" as much as possible. These contracts are deployed on demand to target chains. The address is known ahead of time and is the same for all target chains. User operations can be signed by the user's target private key and executed on target chains.

### User Entry Contract

The user's home smart account entry point. This is the address where the user's home assets, if any, are kept.

### User Operation

An ERC4337-compliant wrapped transaction. This is a normal Ethereum transaction packed and signed in such a way that a bundler/paymaster can submit the transaction and cover fees for the user. The user operation is signed by the user's target private key. This target private key has a deterministic association with the user's ultimate ERC4337 target account address, but it does not have a direct cryptographic association. In other words, if you imported this private key into a traditional wallet, the resulting public key and address would be different from the user's ERC4337 address.
