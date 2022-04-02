#azure #az-204

# Examine Azure App Service Plans
In *App Service*, an app always runs in an ==App Service Plan==.
It defines a set of compute resources for a web app to run.
One or more apps can be configured to run on same computing resources (in same *App Service plan*).
[[Azure Functions]] has the option of running in an *App Service plan*.

Each *App Service plan* defines the following properties:
- Region (`West US`, `East US`, etc.)
- Number of VM instances
- Size of VM instances (`Small`, `Medium`, `Large`)
- Pricing Tier (`Free`, `Shared`, `Basic`, `Standard`, `Premium`, `PremiumV2`, `PremiumV3`, `Isolated`)

## Pricing Tiers
The ==pricing tier== of a plan determines what features are available and how much it costs.
There are a few categories of pricing tiers:
- `Shared compute`
	- Both `Free` and `Shared` share resource pools with apps of other customers
	- Allocate CPU quotas to each app that runs on shared resources
	- These resources *cannot* scale out
- `Dedicated compute`
	- The `Basic`, `Standard`, `Premium`, `PremiumV2`, and `PremiumV3` tiers run on ==dedicated== VMs
	- Only apps within same plan share the same compute resources
	- The higher the tier, the more VM instances available for scale-out
- `Isolated`
	- Runs on dedicated Azure VMs on dedicated Azure Virtual Networks
	- Provides network isolation on top of compute isolation
	- Provides maximum scale-out capabilities
- `Consumption`
	- Only available to [[Azure Functions|function apps]]
	- Scales functions dynamically depending on workload

## How Does the App Run and Scale?
App receives ==CPU minutes== on a ==shared VM instance== and ==cannot scale out== for the `Free` and `Shared` tiers.

In other tiers, app runs and scales as follows:
- App runs on all VM instances configured in plan
- If multiple apps in same plan, they share the same VM instances
- If multiple [[Explore Azure App Service Deployment Slots|deployment slots]] for app, all deployment slots run on same VM instances
- If enabled diagnostic logs, perform backups, or run WebJobs, they also use CPU cycles and memory on same instances

*App Service plan* is the ==scale unit== of the *App Service* apps.
If plan configured to run 5 VM instances, then all apps in plan run on all 5 instances.
If plan configured for auto-scaling, then all apps scaled out together based on auto-scale settings.

## What if App Needs More Capabilities or Features?
The plan can be increased or decreased at any time.
Simply change the [[#Pricing Tiers|pricing tier]] of the plan.
You can move an app into a separate *App Service plan* if desired.

Multiple apps on one plan can save money, but they share resources so the capacity of all the apps needs to be understood and plan configured for the expected load.

You should isolate an app on its own plan when:
- App is resource-intensive
- Want to scale an app independently of other apps
- App needs resources in a different geographical region