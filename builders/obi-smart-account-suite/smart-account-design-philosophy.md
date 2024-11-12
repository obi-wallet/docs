# 📜 Smart Account Design Philosophy

## Modular Design

An Obi Smart Account should not be a monolithic contract. Various types of abstraction rules, user state, asset unifiers, global logic, global settings such as current fees, and user settings should be separated into modules. Reasons for this include:

1. Design, debugging, and auditability are easier when dealing with distinct component contracts.
2. Updates, user migrations, and auditing can be performed on individual pieces separately, reducing costs and risks.
3. Contract size limitations become less of an obstacle.
4. Component contracts can control access, providing additional barriers to exploits.
5. Logic-only contracts and global settings contracts can be shared: for example, a user account can point to the current shared contract with inheritance logic, rather than needing to instantiate and migrate their own logic contract.
6. A governance and/or code signing system can be applied to prevent attackers from convincing users to update to malicious contracts.
7. A minimal user-entry contract connected to the rest of the contracts future-proofs accounts, allowing for migration without user addresses changing, even if the code admin is accidentally nulled or native migration is disallowed on the chain.

## Separated State and Logic

An Obi Smart Account should separate user state and logic, so that user state contracts can be minimal while rule application logic can be shared and independently updated. User state includes items such as:

* All abstraction rules (see [Broken link](broken-reference "mention"))
* Last activity time (for v1 inheritance triggering; later solutions may even account for non-execute activity)
* Contract owner
* Currently used global logic contracts
* Global firewall settings

## Unopinionated Modules

More generic Obi Smart Account modules, such as the `user-entry` and `user-account` contracts, should be able to plug in state and logic modules alike without opinions on how they should operate.

## Query Support

Transacting on target chains should, in most cases, not require an execute action on the account's home chain. Being able to get transaction approval/signature with just a query removes the need to pay home chain fees or wait for block confirmation before the final broadcast, and reduces load on the network by over 98%.

## Inability to Act Alone

In the case where a target chain and a home chain differs, an adverse home chain event such as an exploit or governance attack must not be able to sign for target chains – it must not have access to enough shares to sign.

## Offline Support

In the case where a target chain and a home chain differs, the user should be able to finalize signatures (and thus transact) on the target chain even if the home chain is congested, compromised, or unavailable. This does burden the user with additional multi-factor signing/authentication, but allows continued usage even in disaster scenarios.

## Global Firewalls

Global firewall rules should be applicable to an account regardless of other abstraction rules, in order to prevent a bug in some abstraction rule logic contract (or a state contract) from taking a highly destructive action, such as spending all funds or changing the account owner.

## Full Test Coverage

All Obi Smart Account contracts should have 100% unit test coverage and full CI/CD integration test suites with local, testnet, and mainnet support.

## Safe Third-Party Extensibility

Custom abstraction rules and other code can theoretically be plugged in to Obi Smart Accounts. However, there should be several protections involved:

* global firewalls protect from highly destructive actions
* "unlocked" or "unprotected" states which allows attachment of modules signed by other developers
* code signing or governance system establishing the origin of modules, possibly with a path to funded audits or fee share to included modules in a marketplace setup

