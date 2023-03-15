#azure #az-204 

The data among partitions in Azure Cosmos DB indexes are grouped by the partition keys in order to improve performance.

**Partition Keys** are the keys used to group items.
- Works like primary keys in a relational database
A **logical partition** is a group of items that all have the same partition key value.
**Physical partitions** consist of a set of logical partitions.
- Cosmos DB manages logical partitions
- Can have a one-to-many relationship
**Replica-sets** are made up of a group of physical partitions that are materialised as a self-managed, dynamically load-balanced group of replicas that span across multiple **fault domains**.

![[Cosmos DB - Partitioning Schemes Diagram.png]]