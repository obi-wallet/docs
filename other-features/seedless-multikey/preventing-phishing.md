# 🎣 Preventing Phishing

The most sophisticated multi-key setup in the world cannot protect a user who intentionally signs a bad transaction.

Obi has three protections which can reduce the likelihood of phishing attacks draining a user’s wallet:

1.  **Escalation**: Users are recommended to create spend-limited, permissioned keys (flex accounts) on device which can only take actions up to a certain recurring amount. Any higher-spending or unknown actions will require full multikey threshold signing, indicating that the transaction is not trivial.

    Read more:
2. **Security Limits**: Users can establish a [Global Transaction Limit (Sanity Limit)](../../roadmap-features/global-transaction-limit-sanity-limit.md). Any transaction over this amount will be disallowed until the limit is lifted.
3. **Mandatory Delays**: Transactions of certain kinds, involving certain contracts or tokens (including specific NFTs), or above certain set values can trigger a mandatory delay, where the transaction is queued and can only be completed once the delay has completed. Attacks which rely on tricking the user to sign would then have to also trick the user to confirm later.
