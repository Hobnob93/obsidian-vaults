#azure #az-204 

Azure Table storage is a NoSQL key/value datastore within Azure Storage Accounts.
Azure Table stores non-relational structured data with a schema-less design.

There are two ways to interact with Azure Tables:
- Azure Table Storage API
- Microsoft Azure Storage Explorer

#### Adding Entries
When you enter data you must provide:
- **Partition Key**
	- Unique identifier for the partition within a given table
- **Row Key**
	- Unique identifier for an entity within a given partition

Azure Table supports the following data types:
- String
- Boolean
- Binary
- DateTime
- Double
- Guid
- Int32
- Int64

#### Querying
You can query data along the partition and row key.
You can also further filter for any other data if you choose to.