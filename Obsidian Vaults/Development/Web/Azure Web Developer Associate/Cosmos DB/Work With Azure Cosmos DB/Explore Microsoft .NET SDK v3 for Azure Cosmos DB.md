#azure #az-204 #csharp 

# Explore Microsoft .NET SDK v3 for Azure Cosmos DB
Due to *Azure Cosmos* supports multiple [[Explore Supported APIs|API models]], the .NET SDK uses some generic terms:
- `container`
	- A collection, graph, or table
- `item`
	- A document, edge/vertex, or row
	- Content inside a container

## The `CosmosClient` Class
The class is thread-safe.
Recommended to be a ==singleton== to efficient management and performance.
```cs
var client = new CosmosClient(endpoint, key);
```

## Database Examples
### Create a Database
The `CosmosClient` has method `CreateDatabaseIfNotExistsAsync` to create a database, if the database doesn't already exist.
Use a database `id` to verify if there's an existing database.
```cs
var database = await client.CreateDatabaseIfNotExistsAsync(databaseId, 10000);
```

### Read by Database ID
Reads a database from *Azure Cosmos* as an async operation.
```cs
var readResponse = await database.ReadAsync();
```

### Delete A Database
Delete a database as an async operation.
```cs
await database.DeleteAsync();
```

## Container Examples
### Create A Container
The `Database` has method `CreateContainerIfNotExistsAsync` to create a container, if the container doesn't already exist.
Use a container `id` to verify if there's an existing container.
```cs
var container = await database.CreateContainerIfNotExistsAsync(
	id: containerId,
	partitionKeyPath: partitionKey,
	throughput: 400);
```

### Get A Container by ID
```cs
var container = database.GetContainer(containerId);
var containerProps = await container.ReadContainerAsync();
```

### Delete A Container
```cs
await database.GetContainer(containerId).DeleteContainerAsync();
```

## Item Examples
### Create An Item
The `Container` has method `CreateItemAsync` to create an item.
Method requires a JSON-serialisable object containing an `id`  property, and a `partitionKey`.
```cs
ItemResponse<SalesOrder> response = await container.CreateItemAsync(
	salesOrder,
	new PartitionKey(salesOrder.AccountNumber));
```

### Read An Item
Use method `ReadItemAsync` on the `Container` class to read an item.
```cs
var id = "[id]";
var accountNumber = "[partition-key]";
ItemResponse<SalesOrder> response = await container.ReadItemAsync(
	id,
	new PartitionKey(accountNumber));
```

### Query An Item
Use method `GetItemQueryIterator` on the `Container` class to query items under a container.
Uses an [[SQL]] statement with parameterised values.
Returns a `FeedIterator` instance.
```cs
var query = new QueryDefinition(
	"SELECT * FROM sales WHERE s.AccountNumber = @AccountInput")
	.WithParameter("@AccountInput", "Account1");
	
FeedIterator<SalesOrder> resultSet = container.GetItemQueryIterator<SalesOrder>(
	query,
	requestOptions: new QueryRequestOptions
	{
		PartitionKey = new PartitionKey("Account1"),
		MaxItemCount = 1
	}
)
```

## Additional Resources
The [GitHub Repo](https://github.com/Azure/azure-cosmos-dotnet-v3/tree/master/Microsoft.Azure.Cosmos.Samples/Usage) includes latest .NET sample solutions.