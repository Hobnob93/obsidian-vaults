#azure #az-204 

# Discover Request Units
With *Azure Cosmos DB*, you pay for throughput you provision and storage you consume, per hour.
Throughput must be provisioned to ensure sufficient resources available at all times.

Cost of all database operations normalised and expressed as `request units` (RU).
A `request unit` represents system resources such as CPUs, IOPS, and memory required to perform database operations.

Cost to do a point read (fetching a single item by ID and partition key value) for 1KB item is ==1RU==.
All other operations are similarly assigned cost using RUs.
No matter which API is being used, costs are always measured in this way.

![[Request Unit Concept.png]]

The type of *Cosmos* account determines the way consumed RUs get charged.
There are three modes:
- **Provisioned throughput mode**
	- You provision number of RUs for app on a basis in increments of 100 RUs per second
	- You can increase or decrease this number at any time
	- Can make changes programmatically or by using the *Portal*
	- Can provision throughput at container and database granularity level
- **Serverless mode**
	- Don't need to provision any throughput
	- Get billed for amount of request units consumed by database operations at end of billing period
- **Autoscale mode**
	- An automatically scale throughput (RU/s) of database or container
	- Well suited for mission-critical workloads with variable traffic patterns, and require SLAs on high performance and scale