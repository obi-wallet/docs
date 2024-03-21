# 🔌 Obi SDK

Obi features can be integrated into existing wallet applications.

However, Obi SDK allows Obi Accounts to be easily and immediately integrated into web applications – with modules including onboarding, Multikey, Flex Accounts, and Passport – without requiring end users to install special Obi apps or extensions.

This offers several advantages. UX improves and onboarding completion rates increase when users do not need to install a separate app or extension.

In addition, white-labeled Obi accounts avoid the risks of many current third-party applications. In particular, a wallet or a single application using it can attract negative attention, leading regulators or app store gatekeepers to block features – negatively affecting _**all**_ users and applications using that wallet. For example:

[Apple Removes Trust Wallet from Its App Store. Here's Why | Bitcoinist.com](https://bitcoinist.com/apple-removes-trust-wallet-from-its-app-store-heres-why/)

[Uniswap Wallet Was Rejected From the App Store, Here’s Why](https://www.btcc.com/en-US/coin-news/market-updates/uniswap-wallet-was-rejected-from-the-app-store-heres-why)

Even when used without an extension or Obi app, Obi accounts can still be universal, thanks to the coincidence of multiple factors. If a user creates an account in one app, they can quickly and easily use it in others.

Obi SDK can currently be implemented in two ways:

* Using an easy, customizable webview. Onboarding, wallet functionality, account abstraction settings, and transaction signing are all handled in a white-labeled, modal iFrame which the website/game developer can pass some theming and some chain options. The developer has access to easy transaction and information requests. This approach can also be used directly in games. Using webview plugins, Unity targets are supported; all targets except WebGL have advanced 3d support for highly custom in-game wallet placement if desired.
* Using headless (no UI) scripts loaded in iFrame which expose certain functions to the developer: `createAccount`, `getPubkey`, `getAddress`, `signArbitrary`, `signAndBroadcast`. The EVM- or Cosmos-compatible chain can be specified. (Currently, users must open an Obi webview deployed using method #1, or such an Obi deployment elsewhere offered by a different application, in order to customize their Multikey beyond `createAccount` defaults and to use more advanced account abstraction such as restricted session keys.)

#### Glossary

* **Package**. A package refers to an existing nx app (`apps/*` directory) or nx lib (`lib/*`) in our existing monorepo. Our tooling enforces the absence of relative imports between different packages, enabling us to publish our packages when needed (e.g. to npm or GitHub packages). We can also split them from the monorepo in the future.
* **Platform.** We consider two platforms for our use case: native (i.e. usable in a React Native context) and web (i.e. usable in a web browser or a Unity game webview). Some packages are platform-specific while others aim to be platform-agnostic. Some of our more recent code hasn’t been tested for the react native platform, as web has been the focus.
* **Opinionated**. Much of our existing code is “opinionated” and tailored to our specific technology stack, which includes React, MobX, and TanStack Query, among others. Through the planned packages, we’d like to design some packages to have fewer dependencies so that they are more generally usable. Others (mostly those that are easier to use) are tied to a specific choice of technology.

The current separation of packages strives to balance generalizability and easy usage based on our current knowledge of possible SDK users.

The planned packages for external usage are:

* `@obi-wallet/sdk`: Platform-agnostic SDK that only contains logic. Strives to be as un-opinionated as possible. Apart from network-specific (e.g. `@terra-money/feather.js`), cryptographic (e.g. `sec256k1`) and helpers (e.g. `ramda`) dependencies, it uses `zod` for the validation of external input (e.g. blockchain responses) and to make data structures that are intended to be persisted migratable for future changes.
* `@obi-wallet/headless-ui` (planned): Platform-agnostic React components without any UI. This is intended for customers that want a completely custom UI but are fine with using “our” technology stack. So this will most likely also include dependencies like MobX & TanStack Query.
* `@obi-wallet/obi-web` (planned): Obi Standalone for the web platform. So this will be a React web app, React component, browser extension, or something similar. It will probably also expose some kind of API / interface that makes it easy to integrate into the existing web apps of our clients (e.g. using an iframe).

### Easy Start

_Easy Start will be available soon_. _Obi is still in a co-development stage with clients._

```json
import { obi, Obi } from "@obi-wallet/obi-web";

...

<Obi config={env.CONFIG_URI} />

const service = "spotify.eth";

const result =
  await obi.try_subscribe(
    service, 
    "15.0 SPOT"
  );
```
