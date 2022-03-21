#azure #azure-wda 

# Explore Consistency Levels
Cosmos DB approaches data consistency as a spectrum of choices instead of two extremes.
Strong consistency on one end; eventual consistency at the other.
There are many consistency choices along the spectrum.
Devs can use these options to make precise choices at granular trade-offs.
This is done with respect to high availability and performance.

There are 5 well-defined consistency models on the spectrum, from strongest to more relaxed:
1. `strong`
2. `bounded staleness`
3. `session`
4. `consistent prefix`
5. `eventual`

Each level provides availability and performance trade-offs.
Image below shows different consistency levels as a spectrum:
![[Cosmos Consistency Levels Spectrum.png]]

Consistency levels are region-agnostic.
Guaranteed for all operations regardless of region.

Read consistency applies to a single read operation scoped with partition-key range or a logical partition.
Read operation can be issued by a remote client or stored procedure.