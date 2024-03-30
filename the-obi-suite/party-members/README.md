# 🧙‍♂️ Party Members

Account abstraction enables an Obi Account to enforce rules on transactions, especially regarding permissions given to other accounts or addresses. This unlocks a new design space.

The Obi Account smart contract can attach “gatekeepers” which manage the rules enforced on transactions. Currently available gatekeepers include:

* Spend Limit (Allowances)
* Session Key
* Message (Allow/Block List)
* Debt (Fee Lending)
* Delay

Other gatekeepers can be designed and plugged in by SDK users, community members, or even by end users.

The Obi Account and gatekeeper contracts are independent modules with full access control. Upgrades to implementation only take effect when the user upgrades to a verified new code id, which is not a required action.

Several utility contracts support these: the Asset Unifier and its associated Pair Registry, which holds the LP contracts that must be known in order to retrieve the values of an array of assets in a single selected asset, usually a USD stablecoin. Other price sources may be enabled at a later time.
