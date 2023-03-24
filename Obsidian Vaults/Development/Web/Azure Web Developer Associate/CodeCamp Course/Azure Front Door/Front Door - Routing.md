#azure #az-204 

Routing is the path an HTTP request from the user will take to reach the backend service configured in Azure Front Door.
The steps below highlight the route a request may take:
1. HTTP request received from user
2. Send request to closest *Edge Location*
3. Match on Azure Front Door profile
4. Evaluate WAF rules, if there are any
5. Match to Azure Front Door route
6. Evaluate against engine rules
7. Return cached content, if there is any
8. Select the origin group
9. Select origin from within the group
10. Send request to origin's backend

There are 4 traffic routing methods available:
1. **Latency**
	- Requests are sent to the lowest latency backends acceptable within a sensitivity range
2. **Priority**
	- Requests are sent based on a user-defined number
3. **Weighted**
	- Requests distributed to backends according to weight coefficients
4. **Session Affinity**
	- Requests from same end user gets sent to the same backend (for stateful apps)