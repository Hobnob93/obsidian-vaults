#azure #az-204 

# Choose The Right Consistency Level
Cosmos DB allows devs to choose from the 5 [[Explore Consistency Levels|consistency levels]].
Each provides precise availability and performance tradeoffs.
Each backed by comprehensive SLAs.

## SQL API & Table API
Consider following points if your app is built using SQL or Table API:
- For many scenarios, session consistency is optimal and ==recommended== option
- If app requires strong consistency, recommended you use `bounded staleness`
- If app requires stricter consistency guarantees, recommended you use `bounded staleness`
- If app requires eventual consistency, recommended you use `prefix` consistency
- If app needs less strict guarantees, recommended you use `prefix` consistency
- If you need highest availability and lowest latency, use `eventual` consistency
- If you need much higher durability without sacrificing performance, can create custom consistency level at application layer

## Cassandra, MongoDB, & Gremlin APIs
Cosmos DB provides native support for wire protocol-compatible APIs.
When using *Gremlin*, default consistency level configured on Cosmos account is used.

## Consistency Guarantees in Practice
May often get strong consistency guarantees.
Guarantees for a read operation correspond to freshness and ordering of database state requested.
Read-consistency is tired to ordering and propagation of write/update operations
- When `bounded staleness`, clients always read the value of previous write, with lag bounded by the staleness window
- When `strong`, staleness window is equivalent to zero, clients are guaranteed to read latest committed value of write operation
- For remaining consistency levels, staleness window largely dependent upon workload

If *Azure Cosmos* account configured with consistency level other than `strong`, you can find probability that clients get strong and consistent reads for workload by looking at `Probabilistically Bounded Staleness` (PBS) metric.

Probabilistic bounded staleness shows how eventual the eventual consistency is.
Metric provides insight into how often you get stronger consistency than level you have configured.