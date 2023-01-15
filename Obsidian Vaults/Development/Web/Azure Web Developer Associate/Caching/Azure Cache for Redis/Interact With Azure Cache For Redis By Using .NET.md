#azure #az-204 #csharp 

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
