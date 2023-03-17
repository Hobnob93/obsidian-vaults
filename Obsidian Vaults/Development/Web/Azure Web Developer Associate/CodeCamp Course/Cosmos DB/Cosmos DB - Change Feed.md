#azure #az-204 

Change Feed is a Cosmos DB service that monitors changes in all containers.
It can distribute events triggered by those changes to multiple consumers.
It's a persistent record of changes to a container in the order they occur.

Azure has an SDK for:
- .NET
- Java
- Python
- Node.js

Change Feed is *not* supported for Table API, but does support all other [[Cosmos DB - APIs|Cosmos DB APIs]].

Change Feed processor is composed of four components:
1. **Monitor container**
	- Where any insert or update executes
	- Operations are reflected in the change feed
2. **Lease container**
	- Stores states
	- Coordinates change feed processor
3. **The host**
	- An app instance that uses the change feed processor to listen for changes
4. **The delegate**
	- Code that runs when any event in the change feed notifications triggers it

The Change Feed Processor may be hosted among Azure services that support long-running tasks:
- [[Azure App Services - WebJobs|Azure WebJobs]]
- [[CodeCamp - Virtual Machines|Azure Virtual Machines]]
- Azure Kubernetes Services
- Azure .NET hosted services