#azure #az-204 #cli

## Create And Configure an Azure Cache for Redis Instance
Several parameters needed to configure the cache properly for your purposes:
- __Name__
	- Globally unique
	- Used to generate public-facing URL to connect and communicate with the service
	- Must be between 1 and 63 characters
	- Composed of numbers, letters, and '-' character
	- Can't start with the '-' character
	- Consecutive '-' characters aren't valid
- __Location__
	- Which Azure region in which Redis is physically located
	- Always place cache instance and app in same region
	- A cache in a different region can increase latency and reduce reliability
	- If connecting to cache from outside Azure, select location close to where app consuming the data is running
- __Pricing Tier__
	- Can control amount of cache memory available on each tier
		- Choose a cache level from C0 to C6 for basic/standard
		- Or P0 to P4 for Premium
	- Premium tier allows you to persist data in two ways to provide disaster recover:
		- RDB persistence
			- Takes periodic snapshots
			- Rebuild cache using a snapshot in case of failure
		- AOF persistence
			- Saves every write operation to a log
			- Log saved at least once per second
			- Creates bigger files but has less data loss
- __Virtual Network Support__
	- If using Premium tier, can deploy to a virtual network in the cloud
	- Cache will be available to only other virtual machines and apps in the same virtual network
	- Provides higher level of security when service and cache are both hosted in Azure, or are connected through an Azure virtual network VPN
- __Clustering Support__
	- With premium tier, can implement clustering
	- Automatically splits dataset among multiple nodes
	- To implement, specify number of shards to a maximum of 10
	- Cost incurred is cost of original node, multiplied by number of shards

## Accessing the Redis Instance
Redis has a command line tool for interacting with an Azure Cache for Redis as a client.
Tool available for Windows platforms.
Redis supports a set of known commands.
Command typically issued as `COMMAND param1 param2 param3`.

Some commands you can use:
- `ping`
	- Ping the server
	- Returns "PONG"
- `set [key] [value]`
	- Sets key/value in the cache
	- Returns "OK" on success
- `get [key]`
	- Gets value from cache
- `exists [key]`
	- Returns "1" if key exists, otherwise "0"
- `type [key]`
	- Returns type associated to the value for a given key
- `incr [key]`
	- Increment value associated by the key by `1`
	- Value must be integer or double type
	- Returns new value
- `incrby [key] [amount]`
	- Increment value associated by the key by `amount`
	- Value must be integer or double type
	- Returns new value
- `del [key]`
	- Deletes value associated with key
- `flushdb`
	- Deles ALL keys and values in database

## Adding An Expiration Time To Values
Need a way to expire values when they are stale.
Done by providing a time to live (TTL) to a key.
When TTL elapses, key is automatically deleted.
- Expirations can be set using seconds or milliseconds
- Expire time resolution is always 1 millisecond
- Information about expires are replicated and persisted on disk

Command: `expire [key] [time]`

## Accessing a Redis Cache From a Client
To connect to an Azure Cache for Redis instance, several pieces of information is needed.
Clients need host name, port, and an access key.
Can retrieve this information from portal though `Settings` > `Access Keys` page.
Host name is the public address of cache.
- Created using the name of the cache
- E.g. `sportsresults.redis.cache.windows.net`
Access key acts as a password.
- Two keys created: primary and secondary
- Can use either key
- Two provided in case of primary key change
- Can switch all clients to secondary key and regen primary key
	- This would block apps using original primary key
- MS recommends periodically regenerating keys
