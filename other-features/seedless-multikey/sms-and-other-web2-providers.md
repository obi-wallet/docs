# 📲 SMS and Other Web2 Providers

The MVP of Obi Multikey uses Twilio for SMS keys. This is a possible point of failure, vulnerable to:

* Twilio Terms of Service updates
* Legal actions
* Compromised Twilio staff
* Compromised Twilio infrastructure
* Carrier rate limiting or blocking
* SMS incompatibilities on certain networks

To remedy this, first, Obi will maintain fallback providers other than Twilio.

Once ready, Obi Service Providers will provide this service instead, preventing Obi as a company or Obi staff from being a single point of failure. See [Obi Service Providers](../../roadmap-features/obi-service-providers/).

Similar improvement strategies are planned for other key types requiring web2 services, such as Telegram, WhatsApp, and voice authentication.
