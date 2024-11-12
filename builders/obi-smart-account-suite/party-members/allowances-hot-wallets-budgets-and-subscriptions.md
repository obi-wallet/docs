# Allowances: Hot Wallets, Budgets, and Subscriptions

A [spend limit](../../../glossary.md#spendlimit) has multiple uses. Obi [signet](../signet/ "mention") can assist in signature finalization for an authorized user if a spend limit [abstraction rule](../../../glossary.md#abstraction-rule) applies.

### Examples:

* A customizable daily spend limit of $100 for the user’s primary Passkey, allowing easy quick signing on mobile device without needing to escalate to the whole _x-of-n_ Multikey. This provides the added benefit of a “phishing shield,” where transactions such as minting and small sends should not trigger escalation, and escalation is a warning sign that the connected site is not acting as expected.
* A budget of $1500 per month for a contractor. This does not need to be topped up or manually paid out, as the contractor has permission to spend (withdraw) this amount per month without needing additional action from the Obi Account.
* A subscription of $20 per week. The provider account has permission to withdraw that amount per week. The user can cancel at any time, but otherwise does not need to take any regular action to keep the subscription.
* Creating an Allowance in the User Interface
  * Party Members is coming to the [obi.money](https://obi.money) interface soon.
* Managing Allowances using CLI/Code
  *   Manually: Retrieve your user account's state with the query `"{"gatekeeper_contracts": {}}`. Then, interact with the returned `user_state` contract address as follows:

      * Adding a new allowance:

      ```javascript
      { add_abstraction_rule: {
      	new_rule: {
          		actor: "<ADDRESS>",
          		ty: "spendlimit",
          		main_rule:
          			[["spendlimit", { spendlimit: {
      				address: "<ADDRESS>",   // address with permission to spend
      				cooldown: 0,            // time remaining until reset
      				period_type: "DAYS",    // MONTHS also available
      				period_multiple: 7,
      				spend_limits: [{
      					denom: "<ASSET OR CONTRACT ADDRESS>",
      					amount: 100000000,    // The recurring limit
      					current_balance: 0,
      					limit_remaining: 100000000
      				}],
      				offset: 0,              // Secs after midnight (1st of month) to reset
      				inheritance_records: [] // used only for Inheritance type (below)
      			}}]],
      		sub_rules: []
      	}
      }}
      ```

      * Querying current allowances (optionally for a particular address):

      ```jsx
      {
      	abstraction_rules: {
      		actor: "<ACTOR_ADDRESS>"  //optional
      		ty: ["spendlimit"]  //multiple types allowed, or [] for all
      	}
      }
      ```

      * Removing an allowance (note that currently this will also remove any inheritance on the address):

      ```jsx
      {
      	rm_abstraction_rule: {
      		id: <RULE_ID>
      	}
      }
      ```

      * Updating an allowance to double the limit:

      ```jsx
      {
      	upsert_abstraction_rule: {
      		id: <RULE_ID>,
      		updated_rule: {
      			actor: "<ADDRESS>",
      	    		ty: "spendlimit",
      	    		main_rule:
      	    			[["spendlimit", { spendlimit: {
      					address: "<ADDRESS>",   // address with permission to spend
      					cooldown: 0,            // time remaining until reset
      					period_type: "DAYS",    // MONTHS also available
      					period_multiple: 7,
      					spend_limits: [{
      						denom: "<ASSET OR CONTRACT ADDRESS>",
      						amount: 200000000,    // The recurring limit
      						current_balance: 0,
      						limit_remaining: 200000000
      					}],
      					offset: 0,              // Secs after midnight (1st of month) to reset
      					inheritance_records: [] // used only for Inheritance type (below)
      				}}]],
      			sub_rules: []
      		}
      	}
      }
      ```
