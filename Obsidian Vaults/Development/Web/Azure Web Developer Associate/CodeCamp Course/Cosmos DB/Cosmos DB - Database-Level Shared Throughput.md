#azure #az-204 

When creating a database and a container, you can configure throughput strategy.
There are two strategy options:
- **Dedicated Mode**
	- Throughput is exclusive to this container
	- Backed by SLAs
- **Shared Mode**
	- Throughput shared across all containers

You cannot change throughput strategies after creation.
- If you really need to, you need to create a new container and migrate the data over
Enable *Shared Mode* by ticking the `Share throughput across containers` checkbox.
Shared throughput is *not* available for [[Cosmos DB - Container Capacity|Serverless Capacity Mode]].

Sharing the database-level provisioned throughput is analogous to hosting a database on a cluster of machines.
All containers within a database share the resources available on a machine.
Naturally you do not get predictable performance on any specific container, but you do maximise the use of the resources.