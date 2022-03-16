#azure #azure-wda 

# Explore Staging Environments
Can use a different deployment slot instead of default *production*.
This is available for `Standard`, `Premium`, and `Isolated` [[Examine Azure App Service Plans#Pricing Tiers|pricing tiers]].
Deployment slots are *live* apps with their *own host names*.
App content and config can be **swapped** between the slots.

Deploying to a non-production slot has the following *benefits*:
- Validate app changes in staging before swapping to production
- All instances are warmed up on staging before being swapped to production
	- Reduces down time to practically zero when deploying the app
	- ==Traffic redirection== is seamless
	- No requests will be dropped because of swap operations
	- Can automate this workflow by configuring ==auto swap==  when pre-swap validation isn't needed
- After a swap involving production, the "old" production version continues to exist on staging
	- Can re-swap if an issue occurs on "new" production, setting app back to what it was pre-update

Each *App Service plan* supports a different number of slots.
No additional charge for using these slots.

When changing tiers, ensure the target tier supports the number of slots you need (or already use!).

When creating a new slot, it will have no content.
This is the case even if you import settings from a different slot.
You can deploy to the slot from a repo branch.