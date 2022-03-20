#azure #azure-wda #topic 

# Azure Storage Redundancy Options
Multiple copies of data is always stored.
This is in case of planned or unplanned events, such as:
- Hardware failure
- Network outage
- Power outage
- Natural disasters

This redundancy ensures storage account meets availability and durability targets.
Consider trade-offs when choosing best ==redundancy option==. 
Factors that help determine which option include:
- How data is replicated in the primary region
- Whether data replicated to a secondary region geographically distant to primary
- Whether app requires read access to replicated data in secondary region if primary becomes unavailable

## Redundancy in the Primary Region
Data in *Azure Storage* is always replicated three times in primary region.
There are two options on offer for how data is replicated here:
1. `Locally Redundant Storage` (LRS)
	- Copies data synchronously three times
	- Done within a physical location in the primary region
	- Least expensive option
	- Not recommended for applications requiring high availability or durability
2. `Zone Redundant Storage` (ZRS)
	- Copies data synchronously across availability zones
	- Done within primary region
	- For apps requiring high availability
	- Should do this in conjunction with secondary region replication

## Redundancy in a Secondary Region
For apps requiring high durability and availability.
Copies data to a secondary region many miles from the primary region.
Ensures data is durable through regional disasters or outages.

The paired secondary region is based on the primary region and cannot be changed.

There are two options for copying data to a secondary region:
1. `Geo-Redundant Storage` (GRS)
	- Copies data synchronously three times within a single physical location in primary region using LRS
	- Then copies data asynchronously to a single physical location in secondary region
	- Data is then copied within single physical location in secondary region three times
2. `Geo-Zone Redundant Storage` (GZRS)
	- Copies data synchronously across availability zones in primary region using ZRS
	- Then copies data asynchronously to a single physical location in secondary region
	- Data is further copied synchronously three times using LRS