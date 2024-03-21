# @obi-wallet/sdk notes

_This is specific documentation to the lowest level of Obi SDK. For more information on Obi SDK with UI or three-lines-of-code integration, visit_ [_the parent page_](https://www.notion.so/Obi-SDK-9997bbf5f2554ad8b5896eb4493a2634?pvs=21)_._

@obi-wallet/sdk consists of multiple data structures and other classes that allow you to integrate Obi wallets into your own application with maximum flexibility.

This page serves to introduce concepts and general usage. For more detailed documentation, clone the repository and run `nx docs sdk`.

### Data Structures

A data structure represents something that you most likely want to persist somehow (e.g. in a database, on-device KV store, etc.). In a React app, we expect these to be part of your “store” (e.g. MobX, Redux). Since it consists of sensible data, you want to save it in a secure storage (e.g. KeyChain) and possibly also add another encryption layer.

All data structures have an _observable_ version (for usage with MobX) and a _non-observable_ version (for other usages) that both satisfy the same interface. Both versions expose a single factory that accepts serialized data, migrates it to the current version (so you may pass possibly outdated serialized data), and then returns an instance of the data structure. Some data structures don’t necessarily need serialized data. If it’s not passed, it creates an empty version.

Every data structure can be serialized to a plain JavaScript object with `.toJSON()`. If your persistence layer can’t work with JSON, use `JSON.stringify()` too, and `JSON.parse` when loading the data.

#### Wallets

`Wallets` is a collection of `MultisigWallet`s:

```tsx
// Create empty collection
const wallets = Wallets.create() // OR: ObservableWallets.create()

// OR: load from persisted data
const data = await loadData() // e.g. load from KV-store, consumer responsibility
const wallets = MultisigWallet.create(data)

console.log(wallets.wallets) // array of all existing wallets
console.log(wallets.currentWallet) // currently selected wallet or null

wallets.setCurrentWallet(wallet) // set current wallet
wallets.logout() // deselect wallet,
wallets.getWalletByProxyAddress("terra...") // get the wallet with the specified proxy address
wallets.removeWallet(wallet) // remove wallet
wallets.upsertWallet(wallet) // insert or update wallet

// Persist data
const data = wallets.toJSON() // OR: const dataString = JSON.stringify(wallets.toJSON())
await persistData(data)
```

#### MultisigWallet

A `MultisigWallet` represents an Obi smart account.

```tsx
// Load from serialized data
const data = await loadData()
const wallet = MultisigWallet.create(data)

console.log(wallet.meta) // Info about the current wallet and possibly selected sub account
console.log(wallet.chainId) // ID of the wallet's home chain
console.log(wallet.chain) // Information about the wallet's home chain
console.log(wallet.isDemo) // true if this is a demo wallet
console.log(wallet.proxyAddress) // proxy address (i.e. contract address) of the wallet
console.log(wallet.address) // returns the address of the selected singlesig wallet (if any is selected); proxy address otherwise.
console.log(wallet.shortenedAddress) // address shortened to max 20 characters for displaying
console.log(wallet.currentAccount) // currently selected sub account or null
console.log(wallet.getAccountByMeta(accountMeta)) // get the sub account specified by the param
console.log(wallet.owner) // owner of the MultisigWallet, is a multisig key.
console.log(wallet.gatekeeperConfig) // current gatekeeper config, manages beneficiaries and flex accounts
console.log(wallet.singlesigWallets) // array of attached singlesig sub accounts

wallet.setAccountByMeta(accountMeta) // set current account
wallet.setOwner(owner) // set new owner
wallet.setGatekeeperConfig(gatekeeperConfig) // set new gatekeeper config
wallet.upsertSinglesigWallet(singlesig) // insert or update singlesig wallet
wallet.removeSinglesigWallet(singlesig) // remove singlesig wallet
console.log(await wallet.canExecute({ flexAccount, messages })) // true if the given flex account can execute the specified address
const broadcastResult = await signAndBroadcastTransaction({ flexAccount, messages }) // sign and broadcast tx with the given flex account and given messages
const broadcastResult = await signAndBroadcastTransaction({ singlesigWallet, messages }) // sign and broadcast tx with the given singlesig wallet and given messages
```

#### MultisigKey

A `MultisigKey` represents a multisig threshold key. It consists of multiple `Key`s. A `Key` may still be in a non-usable form (if we only know the public key and the user didn’t finish the recovery process for that specific key). A `Key` becomes usable if we have all relevant information required for that respective `Key`. A `Key` that is usable and not only intended for recovery can be used to sign.

At the moment, we only allow a single key for each type (e.g. you can’t have two phone number keys in your multisig).

Note that “multisig” is legacy terminology – in some setups, the Multikey keys are used to encrypt/decrypt MPC shares, rather than being used directly to sign.

```tsx
// Create empty MultisigKey
const key = MultisigKey.create()

// OR: load from persisted data
const data = await loadData()
const key = MultisigKey.create(data)

console.log(key.chainId) // ID of the multisig key's home chain
console.log(key.threshold) // Number of keys needed to sign
console.log(key.publicKey) // public key of the multisig, atm always of type "Tendermint/PubKeyMultisigThreshold"
console.log(key.address) // address of the multisig
console.log(key.keys) // array of all keys (in-order)
console.log(key.signerTypes) // array of all key types (strings)
console.log(key.hasKeyOfType(KeyType.Device)) // true if the multisig has a key of the given type
console.log(key.getKeyOfType(KeyType.Device)) // returns the key of the given type or undefined
console.log(key.getUsableKeyOfType(KeyType.Device)) // returns the usable key of the given type or undefined

// To make changes to the multisig key, you'd usually make a clone
// and persist all changes together in the end.
const otherKey = key.clone()
console.log(key.equals(otherkey)) // true if key represents the same multisig key as otherKey

key.setThreshold(2) // set threshold
key.setKey(keyInfo) // appends the given key to the multisig. Removes any existing keys of the same type
key.removeKeyOfType(KeyType.Device) // removes the key with the given type
const signer = await key.createSigner({ messages }) // creates a `MultisigSigner` for the given messages
```

#### Key

A `Key` represents a single key in your `MultisigKey`. Every key has a public key, and potentially type-specific additional information. A `Key` is either a `UsableKey` (key that finished recovery and where all required information is present on-device) or a `PendingRecoveryKey` (key where only the public key is known and some crucial information is still missing).

```tsx
// Load from persisted data
const data = await loadData()
const key = Key.create(data)

console.log(key.type) // type of the key, e.g. KeyType.Phone
console.log(key.publicKey) // public key of the key
console.log(key.isUsable) // true if the key is usable
console.log(key.payload) // type-specific additional information for usable keys
```

#### GatekeeperConfig

A `GatekeeperConfig` manages `Beneficiary`s, `FlexAccount`s and their session keys. Most of the information is also saved on-chain (in various Gatekeeper contracts) but there’s also some local meta data (e.g. icons).

There shouldn’t be a need to initiate the `GatekeeperConfig` yourself. You can use `multisigWallet.gatekeeperConfig` (and clone that if you want to batch multiple changes before committing them to chain)

```tsx
console.log(config.beneficiaries) // array of beneficiaries
console.log(config.flexAccounts) // array of flex accounts

config.upsertBeneficiary(beneficiary) // insert or update beneficiary
config.removeBeneficiary(beneficiary) // remove the given beneficiary
config.upsertFlexAccount(flexAccount) // insert or update flex account
config.removeFlexAccount(flexAccount) // remove the given flex account

// To make changes to the gatekeeper config, you'd usually make a clone
// and persist all changes together in the end.
const otherConfig = config.clone()
// We consider two configs to be equal if their on-chain data would be the same
console.log(config.equals(otherConfig)) // true if config represents the same gatekeeper config as otherConfig
```

#### Beneficiary

A `Beneficiary` represents a beneficiary that may access funds after the dormancy threshold has passed. There can’t be two beneficiaries with the same address.

```tsx
// Load from persisted data
const data = await loadData()
const beneficiary = Beneficiary.create(data)

console.log(beneficiary.type) // beneficiary
console.log(beneficiary.meta) // name and icon set by the user
console.log(beneficiary.address) // address of the beneficiary
console.log(beneficiary.dormancyThreshold) // dormancy threshold, e.g. 12 months
console.log(beneficiary.dripSchedule) // drip schedule, e.g. 5% monthly

beneficiary.setDormancyThreshold({ months: 12 }) // set dormancy threshold
beneficiary.setDripRate(0.05) // set drip rate, e.g. 5%
beneficiary.setDripSchedule({ months: 1 }) // set drip schedule, e.g. monthly
```

#### Flex Account

A `FlexAccount` represents a (currently only on-device) wallet with a specified spending limit and possibly active session key.

```tsx
// Load from persisted data
const data = await loadData()
const flexAccount = FlexAccount.create(data)

console.log(flexAccount.type) // flex-account
console.log(flexAccount.meta) // name and icon set by the user
console.log(flexAccount.address) // address of the flex account
console.log(flexAccount.publicKey) // public key of the flex account
console.log(flexAccount.privateKey) // private key of the flex account
console.log(flexAccount.spendLimit) // allowance of the flex account, e.g. 10 $-equivalent daily, or null
console.log(flexAccount.hasActiveAutoSign) // true if there is an active session key for that flex account
console.log(flexAccount.remainingAutoSignDuration) // remaining duration of the active session key or null
console.log(flexAccount.autoSignEndTime) // end time of the active session key or null

flexAccount.setSpendLimit({
	amount: 10,
	period: { days: 1 }
}) // set allowance, e.g. 10 $-equivalent daily
flexAccount.setSpendLimit(null) // remove allowance
flexAccount.enableAutoSign(dateTime) // enable auto signing until the given end time
flexAccount.clearAutoSign() // remove any active session key
```

#### SinglesigWallet

A `SinglesigWallet` represent an on-device private key.

```tsx
console.log(singlesigWallet.type) // singlesig-wallet
console.log(singlesigWallet.publicKey) // public key
console.log(singlesigWallet.privateKey) // private key
```

#### UserInteractions

`UserInteractions` is a class for a global singleton event emitter intended for user interactions (i.e. anything that requires the user to confirm something). You can trigger user interactions from anywhere in your app and handle the corresponding modals in a single location. At the moment, we provide two types of user interactions:

* `SignAndBroadcastTransactionUserInteraction` for signing and broadcasting transactions
* `InitiateWalletConnectSessionUserInteraction` for confirming wallet connect sessions

It is your responsibility to implement the corresponding modals for those interactions. Feel free to create other app-specific user interactions with `createUserInteractionType`.

Consider user interactions as global promises. You can wait for user interactions to resolve and inspect the return failure. Similarly, user interactions may fail with an error.

```tsx
const userInteractions = UserInteractions.create();

// true if there is a pending user interaction of the given type
console.log(userInteractions.hasPendingUserInteractionsOfType(SignAndBroadcastTransactionUserInteraction))
// array of all pending user interactions of the given type
console.log(userInteractions.getPendingUserInteractionsOfType(SignAndBroadcastTransactionUserInteraction))

// Somewhere in your app, you initiate the user interaction
const result = await SignAndBroadcastTransactionUserInteraction.start(txInfo)

// Somewhere else in your app, you handle the corresponding modals
if (userInteractions.hasPendingUserInteractionsOfType(SignAndBroadcastTransactionUserInteraction)) {
  // There are pending user interactions
  const message = userInteractions.getPendingUserInteractionsOfType(SignAndBroadcastTransactionUserInteraction)[0]
  showModal(message)
  // Inside your modal, you call `message.resolve()` with the response if the interaction is done.
  // OR `message.reject()` with an error
}
```

### Other classes

#### Sdk

`Sdk` is a collection of a couple of low-level helper methods that don’t have a better place, yet. We expect most of those to be used only internally or additionally exposed via the other public classes.

```tsx
const sdk = Sdk.chainId("phoenix-1")

await sdk.prepareAccount({ address: "terra..." })
```

#### Signers

There are various `Signer` classes for various use cases. See [https://github.com/obi-wallet/obi-wallet-internal/blob/db3e9f538ea1c3a5f2c62c822c9debbb37977484/libs/sdk/\_\_tests-integration\_\_/signers.ts](https://github.com/obi-wallet/obi-wallet-internal/blob/db3e9f538ea1c3a5f2c62c822c9debbb37977484/libs/sdk/\_\_tests-integration\_\_/signers.ts) for usage examples and [https://github.com/obi-wallet/obi-wallet-internal/tree/db3e9f538ea1c3a5f2c62c822c9debbb37977484/libs/mobile/src/app/modals/signature-modal](https://github.com/obi-wallet/obi-wallet-internal/tree/db3e9f538ea1c3a5f2c62c822c9debbb37977484/libs/mobile/src/app/modals/signature-modal) as an example implementation for a signature modal in React Native that handles the `SignAndBroadcastTransactionUserInteraction` using various `Signer`.

Soon, we’ll add more higher-level methods and headless React Components (i.e. without UI) to make integration easier.
