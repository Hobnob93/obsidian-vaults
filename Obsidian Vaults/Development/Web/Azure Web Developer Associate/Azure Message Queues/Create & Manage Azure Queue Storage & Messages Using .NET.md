#azure #az-204 #csharp 

## Create A Queue Service Client
The `QueueClient` enables retrieval of queues in Queue Storage. One way to create it:
```csharp
string connectionString =
	ConfigurationManager.AppSettings["StorageConnectionString"];

QueueClient client = new QueueClient(connectionString, queueName);
```

## Create A Queue
How to create a queue if it does not already exist:
```csharp
client.CreateIfNotExist();
```

## Insert A Message Into A Queue
Use the `SendMessage` method.
A message can be either a string or a byte array.
```csharp
if (client.Exists())
{
	client.SendMessage(message);
}
```

## Peek At The Next Message
Can peek at messages without removing them from the queue using `PeekMessages`.
Default is one message, but can provide more with `maxMessages` optional parameter.
```csharp
if (client.Exists())
{
	PeekedMessage[] peekedMessages = client.PeekMessages();
}
```

## Change Content Of A Queued Message
Can change contents of a message in-place in the queue.
Could use this feature to update status of a work task, for example.
```csharp
if (client.Exists())
{
	QueueMessage[] messages = client.ReceiveMessages(); // 1 by default
	QueueMessage message = messages.First();

	client.UpdateMessage(message.MessageId,
		message.PopReceipt,
		"Updated contents",
		TimeSpan.FromSeconds(60.0)); // Make invisible for 60 seconds
}
```

## Dequeue Next Message
Dequeue a message in two steps.
When you call `ReceiveMessages`, you get the next message in a queue.
The retrieved message is invisible to any other consumers for 30 seconds (by default).
To completely remove from queue, also call `DeleteMessage`.
This two-step process ensures a message that failed to process can be picked up by another consumer to try again.
```csharp
if (client.Exists())
{
	QueueMessage[] messages = client.ReceiveMessages(); // 1 by default
	QueueMessage message = messages.First();

	Console.WriteLine($"Dequeued message: {message.Body}");

	client.DeleteMessage(message.MessageId, message.PopReceipt)
}
```

## Get Queue Length
Can *estimate* number of messages in a queue.
The `GetProperties` method returns queue properties.
The `ApproximateMessagesCount` contains rough number of messages in queue.
This number will never be lower, but could be higher.
```csharp
if (client.Exists())
{
	QueueProperties properties = client.GetProperties();

	int cachedMessagesCount = properties.ApproximateMessagesCount;

	Console.WriteLine($"Approx Num Messages: {cachedMessagesCount}");
}
```

## Delete A Queue
Call `Delete` method to delete a queue and all messages within it.
```csharp
if (client.Exsits())
{
	client.Delete();
}
```