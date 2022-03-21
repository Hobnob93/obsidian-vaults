#azure #azure-wda 

# Explore The Resource Hierarchy
The *Azure Cosmos* account is fundamental unit of distribution and high availability.
Account contains unique DNS name and can manage account using *Azure Portal*, or *Azure CLI*, or language SDKs.

## Elements in an Azure Cosmos Account
A container is the fundamental unit of scalability.
Can virtually have an unlimited provisioned throughput **(RU/s)** and storage on a container.
Cosmos DB transparently partitions container using logical partition key you specify to elastically scale provisioned throughput and storage.

Can create a maximum of 50 Cosmos accounts under a subscription.
Can manage data in account by creating databases, containers, and items.

The following image shows the hierarchy of different entities in Cosmos DB account:
![[Cosmos DB Entity Hierarchy.png]]

## Azure Cosmos Databases
Can create one more multiple databases in your account.
It is analogous to a namespace.
It is a unit of management for a set of containers.
How Cosmos database is mapped from various API-specific entities:
- **Azure Cosmos entity** => Azure Cosmos database
- **SQL API** => Database
- **Cassandra API** => Keyspace
- **Cosmos DB API for MongoDB** => Database
- **Gremlin API** => Database
- **Table API** => N/A

## Azure Cosmos Containers
The unit of scalability for both provisioned throughput and storage.
It is horizontally partitioned and then replicated across multiple regions.
Items added to container are automatically grouped into logical partitions.
These are distributed across physical partitions based on partition key.
Throughput of container is evenly distributed across physical partitions.

Can configure throughput in the following modes when creating a container:
- **Dedicated provisioned throughput mode**
	- Exclusively reserved for that container and is backed by SLAs
- **Shared provisioned throughput mode**
	- Containers share provisioned throughput with other containers in same database

Container is a schema-agnostic container of items.
Items in container can have arbitrary schemas e.g. a person or a car can be stored in same container.
Items added to container are automatically indexed when added.
They do not require explicit indexing or schema management.

## Azure Cosmos Items
Depending on which API is used, items can represent either a document or a collection; a row in a table; a node or edge in a graph.
How Cosmos items mapped from various API-specific items:
- **Cosmos Entity** => Azure Cosmos Item
- **SQL API** => Item
- **Cassandra API** => Row
- **Cosmos DB API For Mongo DB** => Document
- **Gremlin API** => Node or edge
- **Table API** => Item