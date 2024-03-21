# 🗝️ Non/Semi-Custodial

In the blockchain ecosystem, the way users manage and control their cryptographic keys is critical to their assets' security and control. Two prevalent models that offer varying degrees of control and security are non-custodial and semi-custodial key management.

#### Custodial Keys:

Custodied keys are under the full control of a custodian. That custodian may or may not have measures in place to categorically disallow malicious activity with those keys, and may or may not (mis)manage user funds. Web3 users are often justifiably exhorted to custody their own keys.

From the business side, custodianship has a wealth of legal and regulatory concerns attached to it. Key custodians are arguably financial custodians, and have special regulatory and other liabilities.

#### Non-Custodial Keys:

**Non-Custodial Keys** imply that the user has full control and responsibility for their cryptographic keys. Users have sole control over their keys and, consequently, their assets. No third party has access to these keys.

While this model offers heightened security (as there's no central point of failure), it also places the onus of key management, backup, and recovery entirely on the user. Even experienced users often lose keys due to accident, negligence, or direct attack.

#### Semi-Custodial Setups:

**Semi-Custodial keys** are part of a hybrid model where a portion of key management involves a third party. However, when set up correctly, a semi-custodial setup offers the benefits of both custodial and non-custodial setups.

If a user loses access to their key or needs assistance in certain operations, the third party can assist, but only in conjunction with the user.

Whether the implementation uses multisig or [MPC](multi-party-computation.md), the custodied key share held by the third party cannot on its own sign transactions or access assets. The user's portion is always required, ensuring that the third party cannot unilaterally make decisions or access assets.

In addition, in the event that the third party's systems are compromised, users can update their setups to exclude the compromised keys. The attackers will be unable to take any action on the affected accounts in the meantime.

\
