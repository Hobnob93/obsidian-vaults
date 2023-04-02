#azure #az-204 #exercise #cli #csharp 

## Prerequisites
An Azure account with active subscription

## Start Cloud Shell
1. Log in to Azure Portal and open the Cloud Shell
2. After shell opens, select __Bash__ environment

## Create Azure Resources
1. Create resource group for the resources
```shell
az group create --name az204-redis-rg --location <region>
```
2. Create an Azure Cache for Redis instance using `redis create` command
```shell
redisName=az204redis$RANDOM

az redis create --location <region> --resource-group az204-redis-rg \
	--name $redisName --sku Basic --vm-size c0
```
3. In portal, navigate to the Redis Cache you just created
4. Select `Access Keys` in the `Settings` section
5. Copy `Primary connection string (StackExchange.Redis)` value for use later

## Create The Console Application
1. Create an empty console application with any preferred method
2. Add the `StackExchange.Redis` NuGet package
3. In the `Program.cs` file add the following usings:
```csharp
using StackExchange.Redis;
using System.Threading.Tasks;
```
4. Add the connection string variable:
```csharp
static string connectionString = "<paste conn string>";
```
5. Create the following `Main` method:
```csharp
using var cache = await ConnectionMultiplexer.ConnectAsync(connectionString);

IDatabase db = cache.GetDatabase();

var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

bool setValue = await db.StringSetAsync("test:key", "100");
Console.WriteLine($"SET: {setValue}");

string getValue = await db.StringGetAsync("test:key");
Console.WriteLine($"GET: {getValue}");
```
6. Run the code and see the output result in the terminal prompt
7. Return to portal and select `Activity log` in the `Azure Cache for Redis` blade
8. You can see the operations in the log

## Clean Up Resources
When you no longer need these resources, use the following command to delete the resource group and related resources.
```shell
az group delete --name az204-redis-rg --no-wait
```