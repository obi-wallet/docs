# 💂 Anti-Cheat Sign-in

Session keys are temporarily authorized to act. Session keys can be limited by other rules, as well, such as allow/block lists and spend limits, and are not able to take admin actions such as updating owners, extending their own lifetime, or creating other permissions. They can, however, destroy themselves.

#### Example Use Cases

* “Save password for 30 minutes” functionality on a device. After signing once with their Multikey, users can transact without needing to sign again until the session key expires, or until they lock their device.
* Gaming sessions. Users can sign once at the beginning of a play session, rather than upon taking any action.
* Setting a Session Key in the User Interface (Transaction Screen)
  * Coming to [obi.money](https://obi.money) Early Access very soon
  * Perform any transaction
  * Select “Auto sign transactions on this device for the next 30 minutes”
  * Your device now securely contains an active session key
* Setting a Session Key in CLI/Code: Session keys are no longer their own explicit concept in the code and no longer have their own gatekeeper. Instead, simply set an `expiration` on any other kind of rule or rules.
