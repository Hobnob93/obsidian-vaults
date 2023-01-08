#azure #az-204 

## Overview
To scale your event processing app, you can run multiple instances of the app and have it balance the load among themselves.
In older versions, `EventProcessorHost` allowed you to balance load between multiple instances of your program and checkpoint events when receiving.
In the newer versions (5.0 onwards), `EventProcessorClient` (.NET and Java), or `EventHubConsumerClient` (Python and JavaScript) allows you to do the same.

## Example Scenario
Consider a home security that monitors 100,000 homes.
Every minute, it gets data from various sensors such as motion detector, door/window open sensor, etc.
Company provides a web site for residents to monitor the activity of their home in near real time.

Each sensor pushes data to Event Hub.
Event Hub is configured with 16 partitions.
You need a mechanism that can read (consume) these events, consolidate them, and dump the aggregate to a storage blob, which is then projected to a user-friendly web page.

When designing the consumer in a distributed environment, the scenario must handle:
- __Scale__
	- Create multiple consumers
	- Each taking ownership of reading from a few Event Hubs partitions
- __Load balance__
	- Increase or reduce consumers dynamically
	- E.g. when a new sensor type is added to each home, number of events increases
	- In that case, the operator (a human) increases the number of consumer instances
	- Then, the pool of consumers can rebalance the number of partitions they own, to share the load with newly added consumers
- __Seamless resume on failures__
	- If a consumer fails, then other consumers can pick up partitions owned by this failed one and continue
	- The continuation point, called a _checkpoint_ or _offset_, should be at the exact point in which the consumer failed, or slightly before
- __Consume events__
	- While previous points deal with management of the consumer, there needs to be code to actually consume the events and do something with it
	- Such as aggregate and upload to blob storage

## Event Processor or Consumer Client
You don't need to build your own solution to meet these requirements.
Azure Event Hubs SDKs provide this functionality.
In .NET or Java, you can use `EventProcessorClient`.
In Python and JavaScript, you can use `EventHubConsumerClient`.

For most production scenarios, it's recommended to use the event processor client for reading and processing events.
Event processor clients can work cooperatively within the context of a consumer group for a given event hub.
Clients will automatically manage distribution and balancing of work as instances become available or unavailable for the group.

## Partition Ownership Tracking
An event processor instance typically owns and processes events from one or more partitions.
Ownership of partitions is evenly distributed among all active event processor instances associated with an event hub and consumer group combination.

Each processor is given a UID and claims ownership of partitions by adding or updating an entry in a checkpoint store.
All processor instances communicate with this store periodically to update its own processing state & learn about other active instances.
This is used to balance the load among active processors.

## Receive Messages
When you create a processor, you specify functions that will process events and errors.
Each call to the function that processes events delivers a single event from a specific partition.
Your responsibility to handle this event.
To ensure consumer processor processes every message at least once, need to write your own retry logic - but be cautious about poisoned messages.

Recommend to do things relatively fast - i.e. as little processing as possible.
If you need to write to storage and do some routing, it's better to use two consumer groups and have two event processors.

## Checkpoints
_Checkpointing_ is when a processor marks or commits the position of the last successfully processed event within a partition.
Marking a checkpoint is typically done within the function that processes the events and occurs on a per-partition basis within a consumer group.

If a processor disconnects from a partition, another instance can resume processing at the checkpoint previously committed.
When processor connects, it passes the offset to the event hub to specify location at which to start reading.
Can use checkpointing to mark events as "complete" by downstream applications, and to provide resiliency when an event processor goes down.
It's possible to return to older data by specifying a lower offset from this checkpointing process.

## Thread Safety & Processor Instances
By default, the function that processes the events is called sequentially for a given partition.
Subsequent events and calls to this function from the same partition form a queue behind the scenes as the event pump continues to run in the background on other threads.
Events from different partitions can be processed concurrently and any shared state that is accessed across partitions have to be synchronised.