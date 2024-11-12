# Quickstart: Using Obi

### _Building with Obi? See the Builder's Intro:_ [builders](builders/ "mention")

### Creating an Account

Obi allows the simplest account creation of any wallet. Not only do you simply use a Passkey – which some other wallets do, too – you only have to do this once in order to have an account on all chains.

Ethereum chains, Cosmos chains, [Bitcoin, Solana, Move](#user-content-fn-1)[^1] – you name it.

To make an account, simply click **Passkey** in the account wizard.

If you don't like Passkeys or are using a system without modern Passkey support, you can select **Cloud Key** as an alternative primary key. Google Drive is currently supported, with more providers coming soon.

**CAUTION: Do not use Incognito or Private mode for this step, or your Passkey may not be saved by your local system. This may make wallet recovery difficult later.**

<figure><img src=".gitbook/assets/Screenshot 2024-03-22 at 7.35.54 PM.png" alt=""><figcaption></figcaption></figure>

Your device will prompt you to authenticate with your local Passkey – meaning Face ID, Touch ID, Windows Hello, or another typical system prompt.

### **Buying Assets with Bank/Credit Card**

Kado on-ramping is directly integrated into the Obi dashboard. You can automatically obtain assets directly to your Obi account. You will need to give some information to Kado, including KYC (Know Your Customer) information. Obi cannot observe this information in any way.

To begin, simply go to the Buy Crypto tab and interact with the Kado interface.

<figure><img src=".gitbook/assets/Screenshot 2024-03-22 at 8.01.32 PM.png" alt=""><figcaption></figcaption></figure>

### **Receiving Assets**

To receive crypto assets such as tokens and NFTs, use the **Receive** button and **Receive Tokens**, then select the chain you'd like to receive on.

For Ethereum and EVM chains such as Arbitrum, Optimisim, Polygon, Base, Avalanche, and Binance Smart Chain, your receive address is the same no matter what network you're receiving on.

For Cosmos chains, your address will be similar, but not identical.

![](<.gitbook/assets/Screenshot 2024-03-22 at 7.39.02 PM.png>)![](<.gitbook/assets/Screenshot 2024-03-22 at 7.39.54 PM.png>)

### **Sending Assets**

You can send assets to other addresses using the **Send** button and **Send Tokens** tab. Only addresses are currently supported – name services such as ENS will be supported soon.

Remember to include a memo if needed. Exchange deposits in particular often require transaction memos to identify your deposit.

### Sending and Signing

When you sign a transaction, including a send, you will see the signature prompt.

<figure><img src=".gitbook/assets/Screenshot 2024-03-22 at 7.44.03 PM.png" alt=""><figcaption><p>After you add more keys, they will be shown here. With a single-passkey wallet, "Approve" is all you need to click.</p></figcaption></figure>

### Connecting to Web3 Applications with WalletConnect

You can connect to a web application in another browser tab or on another device using WalletConnect. The flow for doing this can vary; if you need to pretend to be a Cosmos wallet in order to coax an app to show you a connection link, select the Keplr Mobile option.

Keep your browser tab open during your session for the easiest experience.

<figure><img src=".gitbook/assets/Screenshot 2024-03-22 at 7.51.43 PM.png" alt=""><figcaption></figcaption></figure>

Some applications provide Obi connection buttons directly.

When you start transactions in the connected application, a signing prompt will appear in your Obi web browser tab, allowing you to complete the transaction.

### Enabling Extra Life

Extra Life's advanced non-custodial account recovery is in testing and will be available in the UI soon.

[^1]: Some chains are not yet available in the public UI. But as soon as they're released, you'll have immediate access to them.
