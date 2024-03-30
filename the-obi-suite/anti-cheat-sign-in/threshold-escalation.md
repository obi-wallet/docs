# Threshold Escalation

Users of digital assets and identities suffer from constant vulnerability to phishing attacks, wherein they are prompted to connect their identity to a malicious website.

Obi Accounts provide several phishing protections to users, including threshold escalation.

#### Case 1: Spend-Limited Usage

A reasonable daily spend limit is set by the user: for example, $500 cumulative per day.

The user can now interact with websites and sign with the authorized single key. If the single key is somehow compromised, the maximum that the attacker can spend is $500 per day, until the original user disables its permission.

If a connected website attempts to get the user to sign a transaction which spends more than $500 per day, this single key will not be enough. In addition, if some unknown transaction type is attempted which does not apply to spend-limited wallets (native asset send, ERC-20 or cw20 transfer, stake, claim staking rewards), this single key will not be enough.

In this case, the wallet automatically escalates the signing type required to full Multikey. Thanks to both the interface’s depiction of this escalation and the fact that the user now must sign with multiple keys, the user is forced to consider that this is a significant action. If the user did not expect a significant action – they were, for example, only attempting to mint a $5 NFT or pay for an item under $500 – then this will alert them that the site is doing something unexpected.

#### Case 2: Time-Limited Usage

A user sets a session key which can take any action for 30 minutes.

Session keys can be restricted by other rules, for example spend limits as above, but for this example, the user enables “unlocked” permissions for the session key.

Now, the session key can take any action on a connected website. This is not as safe as case #1, but some protections still remain:

* the website cannot try to create new permissions or modify existing permissions
* the website cannot speed up transactions which match a mandatory delay filter
* the website cannot update the account’s owner
