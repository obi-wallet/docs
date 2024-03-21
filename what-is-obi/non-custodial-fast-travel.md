---
description: Anything in Two Clicks
---

# 🚆 Non-Custodial Fast Travel

Fast Travel allows users to one-click move from ETH, USDC, or another common asset into an asset or strategy in a different ecosystem.

Fast Travel Tunnels are non-custodial in design, using Obi Accounts abstraction powers to create pre-authorized fast travel routes which the user custodies without having to hand-hold their assets through the entire travel process (bridging, paying gas, swapping, etc.).

Non-Custodial Fast Travel Tunnels generally work like this:

1. An Ethereum deposit address is created as a first step into the Fast Travel tunnel. This Ethereum address is custodied by the user and is pre-authorized to take the first Fast Travel action. The user's originating account is protected from malicious contracts. The Fast Travel address is unable to take any action with a different destination chain, address, asset, or slippage – each address has only one specific path it can ever take.
2. The optimal bridge is used to reach the destination ecosystem. Currently, ecosystems supported by Axelar are supported – meaning all common EVM and Cosmos SDK chains. Additional ecosystems supported by Wormhole are being released soon. The Obi UI exposes Neutron, Sei, Injective, Stargaze, and Osmosis as easy Fast Travel destinations.
3. Any additional steps – such as a DEX swaps, NFT purchases, staking, or liquidity provision – are executed by addresses custodied by the user and pre-authorized to take these Fast Travel actions. These are currently isolated addresses, protecting the user's destination account from malicious contract interactions.
4. The final asset arrives in the user's destination account.
