# 📳 Security Notifications and Lockdowns

There are numerous cases in which a service may be able to detect that a user is attempting to recover a key. Using SMS keys with an incorrect security answer, requesting new simple recovery emails, and trying to brute force an entropy-boosted NFC or Map Points keys are all examples. If the attacker is using the Obi app, even more key intrusion attempts could be detected.

While the Obi security model relies on numerous types of keys, rather than making a single type 100% secure – which we judge to be impossible – it is very useful to notify a current user that one of their keys is under attack.

Meanwhile, if the recovery attempt is by the user themselves, the notifications will pose no inconvenience.

Here’s an example:

1. An attacker obtains access to a user’s phone number by socially engineering a SIM swap.
2. The attacker attempts to guess the security answer against a Twilio service endpoint.
3. Upon the first incorrect guess, the Twilio service endpoint triggers a push notification to the user associated with the given phone number. “Someone is trying to recover your Obi SMS key. If this isn’t you, tap here to lock down and recover.”
4. The user can now lock their account temporarily, giving them time to handle the key update without engaging in a race against time. This is particularly important when a SIM swap is more serious than just an Obi attack: the user can handle other consequences and fix their Obi Account at their leisure.

Note that even if the attacker guesses the security answer correctly in step #2, they are still unlikely to have account access in any secure Multikey setup, such as a basic 2-of-4 or a recommended 3-of-7.
