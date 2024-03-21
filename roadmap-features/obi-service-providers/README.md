# 🌐 Obi Service Providers

Some Obi Multikey keys currently rely on services or accounts operated or held by Obi:

* SMS providers (Twilio)
* Telegram bot
* WhatsApp business license
* CloudFlare/AWS/Netlify/Heroku services which aid recovery or boost entropy
  * Note that services are spread across providers to avoid single points of failure

These represent points where a compromised Obi Technologies could potentially be better positioned to execute an attack on a user, or where a shut down Obi Technologies could reduce users’ available paths to recovery and make certain key types impossible to use.

To correct this, a network of service providing nodes on a network will be incentivized to offer the above services, and potentially more. These can include other key types, such as fuzzy biometric authorization, but could also provide other services to smart contracts generally. Examples include:

* IPFS pinning
* Oracles (web and blockchain)
* Transaction batching or scheduling
* Off-chain compute

Fees from Obi Accounts will go to these service providers, or, more directly, a marketplace of services can be provided to contracts and bought directly when used or as a regular quota.

The fees will be distributed to service providers, and potentially to other participants or structures in future economic designs.

Entities who wish to ensure uptime for their users without relying on a third-party network of service providers can add their own in-house providers.

[Incentivizing Service Providers](https://app.gitbook.com/o/HJYdCbcd7RYYZKW0R4O4/s/KAhF9NG15l7CNPFvVH7w/overview/obi-service-providers/incentivizing-service-providers)
