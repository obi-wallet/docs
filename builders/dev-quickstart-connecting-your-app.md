# Quickstart for App Developers: Integrating an Obi Web Wallet via WalletConnect

This guide is intended for application developers who wish to connect their applications to an Obi web-based wallet using WalletConnect. By following this guide, you can enable users to seamlessly onboard and interact with your app on any blockchain, using a secure and recoverable non-custodial account.

This guide focuses on how to generate and handle WalletConnect URIs that will allow users to establish connections with our wallet.

## Quickstart Code Snippet: Enable Obi connection in your app

```typescript
import WalletConnect from "@walletconnect/client";

const connector = new WalletConnect({
  bridge: "https://bridge.walletconnect.org",
});

if (!connector.connected) {
  await connector.createSession();
}

const uri = connector.uri;

// Redirect the user to the web wallet with the URI
const walletConnectUri = encodeURIComponent(connector.uri);
const deepLink = `https://obi.money/wallet-connect/${walletConnectUri}`;

// Open the link in a new tab
window.open(deepLink, '_blank');
```

## Understanding the WalletConnect URI

WalletConnect uses a URI scheme to initiate connections between applications (dApps) and wallets. This URI contains all the necessary information to establish a session and communicate securely.

**Example WalletConnect URI:**

```
wc:<topic>@<version>?bridge=<bridge_url>&key=<key>
```

To generate a WalletConnect URI, you can use the WalletConnect client libraries.

### Step 1: Install WalletConnect Client

For JavaScript/TypeScript applications:

```bash
npm install @walletconnect/client
```

### Step 2: Initialize the WalletConnect Client

```typescript
import WalletConnect from "@walletconnect/client";

const connector = new WalletConnect({
  bridge: "https://bridge.walletconnect.org",
  qrcodeModal: null, // We recommend against forcing a QR code default, as users may be using a desktop wallet
});
```

### Step 3: Create a Session and Generate the URI

```typescript
if (!connector.connected) {
  await connector.createSession();
}

const uri = connector.uri;
```

### Step 4: Present the URI to the User

You can display the URI as a link, automatically open the link when the user clicks an Obi button or text, or show a QR code.

We recommend against forcing a QR code default, as users may be using a desktop wallet. However, it is the easiest way to accomodate users preferring to use Obi on a mobile device.

**Example deep link:**

```
https://obi.money/wallet-connect?uri=<encoded_walletconnect_uri>
```

Encode the URI component properly to ensure it is correctly parsed by the web wallet.