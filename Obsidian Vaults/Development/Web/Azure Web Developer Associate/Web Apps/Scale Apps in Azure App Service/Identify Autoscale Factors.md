#azure #azure-wda

# Identify Autoscale Factors
Effective scaling ensures sufficient resources always available to handle large volumes at peak times.
It also needs to manage costs when the demand drops.

## Autoscaling & the App Service Plan
Autoscaling is a feature of the [[Examine Azure App Service Plans|App Service Plan]] used by the web app.
When the web app scales out, new instances are started based on hardware defined by the service plan.

To prevent ==runaway scaling==, the plan has an instance limit.
Plans in higher tiers have higher limits.
Not all tiers support autoscaling, too!

## Autoscale Conditions
These indicate how to autoscale, and there are two options:
1. Scale based on a metric
2. Scale to a specific instance count based on a schedule

Can combine both in the same autoscale condition to scale out incrementally, if desired.
For example; scale out if number of requests exceeds a threshold, but only at certain times of the day.

Can create multiple autoscale conditions for different schedules and metrics.
*Azure* will scale when **any** of these conditions apply.
*App Service Plans* have a **default** condition that will be invoked if no other conditions are applicable.
This default condition is always active and doesn't have a schedule.

## Metrics for Autoscale Rules
An autoscale rule specifies a metric to monitor, and how autoscaling should responded.
The metrics you can monitor for a web app are:
- `CPU Percentage`
	- An indication of CPU utilisation across **all instances**
	- A high value shows instances are becoming ==CPU-bound== which can delay processing requests
- `Memory Percentage`
	- Captures memory occupancy across all instances
	- A high value indicates free memory could be running low, and instances could fail as a result
- `Disk Queue Length`
	- Measures number of outstanding I/O requests across all instances
	- A high value could indicate disk contention
- `HTTP Queue Length`
	- How many clients are waiting for processing
	- If this number is high, clients could start failing with a `408` error (timeout)
- `Data In`
	- Number of bytes received across all instances
- `Data Out`
	- Number of bytes sent by all instances

Can also scale based on metrics for other Azure Services, such as *Service Bus Queue* length.

## How an Autoscale Rule Analyses Metrics
It analyses trends over time across all instances.
Analysis is a multi-step process.

Firstly, an autoscale rule aggregates values retrieved for a metric for all instances across a period of time called a ==time grain==.
Each metric has its own intrinsic time grain. but in most cases it is ==1 minute==.
The aggregate value is known as the ==time aggregate==.
The options available are `Average`, `Minimum`, `Maximum`, `Total`, `Last`, and `Count`.

Secondly, a further aggregation of the *time aggregate* is calculated over a longer, user-specified, time period known as the ==duration==.
This is because *1 minute* is too short to notice lasting changes or trends.
The minimum duration is 5 minutes, with an aggregate done on the last *x* values calculated for the *time grain* (where *x* is duration in minutes)

## Autoscale Actions
An action is performed when a metric has crossed a threshold for an autoscale rule.
A scale-out *increases* the number of instances.
A scale-in *decreases* the number of instances.
Scale-out actions typically use the `greater than` operator to compare metric to threshold.
Scale-in actions typically use the `less than` operator to compare metric to threshold.
An action can also set the instance count to a specific amount, rather than incrementing or decrementing.

Actions have a ==cooldown== period, specified in minutes.
During this time, the scale rule won't be triggered again.
This allows the system time to stabilise between scaling events.
The minimum cooldown is 5 minutes.

## Pairing Autoscale Rules
Plan for scaling in when workload decreases.
Consider creating rules in pairs for a given metric; one for increasing scale and one for decreasing.

## Combining Autoscale Rules
A single *condition* can contain several *rules*.
The autoscale rules within a condition don't have to be directly related.
You could define the following four rules in the same condition:
- If `HTTP Queue Length` > 10, scale out by 1
- If `CPU Utilisation` > 70%, scale out by 1
- If `HTTP Queue Length` == 0, scale in by 1
- If `CPU Utilisation` < 50%, scale in by 1

The autoscale **out** action will be performed if **any** of the scale out rules are met.
The autoscale **in** action will be performed if **all** of the scale in rules are met.
if you want to scale in when a specific rule is met, it needs to be in its own condition.