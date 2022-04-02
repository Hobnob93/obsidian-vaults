#azure #az-204 

# Examine Autoscale Factors
Autoscaling can be triggered according to a schedule, or by a resource usage threshold.
E.g. scaling could occur if CPU utilisation grows, memory capacity increases, number of incoming requests is surging, or a combination of factors.

## What is Autoscaling?
It's a cloud system or process that adjusts resources based on current demand.
Performs scaling ==in== and ==out==.

### Azure App Service Autoscaling
*Autoscaling* in *Azure App Service* monitors resource metrics of a web app.
Detects situations where additional resources are required.
Ensures those resources are available before the system becomes overloaded.

It responds to changes in the environment by adding or removing web servers and balancing the load between them.
It ==does not== have any effect on CPU power, memory, or storage capacity of the servers powering the app; it only changes the ==number== of servers.

### Autoscaling Rules
*Autoscaling* makes its decisions based on defined rules.
A rule is a threshold for a metric.
When a threshold is crossed, the autoscaling triggers.
It can also deallocate resources when workload reduces.

Define autoscale rules ==carefully==!
A ==DoS attack== will cause a huge surge in incoming requests; trying to handle that will be fruitless and expensive.
These requests aren't genuine, and should be discarded rather than processed.
A better solution is to implement detection and filtering of requests during attacks before they reach the service.

## When Should Autoscaling be Considered?
Autoscaling provides elasticity for services.
A suitable solution for when you can't predict workload in advance.
Also useful if workload is likely to vary by date or time.

It improves availability and fault tolerance.
It can help ensure client requests to a service won't be denied either due to an overwhelmed server, or a crashed application instance.

If app performs heavy processing as part of each request, autoscaling **might not** be an effective approach. Manually scaling up might be necessary instead, as a small number of requests could exhaust a single instance.

It's not the best approach for long-term growth.
Autoscaling has an overhead associated with monitoring resources and whether to trigger scaling.
If you can anticipate the rate of growth, manually increasing the instance count might be a more cost-effecting approach.

Number of instances is also a factor.
You may expect only a few instances most of the time, however, the service will always be susceptible to downtime or lack of availability whether autoscaling enabled or not.
The fewer the number of instances initially, the less capacity for handling increased workload while autoscaling spins up more instances.