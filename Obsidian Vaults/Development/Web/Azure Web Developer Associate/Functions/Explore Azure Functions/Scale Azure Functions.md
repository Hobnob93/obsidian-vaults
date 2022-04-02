#azure #az-204

# Scale Azure Functions
Under the `Consumption` and `Premium` plans, *Azure* scales CPU and memory resources.
It does this by adding additional instances of ==Functions host==.
Number of instances determined by number of events triggering a function.

Each instance is under `Consumption` plan is limited to 1.5GB of memory, and one CPU.
An instance of a host is the entire function app.
All functions within an app share resources within an instance and scale at the same time.
Function apps that share the same `Consumption` plan scale independently.
For `Premium` plan, the plan size determines available memory and CPU for all apps in that plan on that instance.

Function app code is stored on *Azure Files* on main storage account.
If you delete the main storage account, the function code is also lost.

## Runtime Scaling
*Functions* uses a component called the ==scale controller== to monitor rate of events.
used to determine whether to scale in/out.
Uses heuristics for each trigger type e.g. queue length and age of oldest queue message for *Azure Queue*.

The unit of scale for *Azure Functions* is the function app.
When it is scaled out, additional resources are allocated to run multiple instances of the Functions host.
As compute demand is reduced, *scale controller* removes function host instances.
Number of instances eventually scaled in to zero when no functions are running within a function app.

## Scaling Behaviours
Scaling can vary on a number of factors.
May scale different based on trigger and language selected.
Some intricacies of scaling behaviours to be aware of:
- `Maximum instances`
	- A single function app can only scale out to 200 instances
	- A single instance may process more than one message or request at a time
	- No set limit on concurrent executions
- `New instance rate`
	- For HTTP triggers, new instances are allocated no more than once per second
	- For non-HTTP triggers, new instances allocated no more than once per 30 seconds
	- Scaling is faster when running the `Premium` plan

## Limit Scale Out
Can restrict number of instances when scaling out.
Common where a downstream component like a database has a limited throughput.
`Consumption` plan scales out to 200 instances by default.
`Premium` plan scales out to 100 instances by default.
Can specify a max limit through `functionAppScaleLimit` value.
Can be set to `0` or `null` for unrestricted; or a valid value between 1 and app maximum.

## Azure Functions Scaling in an App Service Plan
Using *App Service* plan, you can manually scale.
You do this by adding more VM instances.
You can enable autoscale, though will be slower than elastic scale of `Premium` plan.