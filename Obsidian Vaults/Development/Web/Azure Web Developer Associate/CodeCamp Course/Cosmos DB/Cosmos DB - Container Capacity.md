#azure #az-204 

Capacity defines the amount of underlying resources available.
Resources include compute as well as storage.

Cosmos DB has two capacity modes:
1. Provisioned throughput
	- For each container, you provision some amount of throughput
	- Expressed in Request Units (RU) per second
	- For workloads where traffic is reliably predictable
	- More flexible options
1. Serverless
	- You run your database operations against your containers without having to provision any capacity
	- For low (small) workloads
	- For unpredictable spike and traffics
	- Easy to configure, with limitations
	- Can be more cost-effective, but that depends on what your consumption models look like

| Area                          | Provisioned Throughput                                                                 | Serverless                                                            |
| ----------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **Geo-distribution**          | Can run in multiple regions                                                            | Can only run in a single region                                       |
| **Max storage per container** | Unlimited                                                                              | 50 GB                                                                 |
| **Performance**               | <10ms latency for point-reads and writes covered by SLA                                | <10ms latency for point-reads & <30ms for writes covered by SLO       |
| **Billing Model**             | On a per-hour basis for the RU/s provisioned, regardless of how many RUs were consumed | On a per-hour basis for amount of RUs consumed by database operations |
