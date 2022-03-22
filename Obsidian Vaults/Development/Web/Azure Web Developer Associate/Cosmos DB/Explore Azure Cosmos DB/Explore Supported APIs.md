#azure #azure-wda 

# Explore Supported APIs
## Core(SQL) API
Stores data in a document format.
Offers best end-to-end experience as full control over interface, service, and SDK client libraries.
New features rolled out to *Azure Cosmos DB* is first available on SQL API accounts.
Support for querying json items using [[SQL]].

If migrating from other database such as *Oracle*, *DynamoDB*, *HBase* etc. SQL API is recommended option.
Supports analytics and offers performance isolation between operational and analytical workloads.

## API for MongoDB
Stores data in a document structure, via *BSON* format.
Compatible with *MongoDB* wire protocol; but does not use native *MongoDB* related code.
API is great choice if you want to use broader *MongoDB* ecosystem and skills.
Does not compromise on *Azure Cosmos DB* features such as:
- Scaling
- High availability
- Geo-replication
- Multiple wire locations
- Automatic and transparent shard management
- Transparent replication between operational and analytical stores
- Etc.

Can use existing *MongoDB* apps by just changing app's connection string.

## Cassandra API
Stores data in column-oriented schema.
Is wire protocol compatible with *Apache Cassandra*.
Recommended if you want benefit of elasticity and fully managed nature of *Cosmos DB*.
Still use most of native *Apache Cassandra* features, tools, and ecosystems.

Can use *Apache Cassandra* client drivers to connect to *Cassandra API*.
Enables you to interact with data using *Cassandra Query Language* (CQL).
Currently only supports *OLTP* scenarios.
Using *Cassandra*, you can also use unique features of *Cosmos DB* such as change feed.

## Table API
Stores data in a key-value format.
If using *Azure Table* storage, you may see some limitations in:
- Latency
- Scaling
- Throughput
- Global distribution
- Index management
- Low query performance

*Table API* overcomes these limitations and recommended to migrate app if you want to use the benefits of *Azure Cosmos DB*.
*Table API* only supports OLTP scenarios.

Apps written for *Azure Table* can migrate to *Table API* with little code changes and take advantage of premium capabilities.

## Gremlin API
Allows users to make graph queries.
Stores data as edges and vertices.
used for scenarios involving dynamic data, data with complex relations, data that is too complex to be modelled with relational databases, and if you want to use the existing *Gremlin* ecosystem and skills.
Only supports OLTP scenarios.