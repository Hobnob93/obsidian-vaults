#azure #azure-wda 

# Examine Slot Swapping
*App Service* does the following upon swapping slots to ensure *target* slot doesn't experience downtime:
1. Apply settings from ***target*** slot (e.g. production) to all instances of ***source*** slot (e.g. staging).
	- Settings include (if any applicable/enabled):
		- Slot-specific app settings and connection strings
		- Continuous deployment settings
		- App Service auth settings
	- All instances in ***source*** are restarted
	- If `swap with preview`, this is end of first phase - you can validate staging from here before continuing
2. Wait for every instance in ***source*** to complete restart.
	- If any instance fails to restart, swap operation reverts all changes to ***source*** & operation is stopped
3. If `local cache` enabled, initialise local cache through HTTP request to app root (`/`) on each instance on ***source*** slot.
	- Wait for each instance to return *any* HTTP response
	- Causes another restarted on each instance
4. If `auto swap` enabled with `custom warm-up`, trigger app initiation through HTTP request to app root (`/`) on each instance of ***source*** slot.
	- If `applicationInitialization` isn't specified, trigger HTTP request to app root of ***source*** slot on each instance
	- If *any* instance returns *any* response, warm up considered done
5. If all instances warmed up successfully, swap slots by switching routing values for the two slots.
	- The ***target*** slot now has app that's previously been warmed up in the ***source*** slot
6. ***Source*** slot now has the older app previously in ***target*** slot
	- Perform same operation by applying all settings and restarting instances

At any point, all work happens on the ***source*** slot.
***Target*** slot remains online during process, regardless of success or failure.
Ensure prod is ***target*** slot when swapping stage to prod to avoid downtime.

When config is cloned from another slot, the cloned config is editable.
Some config elements follow content across a swap (not slot-specific).
Some config elements stay in the same slot after a swap (slot specific).
Consult table below for which settings go where during a swap:

| Settings that are swapped         | Settings that aren't swapped         |
| --------------------------------- | ------------------------------------ |
| General settings i.e. framework   | Publishing endpoints                 |
| App settings (can be fixed)       | Custom domain names                  |
| Connection strings (can be fixed) | Non-public certificates              |
| Handler mappings                  | TLS/SSL settings                     |
| Public certifications             | Scale settings                       |
| WebJobs content                   | WebJobs schedulers                   |
| Hybrid connections *              | IP Restrictions                      |
| Virtual network integration *     | Always On                            |
| Service Endpoints *               | Diagnostic log settings              |
| Azure Content Delivery Network *  | Cross-origin resource sharing (CORS) |
*Marked items: planned to be unswapped*

To configure app setting or connection string to stick to specific slot, go to ==Configuration== page for that slot.
Add or edit the `Deployment slot setting`.