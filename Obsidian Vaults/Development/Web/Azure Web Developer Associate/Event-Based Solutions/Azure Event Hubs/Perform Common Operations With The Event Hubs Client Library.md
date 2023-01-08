#azure #az-204 #csharp 

## Inspect An Event Hub
Many Hub operations take place within scope of a partition.
As partitions are owned by Event Hub, their names are assigned at time of creation.
Query Hub using on of the Hub clients to find what partitions are available.
```csharp
var connectionString = "conn-string-for-event-hubs-namespace";
var eventHubName = "name-of-event-hub";

await using (var producer = new EventHubProducerClient(connectionString, eventHubName))
{
	string[] partitionIds = await producer.GetPartitionIdsAsync();
}
```

## Publish Events To An Event Hub
Producers publish events in batches and may request a specific partition.
Or it may allow Hubs service to decide which partition events should be published to.
Using automatic routing is recommended when publishing events needs to be highly available, or when event data should be distributed evenly among the partitions.
```csharp
var connectionString = "conn-string-for-event-hubs-namespace";
var eventHubName = "name-of-event-hub";

await using (var producer = new EventHubProducerClient(connectionString, eventHubName))
{
	using EventDataBatch eventBatch = await producer.CreateBatchAsync();
	eventBatch.TryAdd(new EventData(new BinaryData("First")));
	eventBatch.TryAdd(new EventData(new BinaryData("Second")));
	
	await producer.SendAsync(eventBatch);
}
```

## Read Events From An Event Hub
Need to create a client for a given consumer group.
When Hub is created, it provides default consumer group that can be used to get started.
```csharp
var connectionString = "conn-string-for-event-hubs-namespace";
var eventHubName = "name-of-event-hub";

string consumerGroup = EventhubConsumerClient.DefaultConsumerGroupName;

await using (var consumer = new EventHubConsumerClient(consumerGroup, connectionString, eventHubName))
{
	using var cancellationSource = new CancellationTokenSource();
	cancellationSource.CancelAfter(TimeSpan.FromSeconds(45));

	await foreach (PartitionEvent receivedEvent in 
		consumer.ReadEventsAsync(cancellationSource.Token))
	{
		// Loop will wait for events to be available in Hub
		// When event available, loop will iterate with event that was received
		// We did not specify max wait time, loop will wait forever
		// unless cancellation is requested using cancellation token
	}
}
```

## Read Events From An Event Hub Partition
To read from a specific partition, consumer will need to specify where in event stream to begin receiving events.
```csharp
var connectionString = "conn-string-for-event-hubs-namespace";
var eventHubName = "name-of-event-hub";

string consumerGroup = EventhubConsumerClient.DefaultConsumerGroupName;

await using (var consumer = new EventHubConsumerClient(consumerGroup, connectionString, eventHubName))
{
	EventPosition startPos = EventPosition.Earliest;
	string partitionId = (await consumer.GetPartitionIdsAsync()).First();

	using var cancellationSource = new CancellationTokenSource();
	cancellationSource.CancelAfter(TimeSpan.FromSeconds(45));

	await foreach (PartitionEvent receivedEvent in 
		consumer.ReadEventsFromPartitionAsync(partitionId, startPos,
		cancellationSource.Token))
	{
		// Loop will wait for events to be available in Hub
		// When event available, loop will iterate with event that was received
		// We did not specify max wait time, loop will wait forever
		// unless cancellation is requested using cancellation token
	}
}
```

## Process Events Using An Event Processor Client
For most prod scenarios, it is recommended the `EventProcessorClient` is used for reading and processing events.
Since the client has dependency on Azure Storage blobs for persistence of its state, you'll need to provide a `BlobContainerClient` for the processor.
```csharp
var cancellationSource = new CancellationTokenSource();
cancellationSource.CancelAfter(TimeSpan.FromSeconds(45));

var strgConnString = "conn-string-for-storage";
var blobContName = "name-of-blob-container";

var hubsConnString = "conn-string-for-event-hubs";
var eventHubName = "name-of-event-hub";
var consumerGroup = "name-of-hub-consumer-group";

Task processEventHandler(ProcessEventArgs eventArgs) => Task.CompletedTask;
Task processErrorHandler(ProcessErrorEventArgs eventArgs) => Task.CompletedTask;

var strgClient = new BlobContainerClient(strgConnString, blobContname);
var processor = new EventProcessorClient(strgClient, consumerGroup,
	hubsConnString, eventHubName);

processor.ProcessEventAsync += processEventHandler;
processor.ProcessErrorAsync += processErrorHandler;

await processor.StartProcessingAsync();

try
{
	// Processor performs its work in background; block until cancellation
	// to allow processing to take place

	await Task.Delay(Timeout.Infinite, cancellationSource.Token);
}
catch (TaskCanceledException)
{
	// This is expected when delay is canceled
}

try
{
	await processor.StopProcessingAsync();
}
finally
{
	// Prevent leaks

	processor.ProcessEventAsync -= processEventHandler;
	processor.ProcessErrorAsync -= processErrorHandler;
}
```