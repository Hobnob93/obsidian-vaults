#azure #azure-wda 

# Route Traffic in App Service
By default, all client requests to prod URL go to `http://<appname>.azurewebsites.net`.
You can route a *portion* of the traffic to another slot.
Useful if you need user feedback for a new update which isn't ready for production.

## Route Production Traffic Automatically
1. Go to app's ==Resource== page and selected ==Deployment Slots==.
2. In `Traffic %` column, specify amount of traffic you want to route.
3. Make sure to `Save`.

The specified percentage of clients will be *randomly* routed to the non-production slot.

Once automatically routed, the client is "==pinned==" there for the duration of the session.
The slot the session is bound to is stored in the `x-ms-routing-name` cookie in HTTP headers.
A request routed to "staging" would have the cookie `x-ms-routing-name=staging`.
A request routed to production would have the cookie `x-ms-routing-name=self`.

## Route Production Traffic Manually
*App Service* can route traffic to a specific slot.
useful when you want users to be able to opt in or out of a beta app.
You can use the query parameter `x-ms-routing-name` to direct them.
Once accessing the link, they will be "==pinned==" for the session as with the automatic approach.

By default, new slots are allocated 0% of the traffic.
users can access staging slot manually but they won't be redirected automatically.