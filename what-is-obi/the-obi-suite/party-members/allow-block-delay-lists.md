# Allow/Block/Delay Lists

The message gatekeeper can inspect a message to see if it matches a current Authorization, Block, or Delay order. Contract address, message URL, WASM action name, and fields can all be filtered on.

#### Examples

* Allow any action on a specified contract with a specified `token_id` (a single NFT).
* Allow any trades on specified LP contracts as long as the `max_slippage` is under a set value.
* Disallow the `burn` action on all contracts.
* Delay any action with a specified `token_id` (a high-value NFT).

Creating an Allow Authorization using CLI/Code:

<pre><code><strong>{ add_abstraction_rule: {
</strong>    new_rule: {
    	actor: "&#x3C;ADDRESS>",
    	ty: "allow",
    	main_rule:
    	    [["allow", { allow: {
<strong>                "identifier": 0  // usually unspecified
</strong>		"actor": "&#x3C;ADDRESS>"  // optional
	    	"contract": "&#x3C;CONTRACT_ADDRESS">  // optional
      		"message_name": "MsgExecuteContract"  // optional
      		"wasmaction_name": "transfer"         // optional
      		"fields": [                           // optional
		    ["captain","picard"],
		    ["strategy","engage"]
		]    
	    }}]],
	sub_rules: [] // not yet supported for this main_rule type
    }
}}
</code></pre>

