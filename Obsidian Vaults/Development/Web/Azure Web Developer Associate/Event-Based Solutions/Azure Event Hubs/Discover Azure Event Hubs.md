#azure #az-204 

## Overview
Event Hubs is the "front door" for an event pipeline.
Often called an __event ingestor__ in solution architectures.
- A component or service that sits between publishers and event consumers
- Decouples production of event stream from consumption of those events
Event Hubs provides a unified streaming platform, with:
- Time retention buffer
- Decoupling event producers from consumers

Key features of Azure Event Hubs service:
- __Fully managed PaaS__
	- Event Hubs is a fully managed Platform-as-a-Service (PaaS)
	- Little configuration or management overhead
	- Event Hubs for Apache Kafka ecosystems gives you the PaaS Kafka experience without having to manage, configure, or run your clusters
- __Real-time and batch processing__
	- Event Hubs uses a partitioned consumer model
	- Enabled multiple applications to process the stream concurrently
	- Lets you control the speed of processing
- __Scalable__
	- Scaling options, like auto-inflate, scale number of throughput units to meet usage needs
- __Rich ecosystem__
	- Event Hubs for Apache Kafka ecosystems enables Apache Kafka (1.0 and later) clients and apps to talk to Event Hubs
	- No need to set up, configure, and manage your own Kafka clusters

## Key Concepts
Event Hubs contains the following components:
- __Event Hubs client__
	- Primary interface for devs interacting with Event Hubs client library
	- Several different clients, each dedicated to a specific use of Event Hubs
		- Such as publishing or consuming events
- __Event Hubs producer__
	- Type of client
	- Serves as a source of:
		- telemetry data
		- diagnostics information
		- usage logs or other log data
	- As part of:
		- an embedded device solution:
		- a mobile app
		- a game running on a console or other device
		- a client or server based business solution
		- a web site
- __Event Hubs consumer__
	- Type of client
	- Reads information from hub and allows processing of it
	- Processing may involve aggregation, complex computation, or filtering
	- May also involve distribution or storage of information either raw or transformed
	- Consumers are often robust and high-scale platform infrastructure parts with built-in analytics capabilities, like Azure Stream Analytics, Apache Spark
- __Partition__
	- Ordered sequence of events held in a hub
	- A means of data organisation associated with parallelism required by consumers
	- Hubs provides message streaming through partitioned consumer pattern
		- Each consumer only reads a subset, or partition, of the message stream
	- As newer events arrive, they are added to the end of the sequence
	- Number of partitions is specified at time of Hub creation and _cannot be changed_
- __Consumer group__
	- A view of an entire Hub
	- Enable multiple consuming apps to each have a separate view of the event stream
	- Can read the stream independently at their own pace and from their own position
	- Can be at most 5 concurrent readers on a partition per consumer group
		- It is recommended that there is only one active consumer for a given partition and consumer group pairing
	- Each active reader receives all events from its partition
		- If there are multiple readers on same partition, they will all receive duplicate events
- __Event receivers__
	- Any entity that reads data from a Hub
	- All Hubs consumers connect via the AMQP 1.0 session
	- Event Hubs service delivers events through a session as they become available
	- All Kafka consumers connect via Kafka protocol 1.0 and later
- __Throughput units__ or __Processing units__
	- Pre-purchased units of capacity
	- Controls the throughput of Event Hubs

## Event Hubs Stream Processing Architecture
![[Event Hubs Stream Processing Architecture Diagram.png]]