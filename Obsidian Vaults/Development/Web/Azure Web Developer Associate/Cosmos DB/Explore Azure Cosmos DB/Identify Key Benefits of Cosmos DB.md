#azure #az-204

# Identify Key Benefits of Cosmos DB
Designed for these main benefits:
- Low latency
- Elastic scalability of throughput
- Well-defined semantics for data consistency
- High availability

Can configure database to be globally distributed and available in any region.
Choosing regions depends on the global reach of your application and where users are located.

Can add or remove the regions associated with account at any time.
App doesn't need to be paused or deployed to add or remove a region.

## Key Benefits of Global Distribution
Multi-master replication protocol, meaning every region supports reading and writing.
It also enables:
- Unlimited elastic write and read scalability
- Nearly 100% read and write availability around the world
- Guaranteed reads and writes in less than 10 milliseconds at the 99th percentile

Application can perform near real-time reads and writes.
Internally handles data replication between regions with consistency guarantees.

Running database in multiple regions increases availability of the database.
If one region unavailable, other regions can step in to handle requests.