#azure #az-204 

When triggering the function with an HTTP request as a trigger.

**Authorisation level** determines what keys, if any, need to be present on the request in order to invoke the function.

Authorisation level can be any of the following:
- anonymous
	- no API key required
- function
	- function-specific API key is required (default)
- admin
	- master key is required

Set the Authorisation level in the Function's integration pane.
![[Set Authorisation Level For Function.png]]