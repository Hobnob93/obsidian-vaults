#azure #az-204 

Azure Cache for Redis is based on the popular open-source Redis cache.
Gives you access to a secure, dedicated Redis cache that Microsoft manages.
You can access it from any Azure application.

Azure Cache for Redis is suited for high-throughput and low-latency requirements where the same data is often requested.

Azure Cache for Redis is commonly used to:
- Store session data so your web apps are stateless and can take advantage of multiple VMs or containers
- Stores cached HTML or JSON to speed up response times for fetching web pages or API calls
- Used to support a job or message queuing system
- Used in front of a database to reduce read contention on the database, or improve response times for fetching data
	- Azure Cache for Redis could be put in front of database services such as Cosmos DB or Azure SQL
		- The Aside-Cache Pattern is when a Cache Store sits in front of a database

![[Pasted image 20230328202314.png]]