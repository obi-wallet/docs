# Major 2 Key Loss Vectors and Mitigations

Most of these vectors assume that the user's passkey is on a device with an old implementation. Modern passkey implementations (such as on iCloud) are highly recoverable.

* Passkey loss in a context where this also means irretrievable phone number loss (such as losing an Android phone with pre-passkey WebAuthN where that phone had the exclusive SIM card for a phone number which cannot otherwise be recovered)
  * Ultimately network recovery may still be possible. See **SMS Providers.**
* Passkey loss where mobile device is the only holder of email/cloud credentials
  * Encourage users not to follow this unsafe practice.
* Censorship from a single provider, such as Google for email and cloud (Google Drive)
  * Attempt to enforce different _providers_ for Email Key and Cloud Key.
* Theft of both single passkey device and NFC device
  * Encourage users not to carry both together. _**This is a weak mitigation and should be improved.**_
* Forgetting security answer + another single loss
  * Regularly suggest user confirm security answer or sign with a phone number key if they have not in some time.
* Forgetting map points + another single loss
  * Regularly suggest user confirm map points or sign with map points key if they have not in some time.
* Irretrievable phone number loss where both SMS Key and Telegram/WhatsApp Key are being used.
  * Discourage use of multiple phone number keys in lower key-count setups.
