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
How Cosmos database is mapped to various API-specific entities:
- **Azure Cosmos entity** => Azure Cosmos database
- **SQL API** => Database
- **Cassandra API** => Keyspace
- **Cosmos DB API for MongoDB** => Database
- **Gremlin API** => Database
- **Table API** => N/A

## Azure Cosmos Containers
