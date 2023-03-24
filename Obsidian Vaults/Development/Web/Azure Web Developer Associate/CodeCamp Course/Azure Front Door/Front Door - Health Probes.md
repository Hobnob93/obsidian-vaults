#azure #az-204 

Origin group health probes (a.k.a. health checks) allow you to ping a backend to determine if a healthy response is returned.
A healthy response is determined by HTTP status code 200 (OK) being returned.

When a backend is considered unhealthy traffic will not be routed to it.
Instead, traffic is routed to other healthy origins (if others are configured).

When configuring, you can choose:
- Whether it's enabled
- The path to check
- The protocol to use when checking
- The probe method to use
- The interval (in seconds)