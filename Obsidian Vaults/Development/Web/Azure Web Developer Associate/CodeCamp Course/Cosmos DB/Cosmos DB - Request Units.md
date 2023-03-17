#azure #az-204 

The cost of all database operations is normalised by Azure Cosmos DB.
It is expressed as Request Units (RU).
RUs abstract away memory, CPU, and IOPS (I/O per second) with a single value based on data processed.
There is a [Capacity Calculator](https://cosmos.azure.com/capacitycalculator) to help work out costs.

Database operations include:
- **Read**
	- Size of item retrieved e.g. 1KB = 1RU
- **Insert**
	- Inserting a 1KB item without indexing costs ~5.5RUs
- **Upsert**
	- Replacing an item costs two times the charge required to insert the same item
- **Delete**
	- No associated RUs
- **Query**
	- The size of the items retrieved