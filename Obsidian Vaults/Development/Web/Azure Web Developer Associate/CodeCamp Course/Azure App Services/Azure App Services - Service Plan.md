#azure #az-204 

Azure App Service Plan defines how much you pay and what resources are available to you.
There are 3 pricing tiers for the App Service Plan.

## Shared Tier
There are 2 sub-tiers within the Shared Tier:
- **Free Tier**
	- 1 GB of disk space
	- Up to 10 apps on a single shared instance
	- No SLA for availability
	- Each app has a compute quota for 60 minutes per day
- **Shared Tier**
	- Up to 100 apps on a single shared instance
	- No SLA for availability
	- Each app has a compute quota of 240 minutes per day

Shared Tier *does not* support Linux-based instances.

## Dedicated Tier
There are 5 sub-tiers within the Dedicated Tier:
- **Basic**
	- More disk space
	- Unlimited apps
	- 3 levels within that offer varying amounts of compute power, memory, and disk storage
- **Standard**
	- Scale out to 3 dedicated instances
	- SAL of 99.95% availability
	- 3 levels within that offer varying amounts of compute power, memory, and disk storage
- **Premium**, **PremiumV2**, **PremiumV3**
	- Scale to 10 dedicated instances
	- Availability SLA of 99.95%
	- Multiple levels of hardware

## Isolated Tier
- Only really used for [[Azure App Services - App Service Environment (ASE)|ASEs]]
- Dedicated Azure virtual network
- Scale out to 100 instances
- Availability of 99.95%