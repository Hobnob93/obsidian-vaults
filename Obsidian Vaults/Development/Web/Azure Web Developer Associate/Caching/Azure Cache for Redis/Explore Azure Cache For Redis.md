#azure #az-204 

## Overview
Azure Cache for Redis provides in-memory data store based on [Redis software](https://redis.io/).
Improves performance and scalability of an app that uses backend data stores heavily.
Able to process large volumes of app requests by keeping frequent data in server memory.
Server memory can be written to/read from quickly.
Provides critical low-latency and high-throughput data storage solutions to modern apps.

Azure Cache for Redis offers Redis open-source (OSS Redis) and commercial product from Redis Labs (Redis Enterprise) as a managed service.
Provides secure and dedicated Redis server instances and full Redis API compatibility.
Service is operated by Microsoft, hosted on Azure, usable by any app within or outside of Azure.

## Key Scenarios
Improves app performance by supporting common app architecture patterns.
Some of the most common include the following patterns:
- __Data cache__
	- Databases often too large to load directly into a cache
	- Common to use cache-side pattern to load data into cache only as needed
	- System can also update the cache when changes are made
	- Updates then distributed to other clients
- __Content cache__
	- Many web pages generated from templates using static content such as headers, footers, banners, etc.
	- These static items shouldn't change often
	- Using in-memory cache provides quick access to static content compared to backend data stores
- __Session store__
	- Commonly used with shopping carts and other user history data
	- A web app may associate with user cookies
	- Storing too much in a cookie can impact performance
		- Cookie is passed and validated with every request
	- Typical solution uses cookie as a key to query data in database
	- Using in-memory cache to associate information with a user is faster than interacting with a database
- __Job and message queueing__
	- Apps often add tasks to a queue when operations associated with request take time to execute
	- Longer running operations queued to be processed in sequence, often by another server
	- This method of deferring work is called task queueing
- __Distributed transactions__
	- Apps sometimes require a series of commands against a backend data-store to execute as a single atomic operation
	- All commands must succeed, or they must all be rolled back to an initial state
	- Azure Cache for Redis supports executing batch of commands as a single transaction

## Service Tiers
Azure Cache for Redis is available in these tiers:
- __Basic__
	- An OSS Redis cache running on a single VM
	- No service-level agreement (SLA)
	- Ideal for development/test and non-critical workloads
- __Standard__
	- OSS Redis cache running on two VMs in a replicated configuration
- __Premium__
	- High performance OSS Redis caches
	- Offers higher throughput
	- Lower latency
	- Better availability
	- Premium caches deployed to more powerful VMs
- __Enterprise__
	- High-performance caches powered by Redis Labs' Enterprise software
	- Supports Redis modules including RediSearch, RedisBloom, and RedisTimeSeries
	- Offers higher availability than all previous tiers
- __Enterprise Flash__
	- Cost-effective large caches powered by Redis Labs' Enterprise software
	- Extends Redis data storage to non-volatile memory
		- Cheaper than DRAM on a VM
		- Reduces overall per-GB memory cost
