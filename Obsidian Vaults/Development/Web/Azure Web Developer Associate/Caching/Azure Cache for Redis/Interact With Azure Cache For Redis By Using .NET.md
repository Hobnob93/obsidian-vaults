#azure #az-204 #csharp #json 

## Overview
Typically, client app will use a client library to form requests and execute commands on a Redis cache.
Can get a list of client libraries directly from Redis clients page.

A popular high-performance Redis client for .NET language is [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis).
Package is available through NuGet.
Below are examples of how to use the client.

## Connecting To Redis Cache With `StackeExchange.Redis`
Azure offers a connection string for some Redis clients, which bundles all data required to connect into a single string.
It will look something like this:
```
[cache-name].redis.cache.windows.net:6380,password=[pw]mssl=True,abortConnectt=False
```
Can pass this string to `StackExchange.Redis` to create connection to server.

There are two additional parameters at the end:
- `ssl`
	- Ensures communication is encrypted
- `abortConnect`
	- Allows connection to be created even if server is unavailable at that moment
There are other optional parameters as well.

## Creating A Connection
Main connection class is `StackExchange.Redis.ConnectionMultiplexer`.
It abstracts the process of connecting to a server.
It's optimised to manage connections efficiently and intended to be kept around while you need to access the cache.

Can create an instance the static `ConnectionMultiplexer.Connect` or `ConnectionMultiplexer.ConnectAsync` methods,
Can pass a connection string or a `ConfigurationOptions` object.
```csharp
using StackExchange.Redis;
...
var connectionString = "[from config]";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
```

Once you have a connection, there are 3 primary things you might want to do:
1. Access a Redis database
2. make use of publisher/subscriber features of Redis
3. Access individual server for maintenance or monitoring purposes

## Accessing A Redis Database
Redis database represented by the `IDatabase` interface.
Retrieved using the `GetDatabase()` method.
The `IDatabase` instance is lightweight and does not need to be stored; only the `ConnectionMultiplexer` instance should be stored.
```csharp
IDatabase db = redisConnection.GetDatabase();
```

With the database object you can execute methods to interact with the cache.
All methods have sync and async versions.
Example of storing a key/value pair in cache:
```csharp
bool wasSet = db.StringSet("favourite:flavour", "mint");
```
It returns a `bool` indicating whether value was successfully set.
Can then retrieve the value with `StringGet`:
```csharp
string val = db.StringGet("favourite:flavour");
	ConsoleWriteLine(val); // outputs 'mint'
```

## Getting & Setting Binary Values
Redis keys and values are binary-safe.
Can be used to store binary data.
Implicit conversion operators to work with `byte[]` types so you can work with the data naturally.
```csharp
byte[] key = ...;
byte[] val = ...;

db.StringSet(key, val);

...

byte[] key = ...;
byte[] val = db.StringGet(key);
```

`StringExchange.Redis` represents using the `RedisKey` type.
The type has implicit conversions to and from both `string` and `byte[]`.
Allows both text and binary keys to be used without any complication.
Values are represented by the `RedisValue` type, and has the same implicit conversions.

## Other Common Operations
The `IDatabase` interface includes other methods, allow you to work with hashes, lists, sets, and ordered sets.
Some common methods that work with single keys:
- `CreateBatch`
	- Creates group of operations to be sent to the server as a single unit, but not necessarily processed as a unit
- `CreateTransaction`
	- Creates a group of operations to be sent to the server as a single unit, and processed as such
- `KeyDelete`
	- Delete the key/value pair
- `KeyExists`
	- Returns whether a given key exists
- `KeyExpire`
	- Sets a time to live (TTL) expiration on a key
- `KeyRename`
	- Renames a key
- `KeyTimeToLive`
	- Returns the TTL for a key
- `KeyType`
	- Returns the string representation of the type of value stored at the key
	- Different types returned could be `string`, `list`, `set`, `zset`, and `hash`

## Executing Other Commands
The `IDatabase` object has `execute` and `ExecuteAsync` methods for passing textual commands to the server. Example:
```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString());  // displays 'PONG'
```

The `Execute` methods return a `RedisResult` object which is a data holder containing two properties:
- `Type`
	- A `string` indicating type of result ("STRING", "INTEGER", etc)
- `IsNull`
	- A boolean of the null status of the value
Can then call `ToString()` to get the actual value.
Can use `Execute` for any supported textual commands.

## Storing More Complex Values
Can cache object graphs by serialising them to textual format - typically XML or JSON.
As an example, statistics from a game:
```csharp
public class GameStat
{
	public string Id { get; set; }
	public string SomeStat { get; set; }
	public DateTimeOffset DatePlayed { get; set; }
	public IReadOnlyList<string> SomeStats { get; set; }

	public GameStat(string someStat, DateTimeOffset datePlayed, string[]
		someStats)
	{
		Id = Guid.NewGuid().ToString();
		SomeStat = someStat;
		DatePlayed = datePlayed;
		SomeStats = someStats.ToList();
	}
}
```

Can use the `Newtonsoft.Json` library to turn instance into JSON:
```csharp
var stat = new GameStat("Foobar", DateTime.Now, new[] { "Val1", "Val2" });
string serializedStat = JsonConvert.SerializeObject(stat);
bool added = db.StringSet("some:stat:2023", serializedStat);
```

Could then retrieve it and turn it back to the original object:
```csharp
var result = db.StringGet("some:stat:2023");
var stat = JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine("stat.SomeStat"); // displays 'Foobar'
```

## Cleaning Up The Connection
Once you're done with Redis connection, you can `Dispose` the `ConnectionMultiplexer`.
It closes all connections and shuts down communication with the server.
```csharp
redisConnection.Dispose();
redisConnection = null;
```