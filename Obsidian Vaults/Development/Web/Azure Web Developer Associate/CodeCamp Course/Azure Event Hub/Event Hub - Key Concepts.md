#azure #az-204 

Azure Event Hub helps you build your big data pipeline to analyse logging, anomalies, user, and device telemetry.
You only *pay* for what you *use*.

Azure Event Hub Key Concepts
- **Namespace**
	- an endpoint for receiving and distributing events to event hubs
- **Event Hub**
	- where events will be delivered
- **Event Hub Cluster**
	- a dedicated Event Hub with 99.99% SLA
- **Event Hub Capture**
	- allows you to automatically capture and save streaming events
	- see [[Event Hub - Entities#Capture]]
- **Event Hub for Apache Kafka**
	- endpoints are compatible with Apache Kafka
	- see [[Event Hub - Kafka Compatibility]]
- **Event Publishers**
	- apps or services that publish event to an Event Hub
	- see [[Event Hub - Producers]]
- **Publisher Policy**
	- a unique ID used to identify publishers
- **Partitions**
	- used to organise the sequence of events in an Event Hub
	- see [[Event Hub - Partitions]]
- **Event Consumers**
	- apps or services that read events from an Event Hub
	- see [[Event Hub - Consumers]]
- **Consumer Group**
	- enable consuming apps to each have a separate view of the event stream
	- see [[Event Hub - Consumer Groups]]
- **Stream Offset**
	- holds the position of event inside a partition
- **Checkpointing**
	- process of distinguishing between read and unread events