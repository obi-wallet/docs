# ✋ Global Transaction Limit (Sanity Limit)

The global transaction limit is an optional single-transaction maximum value (unlike spendlimits, which are cumulative and recurring) that applies to all transactions, regardless of the permission being used to authorize them.

This provides a final line of defense against the following cases:

1. An exploit in the spendlimit gatekeeper
2. A maliciously created spendlimit authorization
3. An unlocked (no restrictions) session key connecting to a malicious website
4. A temporarily stolen, unlocked device

Only the user’s full Multikey can raise or remove the global transaction limit. This transaction may be subject to a delay – increasing safety, but lowering convenience.
