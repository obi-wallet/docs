# “Unlocked Obi Theft” Attack

Most of the attack and loss vectors are remarkably different among keys. Still, a scenario in which a user’s phone is stolen with an Obi application unlocked is conceivable. It is particularly threatening if some other item such as an NFC key or Ledger is stolen along with the phone. Even Security Notifications will offer no protection since the user’s device is stolen.

In this case, the attacker would be unlikely to have access to the user’s Device Key, as every single use is guarded by OS-level biometric or passcode protection. If the attacker switches to the user’s email application, they will be unable to re-enter the Obi application without again passing the OS-level biometric or passcode protection. However, a sophisticated attacker may be able to use any combination of the following:

1. Keep the Obi application open, and thus have access to a Cloud Key.
2. Know the security answer from previous research, and thus have access to SMS, Telegram, or WhatsApp Key.
3. Use a stolen Ledger Key or NFC Key.
4. Use an observed passcode to have access to Passkey.
5. Use observed or learned Map Points.
6. Use their social key, if the attacker is also the user’s social recovery partner.

Each of these is unlikely by design, since each requires more than just stealing the phone – except, perhaps, for #1.

In order to reduce the likelihood of #1, then, using the connected Cloud Key is also guarded by biometrics (though not Device Key), as if unlocking the application.

To reduce the likelihood of #2, the user can optionally force the Obi app to never send SMS, Telegram, or WhatsApp requests – in this case, the app will switch to the relevant application with a pre-filled message which the user must send. This will require the app to be unlocked when switching back, and thus is more secure.

\#3 NFC can require a PIN code at the WebAuthN level. Ledger is less of a risk due to the PIN code.

\#4 is difficult to protect against, and would make all of the above proposed protections invalid. Users with any high value should have a secure (not numeric) passcode and take care to protect it.

A user still may be able to take certain actions in the case of #4 in order to lock the thief out of the account, even if temporarily, before funds can be stolen, especially if they have activated protections such as delays and global maximums. For example, even without their device, the user could:

* trigger a defense mode which sends an alternate SMS code. While this looks like a normal code to the thief, when entered it can instruct the app to lock or pause functionality.
* disconnect cloud accounts so that the app cannot access cloud keys
