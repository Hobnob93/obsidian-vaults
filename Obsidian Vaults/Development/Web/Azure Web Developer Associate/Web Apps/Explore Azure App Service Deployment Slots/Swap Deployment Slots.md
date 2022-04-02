#azure #az-204

# Swap Deployment Slots
Can swap slots on app's ==Deployment Slots== page or ==Overview Page==.
Ensure production is ***target*** slot if swapping stage to prod.
Ensure staging slot configured exactly how you want it to be on prod.

## Manually Swapping Deployment Slots
1. Go to app's ==Deployment Slots== page and choose `Swap`.
	- A dialog box shows settings that will be changed for ***source*** and ***target*** slots
2. Select desired ***source*** and ***target*** slots.
	- Select the `Source Changes` and/or `Target Changes` tabs to verify config changes are as expected
	- Swap slots immediately by pressing `Swap`.
	- Optionally can also [[#Swap with Preview Multiphase Swap|swap with preview]]
3. When finished click `Close`.

## Swap with Preview (Multiphase Swap)
This allows you to validate the app runs with the swapped settings.
Also allows ***source*** slot to be warmed up before swap completion - desirable for mission-critical applications.

If you cancel the swap, *App Service* reapplies config elements to ***source*** slot.

To swap with preview:
1. Follow manual steps [[#Manually Swapping Deployment Slots|above]], but choose `Perform swap with preview` at step 2.
2. Select `Start Swap` when ready to start the swap.
	- When phase 1 finishes, you're notified in the dialog box
	- Preview the ***source*** slot by going to `https://<appname>-<slotname>.azurewebsites.net`
3. When ready to complete the pending swap, choose `Complete Swap` in ==Swap action==.
	- Click `Cancel` if you wish to cancel instead
4. When done, click `Close`.

## Configure Auto-swap
Auto-swap streamlines scenarios for CI.
Ensures zero cold starts and downtime for customers.
Will automatically swap each time app changes are deployed.

To configure auto-swap:
1. Go to app's ==Resource== page and select slot you want to configure auto-swap
	- The setting is in the ==General Settings== page
2. Set `Auto swap enabled` to `On`.
3. Select desired target slot and click `Save`.
4. Execute a code push to the source slot, and it will kick off after a short time.

## Specify Custom Warm-Up
Some apps might require a custom warm-up before the swap.
The `applicationInitialization` in `web.config` lets you specify these custom actions.
Swap operation waits for these custom warm-up to complete before swapping.

Here's a `web.config` fragment:
```xml
<system.webServer>
	<applicationInitialization>
		<add initializationPage="/" hostName="[app hostname]" />
		<add initializationPage="/Home/About" hostName="[app hostname]" />
	</applicationInitialization>
</system.webServer>
```

You can get more info on this [here](https://ruslany.net/2017/11/most-common-deployment-slot-swap-failures-and-how-to-fix-them/).

You can customise the behaviour with one or both of the following app settings:
- `WEBSITE_SWAP_WARMUP_PING_PATH`
	- The path to ping to warm up the site
	- E.g. `/statuscheck`
	- Default value is app root (`/`)
- `WEBSITE_SWAP_WARMUP_PING_STATUSES`
	- Valid HTTP response codes for warm-up operation
	- Comme-separated list of HTTP response codes
	- If returned status not in list, warm-up and swap operations stopped
	- By default, *any* response code is valid

## Roll Back and Monitor a Swap
If any errors occur in ***target*** slot after a slot swap, you can restore slots to their pre-swap states.

If the swap operation takes a long time, you can get information in the *Activity Log*.
Swap operations appear in log query as `Swap Web App Slots`.