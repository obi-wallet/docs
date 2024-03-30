# 🔒 Multikey

_**Note that “key” is used generally, and may in different contexts refer to an actual private key for a network account, an MPC key share, or even an encryption key used by a client app or network to securely hold either of the former. On the whole, security and other considerations remain the same for all definitions.**_

Obi Multikey assembles threshold setups from four key sources: the classic three [listed](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.1800-17.pdf) repeatedly in NIST multi-factor authentication standards, and an optional third-party component.

1. Something you know
2. Something you have
3. Something you are
4. (Optional) Something a third party has

Some of these source types can be defended by others in compound setups. For example:

* a key deliverable over SMS (something you have, but which can be taken in a SIM swap attack) can be bolstered by a security answer (something you know)
* a device key stored in a modern secure enclave (something you have) is protected by biometrics or a password (something you are or know)
* a map points key (something you know) is protected by additional brute-forceable entropy (something you have but can also brute-force recover if you know your points)

Obi Multikey can expand to include any imaginable key type. At the time of this writing, the options are: Device (Secure Element or Keychain), Cloud (any major provider), SMS, Telegram, WhatsApp, Social Recovery, Email Recovery (simple or ZK), Ledger Hardware, Map Points, NFC Device, Network MPC, and Social Login.

OTP Authenticators (Google Authenticator, Authy) are being considered as a key type.

Also, voice authentication and other biometric keys are being considered. Voice authentication would require an authenticating service as it tends to be too fuzzy to deterministically generate a keypair on demand; [Obi Service Providers](../../roadmap-features/obi-service-providers/) can provide this service in a later version.

### Security by Diversity

Multikey is protected primarily by its diversity. Each key has distinct attack and loss vectors, making loss unlikely and attacks infeasible. See full discussion of the various keys and attack scenarios in [Appendix: Multikey _**Attack & Loss Vectors**_](../../appendices/multikey-attack-and-loss-vectors/).

### Threshold

Multikey users are protected from attacks targeting one or even two keys, since a minimum threshold is required in order to sign messages. Depending on the implementation, threshold signing is realized via Multi-Party Computation (in which case key source entropy encrypts the MPC shares) or via native or contract multisig.

For convenience, addresses can receive spend-limited, time-limited, or use-count-limited permissions on the parent account. Anything exceeding these limits triggers threshold escalation as appropriate.

### Updatability

Using either proxy updating (multisig) or rotation of shares (MPC), Obi Multikey can replace any compromised or lost keys with new ones, restoring the account’s original level of security. Regular health checks and a **Security Notifications** service serve to keep the user informed of any keys which are at risk.

Updatability also allows users to improve the security of their accounts as appropriate. Entities using Obi SDK can use progressive onboarding to improve user acquisition and security in balance. For example, onboarding can set up only a 1-of-2 multisig at first, with negligible onboarding time. At a later time, the application can prompt users to move to 2-of-4 if assets are added, and to 3-of-6 or 3-of-7 if significant value enters the account.
