#azure #az-204 #csharp 

A producer (a.k.a. publisher) emits data to the stream.
Publishers can publish events using the following protocols:
- HTTPS
	- Most Azure SDKs use HTTPS
	- Requires additional TLS (transport level security) overhead for every request
- AMQP 1.0
	- Requires establishment of a persistent bidirectional socket
	- Also requires TLS or SSL/TLS
	- Has a higher network cost when initialising the session
	- Higher performance for frequent publishers
	- Can achieve much lower latencies with async publishing
- Kafka Protocol

You can publish events either:
- one at a time
- as a batch

There is a limit of 1 MB, regardless of sending one message at a time or as a batch.
Events greater than 1 MB will be rejected.

For authorisation, publishers use either:
- Azure AD with OAuth2-issued JWT tokens
- Shared Access Signature (SAS)

There are also **publisher policies**.
Enables granular control over event publishers.
- Policies are run-time features designed to facilitate large numbers of independent event publishers
- Each publisher uses its own unique identifier when publishing

Generally you'll be using the Azure SDK to publish events:
```cs
const string ConnString = "EventHubsNamespaceConnString";
const string EventHubName = "EventHubName";

public static async Task Main()
{
	var producer = new EventHubProducerClient(ConnString, EventHubName);

	var batch = await producer.CreateBatch();
	batch.TryAdd(new { body: "First Event" });
	batch.TryAdd(new { body: "Second Event" });
	batch.TryAdd(new { body: "Third Event" });

	await producer.SendBatch(batch);

	await producer.Close();
}
```