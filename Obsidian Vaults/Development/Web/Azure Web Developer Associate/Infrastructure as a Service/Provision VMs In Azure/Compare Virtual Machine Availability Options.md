#azure #az-204 

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
A logical group of shared underlying hardware.
Hardware shared include:
- Power source
- Network switch
As VMs created within availability set, *Azure* platform automatically distributes VMs across different fault domains.
This approach limits impact of potential physical hardware failures, network outages, or power interruptions.

![[Fault Domain Diagram.png]]

### Update Domains
A logical group of underlying hardware that can undergo maintenance or be rebooted at the same time.
*Azure* platform automatically distributes VMs across different update domains.
This ensures at least one instance always remains running as periodic maintenance takes place.
Order of update domains being rebooted may not proceed sequentially planned maintenance.
Only one update domain is rebooted at a time.

![[Update Domain Diagram.png]]

## Virtual Machine Scale Sets
Lets you create and manage group of load balanced VMs.
Number of VM instances can automatically increase or decrease in response to demand or defined schedule.

### Load Balancer
Combine load balancer with availability zone or availability set to get most resiliency.
*Azure* load balancer is a Layer-4 (TCP, UDP) load balancer providing high availability.
It distributes traffic among healthy VMs.
A health probe monitors a given port on each VM and only distributes traffic to operational VM.

You define front-end IP config containing one or more public IP addresses.
This config allows your load balancer and apps to be accessible over the Internet.

VMs connect to a load balancer using their virtual network interface card (NIC).
To distribute traffic to VMs, back-end address pool contains IP addresses of the virtual NICs connected to load balancer.

To control traffic flow, you define load balancer rules for specific ports and protocols that map to your VMs.