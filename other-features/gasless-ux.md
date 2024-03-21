# ⛽ Gasless UX

There are several technologies which enable this:

1. **Use of paymasters**: on EVM chains, the ERC 4337 setup allows for transaction gas fees to be covered.
2. **Feegrant**: on Cosmos SDK chains, x/feegrant provides a similar mechanism (though with much simpler implementation), where an account can authorize its balance to be used to cover transaction fees for another account.
3. **Fee conversion and lending**: if the context requires users to pay their own fees, they can do so in any token with a reliable price source, whether in an EVM or Cosmos SDK context. If the user has no assets, they can still transact, but their account incurs a fee debt. Note that price conversion is not available for tokens which are not established, and the debt module is not included in the scope of the current audits.

This leaves entities (apps, DAOs, communities, etc.) the ability to decide among these situations:

1. Users pay their own fees. This is the default, with fee lending and debt enabled where able.
2. Users pay their own fees in another asset. Suitable for ecosystems and apps focused on a single asset (such as games), this requires either a reliable price source or a manually set rate. Paymasters can accept any amount, so how much the entity cares about the risks of price fluctuations is for them to decide – the paymaster still pays in the network asset (e.g. ETH) and the tokens used to “pay” are sent to the entity.
3. User fees are subsidized. A subsidy pool can cover user fees. This can have maximum per-transaction, per-period, or lifetime limits.
