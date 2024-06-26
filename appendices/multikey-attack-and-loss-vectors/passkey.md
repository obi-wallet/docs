# Passkey

can be lost if:

* the user loses access to their account (Apple, Windows, Google) or all devices (especially if on Android with a pre-passkey webAuthN implementation) and loses all recovery paths
* the user loses access to encrypted information by irrecoverably forgetting the passcode
* the user intentionally resets all devices or deletes their account

Non-duress attacks include:

* zero-day exploits affecting the secure hardware
* physical theft of a device, combined with a biometric workaround or an insecure passcode\
  NEW: Apple has included an upgraded security model which avoids an attacker being able to take over a device and Passkeys simply by knowing the passcode. Obi will recommend this to users, as well as any Android equivalent.
