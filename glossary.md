# Glossary

### Account

See [Home Account](glossary.md#home-account).

### Actor

The address or public key associated with the signature of an incoming request to the [user account](glossary.md#home-account) or threshold [signer](glossary.md#signer) contract. This is the party trying to transact on behalf of the user account, and it may be the [owner](glossary.md#owner) or a party authorized by a [transaction policy](glossary.md#transaction-policy).

### Allow List

A [transaction policy](glossary.md#transaction-policy) type which checks parameters of transactions, such as [actor](glossary.md#actor), contract address, action/function name, message type, and parameters. Only matching transactions are allowed; otherwise, the action is blocked, unless the caller is [owner](glossary.md#owner). Policies are stored in `user-state` contract and logic executed by the `gatekeeper-message` contract, where relevant policies are called `Authorizations`. EVM targets currently only support [actor](glossary.md#actor) and contract address filtering.

### Authorization

The internal name for any kind of [transaction policy](glossary.md#transaction-policy) which depends on message inspection, such as [Allow List](glossary.md#allow-list), [Block List](glossary.md#block-list), [Delay List](glossary.md#delay-list), and [Trigger List](glossary.md#trigger-list) policies. Action-limited session keys can be created by using `expiration` in conjunction with such policies.

### Block List

A [transaction policy](glossary.md#transaction-policy) type which checks parameters of transactions, such as [actor](glossary.md#actor), contract address, action/function name, message type, and parameters. A matching transaction is blocked. Policies are stored in `user-state` contract and logic executed by the `gatekeeper-message` contract, where relevant policies are called `Authorizations`. EVM targets currently only support [actor](glossary.md#actor) and contract address filtering.

### Chain ID

The unique identifier for a [home](glossary.md#home-chain) or [target chain](glossary.md#target-chain). The code base and documentation uses "home chain ID" and "target chain ID" to avoid confusion.

### Delay List

A [transaction policy](glossary.md#transaction-policy) type which checks parameters of transactions, such as [actor](glossary.md#actor), contract address, action/function name, message type, and parameters. A delay can then be enforced if the parameters match a delay policy. Policies are stored in `user-state` contract and logic executed by the `gatekeeper-message` contract, where relevant policies are called `Authorizations`. EVM targets currently only support [actor](glossary.md#actor) and contract address filtering.

### Entry Point

A special contract which handles [user operations](glossary.md#user-operation) on EVM chains. Note that in the Rust contract code – including [home account](glossary.md#home-account) code – "entry point" also refers to the various home account contract messages: `instantiate`, `execute`, `migrate`, `sudo` and `query`.

### EOA

Externally Owned Account. A traditional blockchain account, where a private key produces signatures which can be verified to belong to the corresponding public key, and thus directly controls addresses and assets. An Obi account is not an EOA, but it can control any number of EOAs on any number of chains.

### Fast Travel Tunnel

A pre-authorized route across multiple chains. Due to the limitations of multi-chain messaging protocols, in most instances, a non-custodial [worker address](glossary.md#worker-address) is used to complete subsequent steps of a fast travel transaction. However, the worker is only authorized to proceed with the Fast Travel route approved by the user – a [signer](glossary.md#signer) will refuse to sign any other transactions.

### Flex Account

An [actor](glossary.md#actor) authorized by a [transaction policy](glossary.md#transaction-policy), such as a spendlimit account, an [inheritance](glossary.md#inheritance) beneficiary, or a [sessionkey](glossary.md#gasless-mpc). Used to distinguish authorized accounts from [owners](glossary.md#owner) and their smart accounts (whether [home accounts](glossary.md#home-account) or [target accounts](glossary.md#target-account)). A [worker address](glossary.md#worker-address) is architecturally identical, but is intended to be easily triggered and [immutably](glossary.md#immutable-intents) bound to [intent](glossary.md#intent), not directly controlled by another person or device.

### Gasless MPC

Obi's MPC signature finalization runs on a query, which passes no gas cost on to the user, returns instantly without waiting for block time, and costs the node 1/80th of the resources of a typical transaction. Gas is still paid by the user or their sponsor on the [target chain](glossary.md#target-chain), whether directly or via fee abstraction (`feegrant` or ERC-4337 paymaster).

### Home Account

The user's account on the [home chain](glossary.md#home-chain).

### Home Chain

A user's home chain is where their smart account lives – where [transaction policies](glossary.md#transaction-policy) are stored and enforced. In current implementations, this is also where the threshold (MPC) [signer](glossary.md#signer) contract lives, and can sign for various [target chains](glossary.md#target-chain). In the future, multiple signers will be available. The home chain ID is currently secret-4. It will be obi-1 upon Obi network activation, with secret-4 as a backup.

### Immutable Intents

Intent-bound [worker addresses](glossary.md#worker-address) cannot have their [intent](glossary.md#intent) modified. This is doubly ensured by the address keypair combining the intent with its entropy – meaning that if a signature is created for a different intent (such as a different asset, receiver, or slippage setting), the signature will not even match and no execution can proceed.

### Inheritance

A special kind of [spendlimit](glossary.md#spendlimit) (allowance) which has a "dormancy period" (`cooldown` in contract code). Inheritanced beneficiaries cannot act unless the account has been dormant for this amount of time. Governed by the `gatekeeper-spendlimit` contract.

### Intent

In the context of distributed applications, an intent is a (trans)action where the user expresses their desire – such as obtaining a specific asset – without needing to execute the various complex details needed to reach that objective. For example, the user may say "I wish to convert this ETH on Arbitrum to a wstETH/ETH LP on a Cosmos chain," instead of separately signing the 10-12 transactions usually required to perform such an action. Obi can restrict intent solvers, whether AI or otherwise, so that they cannot violate customizable [transaction policies](glossary.md#transaction-policy).

### Modular

A design principle for distributed applications which uses specialized distributed networks for specific purposes in the stack – such as using one chain for settlement, consensus, execution, and data availability.

### Modular Accounts

Obi's place in the modular space. Unlike most other modular solutions, Obi accounts can be used seamlessly without the blockchain or application developers needing to even have knowledge of it.

### Obi

A Japanese word for certain types of belts. In addition, _bi_ is the Mandarin word for "coin."

### Owner

The user; the address or public key (preferably a [Broken link](broken-reference "mention")) which is the ultimate owner of the user [smart account](glossary.md#smart-account). The owner is the only signing party authorized to take admin actions such as updating the account, updating the owner, and adding [transaction policies](glossary.md#transaction-policy).

### Paymaster

The service and account which covers fees for user transactions on EVM chains.

### Sessionkey

Enabling a "one-click login experience" that can still protect the user from destructive or accidental actions, a sessionkey is a temporary authorization to transact until the expiration time is reached. A sessionkey can destroy itself or can be destroyed by the owner at any time. The sessionkey can be limited by any other kinds of limitations, such as [spend limits](glossary.md#spendlimit), message restrictions, contract address restrictions, and more. The "sessionkey policy" is an abstraction itself; it is expressed in code by attaching an `expiration` to some other kind of [transaction policy](glossary.md#transaction-policy). An admin-level sessionkey is simply an unrestricted [Allow List](glossary.md#allow-list) (`actor` matching only) with an `expiration` attached.

### Signer

A special smart contract which can finalize signatures for transactions, regardless of their [target chain](glossary.md#target-chain), if and only if they are allowed to be signed by some [transaction policy](glossary.md#transaction-policy), r they are signed by the full [owner](glossary.md#owner) of the user account. The finalization is the final round of threshold [MPC](broken-reference) signing. A threshold signer has access – in a secure, isolated Intel SGX hardware environment – to a single share of a user's [target](glossary.md#target-account) private key.

### Smart Account

A smart contract account. Transactions are only approved if they match the [transaction policies](glossary.md#transaction-policy) held in smart contract code/state, which may be simple ("Is the actor the [owner](glossary.md#owner)?") or complex ("Is the actor an active [session key](glossary.md#sessionkey), and does this transaction spend funds less than or equal to the session key's remaining [spend limit](glossary.md#spendlimit)?"). The Smart Account does not itself finalize transaction signatures – prior to finalizing, the [signer](glossary.md#signer) asks the relevant smart account if the given message may be signed for the given [actor](glossary.md#actor).

### Spendlimit

An allowance, permitting an [actor](glossary.md#actor) to spend a user account's funds. The usual term "allowance" is generally avoided here to distinguish from token contract allowances, which are handled by token contracts instead of account contracts. A spendlimit can be used for a budget or subscription. On some chains, spendlimits can be unified, meaning that assets with known price sources can be converted to the spendlimit asset when verifying transactions. For example, ETH could be spent by an [actor](glossary.md#actor) with a USDC unified spendlimit. Spendlimits are governed by the `gatekeeper-spendlimit` contract, and entries include `params` for spendlimit details and `beneficiary_params` for inheritance details. A single [actor](glossary.md#actor)/address can have both.

### Target Account

The destination "actor" for a transaction – the account associated with the transaction on the [target chain](glossary.md#target-chain). Assets and addresses on various target chains (Ethereum, Arbitrum, Polygon, Bitcoin, Cosmos, Osmosis, etc.) can be controlled by the user's smart account on their home chain, thanks to threshold signer contracts. From the perspective of the target chain, a transaction is a simple, standard transaction – whether an EOA or SCA transaction – and there is no need for the chain to be aware that an Obi Account's transaction policies were checked in order to finalize the transaction signature.

### Target Chain

The destination chain for a transaction. One [home account](glossary.md#home-account) can control addresses/accounts on any number of target chains.

### Transaction Policy

A permission; a rule which allows a certain actor (public key/address) to complete transactions under certain conditions, or which prohibits/delays an actor or actors from completing transactions under certain conditions. Transaction policy types currently available include [allow](glossary.md#allow-list)/[block](glossary.md#block-list)/[delay](glossary.md#delay-list)/[trigger](glossary.md#trigger-list) list, [inheritance](glossary.md#inheritance), [owner](glossary.md#owner), [sessionkey](glossary.md#sessionkey), and [spendlimit](glossary.md#spendlimit) policies – which can be used as allowance/budget or subscription policies.

### Trigger List

A transaction policy type which checks parameters of transactions, such as [actor](glossary.md#actor), contract address, action/function name, message type, and parameters. Blockchain actions can be triggered – whether directly or by appending to messages. Policies are stored in `user-state` contracts and logic executed by the `gatekeeper-message` contract, where relevant policies are called [authorizations](glossary.md#authorization). EVM targets currently only support [actor](glossary.md#actor) and contract address filtering.

### User Account Contract (UAC)

A target user account which is not an EOA but an ERC4337 contract account on an EVM chain. This may also apply to analogous accounts on Cosmos chains and Solana in the future. This is different from the user's core smart account, which is a [home account](glossary.md#home-account). UAC or SCA (smart contract account) is used, as this is an industry standard term, but we clarify "[target user account](glossary.md#target-account) contract" as much as possible. These contracts are deployed implicitly or on demand to [target chains](glossary.md#target-chain). The address is known ahead of time, and is the same across all target EVM chains. [User operations](glossary.md#user-operation) can be signed by the user's target private key and executed on target chains.

### User Entry Contract

The user's [home smart account](glossary.md#smart-account) entry point. This is the address where the user's home assets, if any, are kept.

### User Operation

An ERC4337-compliant wrapped transaction. This is a normal Ethereum transaction packed and signed in such a way that a bundler/paymaster can submit the transaction and cover fees for the user. The user operation is [signed](glossary.md#signer) by the user's [target](glossary.md#target-account) private key. This target private key has a deterministic association with the user's ultimate ERC4337 target account address, but it does not have a direct cryptographic association. In other words, if you imported this private key into a traditional wallet, the resulting public key and address would be different from the user's ERC4337 address.

### Worker Address

[Transaction policies](glossary.md#transaction-policy) often apply to other individuals, but they can also be used to implicitly create [intent](glossary.md#intent)-bound addresses. Assets and other properties belonging to these addresses can only pursue the allowed intent. This allows non-custodial pre-authorized activity, such as [fast travel tunnels](glossary.md#fast-travel-tunnel), stop losses, and [triggered](glossary.md#trigger-list) actions, without needing special smart contract pools or custodial solutions.
