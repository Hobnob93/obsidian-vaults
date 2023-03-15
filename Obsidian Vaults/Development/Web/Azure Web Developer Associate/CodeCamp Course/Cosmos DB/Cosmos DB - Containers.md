#azure #az-204 

Azure Cosmos Containers are useful for scalability in Azure Cosmos DB, both in terms of storage and throughput.
They are beneficial when you need a different set of configurations for each of your Azure Cosmos DBs because they allow you to customise each container individually.

Azure Cosmos Container has some container-specific properties.
The properties can be system-generated or user-configurable.
They vary according to the used API.

#### Properties
An Azure Cosmos Container has a set of system-defined properties.
Depending on which API you use, some properties might not be directly exposed.

The following table describes the list of system-defined properties:
| Property | Type              | Purpose                                            | SQL API | Cassandra API | MongoDB API | Gremlin API | Table API |
| -------- | ----------------- | -------------------------------------------------- | ------- | ------------- | ----------- | ----------- | --------- |
| `_rid`   | System-generated  | Unique identifier of container                     | Yes     | No            | No          | No          | No        |
| `_etag`  | System-generated  | Entity tag used for optimistic concurrency control | Yes     | No            | No          | No          | No        |
| `_ts`    | System-generated  | Last updated timestamp of the container            | Yes     | No            | No          | No          | No        |
| `_self`  | System-generated  | Addressable URI of the container                   | Yes     | No            | No          | No          | No        |
| `id`     | User-configurable | User-defined unique name of the container          | Yes     | Yes           | Yes         | Yes         | Yes       |

This is **NOT** a complete list, as there are more... these are just examples.