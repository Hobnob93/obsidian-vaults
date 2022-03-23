#azure #azure-wda 

# Compare Virtual Machine Availability Options
*Azure* offers several options for ensuring availability of VMs.

## Availability Zones
Expands level of control to maintain availability of apps and data on VMs.
A zone is physically separate, within an *Azure* region.
There are three Availability Zones per *Azure* region.

It is a combination of a fault domain and an update domain.
If you create three or more VMs across three zones in a region, VMs are effectively distributed across three fault domains and three update domains.
*Azure* platform recognises the distribution to make sure VMs in different zones are not scheduled to be updated at the same time.

Build high-availability into your app architecture by co-locating compute, storage, networking, and data resources within a zone and replicating in other zones.
*Azure* services that support Availability Zones fall into two categories:
- **Zonal services**
	- a resource is pinned to specific zone
- **Zone-redundant services**
	- *Azure* platform replicates automatically across zones

## Availability Sets
A logical grouping of VMs allowing *Azure* to understand how app is built to provide redundancy and availability.
A set is composed of two additional groupings that protect against hardware failures and allow updates to safely be applied.

### Fault Domains

### Update Domains
