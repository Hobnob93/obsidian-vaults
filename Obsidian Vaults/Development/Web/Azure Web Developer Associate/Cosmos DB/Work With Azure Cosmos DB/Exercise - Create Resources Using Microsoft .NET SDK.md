#azure #az-204 #exercise #shell #csharp 

# Exercise - Create Resources Using Microsoft .NET SDK
## Prerequisites
- An *Azure* account with an active subscription
- An IDE
- Azure CLI
- .NET 3.1 or .NET 5.0 SDK

## Setting Up
### Connecting To Azure
1. Start the IDE and open the terminal window
2. Use the command below to log in to *Azure*
```shell
az login
```

### Create Resources in Azure
1. Create a resource group
```shell
az group create --location <my-loc> --name <resource-group>
```
2. Create the *Azure Cosmos DB* account with a *unique* name
```shell
az cosmosdb create --name <cosmos-db-acct> --resource-group <resource-group>
```
3. Make note of the `documentEndpoint` shown in JSON response
4. Retrieve primary key for account
```shell
az cosmosdb keys list --name <cosmos-db-acct> --resource-group <resource-group>
```
5. Make note of the `primaryMasterKey` from the command result

### Set Up the Console Application
Create folder and project, and open in VS Code (if that's your IDE)
```shell
md <project-name>
cd <project-name>

dotnet new console

code . -r
```

## Build The Console Application
### Add Packages And Using Statements
1. Run the command in the terminal to install Cosmos package
```shell
dotnet add package Microsoft.Azure.Cosmos
```
2. Add using statements to include the Cosmos package and async operations
```cs
using System.Threading.Tasks;
using Microsoft.Azure.Cosmos;
```

## Connect To An Azure Cosmos DB Account
Implement the `Program` class below.
Replace **`documentEndpoint`** with the `documentEndpoint` value retrieved earlier.
Replace **`your primary key`** with the `primaryMasterKey` value retrieved earlier.
```cs
public class Program
{
	private static readonly string EndpointUri = "documentEndpoint";
	private static readonly string PrimaryKey = "your primary key";
	private static readonly string DatabaseId = "db-id-123";
	private static readonly string ContainerId = "cont-id-123";

	private CosmosClient cosmosClient;
	private Database database;
	private Container container;

	public static async Task Main(string[] args)
	{
		try
		{
			Console.WriteLine("Beginning operations...\n");
			
			var p = new Program();
			await p.CosmosAsync();

			// Create the database call
			// Create the container call
		}
		catch (CosmosException ex)
		{
			var baseException = ex.GetBaseException();
			Console.WriteLine("{0} error occurred: {1}", ex.StatusCode, ex);
		}
		catch (Exception ex)
		{
			Console.WriteLine("Error: {0}", ex);
		}
		finally
		{
			Console.WriteLine("End of program, press any key to exit.")
			Console.ReadKey();
		}
	}

	public async Task CosmosAsync()
	{
		this.cosmosClient = new CosmosClient(EndpointUri, PrimaryKey);
	}
}
```

### Create A Database
Add the following method to the `Program` class:
```cs
private async Task CreateDatabaseASync()
{
	this.database = await this.cosmosClient.CreateDatabaseIfNotExistsAsync(
		DatabaseId);
	Console.WriteLine("Created Database: {0}\n", this.database.Id);
}
```
Then replace the Create database call comment with:
```cs
await this.CreateDatabaseAsync();
```

### Create A Container
Add the following method to the `Program` class:
```cs
private async Task CreateContainerAsync()
{
	this.container = await this.database.CreateContainerIfNotExistsAsync(
		ContainerId, "/LastName");
	Console.WriteLine("Created Container: {0}\n", this.container.Id);
}
```
Then replace the Create container call comment with:
```cs
await this.CreateContainerAsync();
```

### Run The Application
You'll see the connection take place, as well as the creation of the database and the container.
You can navigate to *Portal* and use ==Data Explorer== to view database and container.

## Clean Up Azure Resources
Run the following command to remove all resources created:
```shell
az group delete --name <resource-group> --no-wait
```