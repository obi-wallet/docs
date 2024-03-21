# ♻️ Multi-Party Computation

**Multi-Party Computation (MPC)** is a cryptographic protocol enabling multiple entities to jointly compute a function over their inputs, while ensuring each party's input remains private.

When used by a single user, the "entities" can be different keys and systems which that user uses to store or otherwise secure shares of their private key, without needing to rely on a native or contract-based on-chain multisig.

The term **Threshold Signature Scheme** is not exactly synonymous, but as far as relates to smart account owner verification, the two acronyms are often used interchangeably. A threshold signature scheme is one in which _x-_of-_n_ (such 2-of-3, or 6-of-10) signatures are needed in order for a complete signature to be created. (By convention, 2-of-3 is threshold 1. 6-of-10 is threshold 5.)

This distribution ensures the user isn't overly reliant on a singular key, thereby reducing risks linked to key misplacement or theft.

#### Dealing and Rerolling in MPC:

1. **Dealing Process:** The dealing ceremony is the initial division of the cryptographic key into shares. In a multi-party setup, the participant obtains their designated share, but the original key's composition remains undisclosed and unknown. Many MPC algorithms are vulnerable to malicious parties in the dealing process, such as the widely used gg20. In single-user applications, this concern is markedly less of a concern.
2. **Rerolling Process:** If a key share becomes vulnerable or is lost, the rerolling mechanism creates a fresh set of shares, all while keeping the original key unchanged. This way, the adversary, if any, loses any progress towards a complete set of shares, since the shares now in use cannot be used in combination with the share stolen by the adversary.

**Attacking MPC:**

In addition to the compromised dealing ceremony mentioned above, some algorithms can be attacked with malicious signing requests which have obtained a key share and proceed to initiate signing rounds and observe the results (see Fireblocks nofiticaions on [Lindell17](https://www.fireblocks.com/blog/lindell17-abort-vulnerability-technical-report) and [gg18/gg20](https://www.fireblocks.com/blog/gg18-and-gg20-paillier-key-vulnerability-technical-report/)).

In Obi's implementation, a signing request cannot even be made by an unauthorized party – the requested must have some active [abstraction rule](../smart-account-architecture/flex-accounts/) created by the account owner Multikey which allows them to request a signature. However, Obi still has an upgrade to [cggmp](https://github.com/webb-tools/cggmp-threshold-ecdsa) on its roadmap.
