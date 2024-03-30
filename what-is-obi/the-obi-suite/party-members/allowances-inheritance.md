# Allowances: Inheritance

Inheritance works like a spend limit, but with some additional notes:

* Inheritance only activates after a dormancy period – a customizable minimum amount of time during which the main account must be inactive, indicating that something has happened to its owner.
* Inheritance spend limits are likely set as a percentage of assets – such as 5% per month – instead of numerical or dollar totals. If the `spendlimit` field is `[]`, 100% is available immediately.
* A “full control” time sets when beneficiaries receive full control of the Obi Account, unlocking any account assets which could not meaningfully be provided in a drip, as well as cross-chain signing potential.
* Setting an Inheritance Address in the User Interface
  * Go to the Accounts tab.
  * Create a new Inheritance Account.
  * Enter the address which will inherit funds. It can be an Obi Account or any other kind of address.
  * Set the parameters for the inheritance:
    * **Dormancy Period**: Your account must have no activity for this time period in order for inheritance to be claimable.
    * **Drip**: Your selected percentage of assets will be available each selected time period (for example, 5% per month). Rollover is not yet implemented.
    * **Full Control**: The recipient will receive full control of your account and be able to take any action on it after this amount of time has passed.
    * Note that any owner activity on the account will restart the Dormancy Period – even if inheritance is currently active.
  * Confirm your settings.
