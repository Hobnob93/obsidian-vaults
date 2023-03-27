#azure #az-204 #csharp 

A consumer (a.k.a. reader) receives data from the stream to process.
All Event Hub consumers connect via the AMQP 1.0 session.
Events are delivered through session as they become available.

The client does not need to poll for data availability:
```cs
const string StorageContainerConnString = "StorageeConnString";
const string ContainerName = "ContainerName";

const string ConsumerGroup = "ConsumerGroup";
const string HubConnString = "EventHubConnString";
const string EventHubName = "EventHubName";

public static async Task Main()
{
	var containerClient = new ContainerClient(StorageContainerConnString);
	var checkpointStore = new BlobCheckpointStore(containerClient);
	var consumerClient = new EventHubConsumerClient(ConsumerGroup,
		HubConnString, EventHubName, checkpointStore);

	consumerClient.ProcessEvents += ProcessEvent;
	consumerClient.ProcessError += ProcessError;
}

private static async Task ProcessEvent(Event[] events, Context context)
{
	if (events.Length == 0)
	{
		Console.WriteLine("No events received yet - waiting for next interval");
		return;
	}

	foreach (var evt in events)
		Console.WriteLine($"Event: {evt.Body}");

	await context.UpdateCheckpoint(events[events.Length - 1]);
}

private static async Task ProcessError(string error, Context context)
{
	Console.WriteLine($"Error: {error}");
}
```