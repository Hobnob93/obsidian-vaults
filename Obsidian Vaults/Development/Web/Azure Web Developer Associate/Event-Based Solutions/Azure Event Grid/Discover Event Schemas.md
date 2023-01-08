#azure #az-204 #json 

## Overview
Events consist of ==four== required string properties.
They are common to all events from any publisher.
Data object has properties that are specific to each publisher.
For system topics, these properties are specific to the resource provider.

Event sources send events to Azure Event Grid in an array.
When posting an event to Event Grid topic, they can have a total size of up to 1MB.
If the payload size is larger, a `413 Payload Too Large` error is returned.
Operations are charged in 64KB increments.

Event Grid sends events to subscribers in an array that has a single event.
Can find the JSON schema for the Event Grid event and each Azure publisher's data payload in the [Event Schema store](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/eventgrid/data-plane).

## Event Schema
The following example shows properties used by all event publishers:
```json
[
	{
		"topic": "string",
		"subject": "string", 
		"id": "string",
		"eventType": "string",
		"eventTime": "string",
		"data": {
			<object unique to each publisher>
		},
		"dataVersion": "string",
		"metadataVersion": "string"
	}
]
```

## Event Properties
All events have the same following top-level data:
| Property        | Required | Description                                            |
| --------------- | -------- | ------------------------------------------------------ |
| topic           | No       | Resource path to event source. Provided by Event Grid. |
| subject         | Yes      | Publisher-defined path to event subject                |
| eventType       | Yes      | Registered event type for event source                 |
| eventTime       | Yes      | Time event generated in UTC                            |
| id              | Yes      | Unique identifier for the event                        |
| data            | No       | Specific to resource provider                          |
| dataVersion     | No       | Schema version of data object. Provided by EG.         |
| metadataVersion | No       | Schema version of metadata. Provided by EG.            |

For custom topics, the publisher determines the data object.
Top-level data should have the same fields as standard resource-defined events.

When publishing events to custom topics, create subjects for events that make it easy for subscribers to know whether they're interested in the event.
Subscribers use filtering to determine interest in subjects.
Consider providing a path for where the event happened, so subscribers can filter by segments of that path.
Path allows for events to narrowly or broadly filter events.

Sometimes subject needs more detail about what happened.
E.g. Storage Accounts publisher provides subject `/blobServices/default/containers/<container-name>/blobs/<file>` when a file is added to a container.
A subscriber could filter by path container to get all events for that container, but not other containers in the same storage account.
A subscriber could also filter by route suffix (e.g. `.txt`).

## CloudEvents v1.0 Schema
In addition to default event schema, Azure Event Grid natively supports events in the JSON implementation of CloudEvents v1.0 and HTTP protocol binding.
CloudEvents is an open specification for describing event data.

CloudEvents simplifies interoperability by providing a common event schema for publishing and consuming cloud based events.
Schema allows for uniform tooling, standard ways of routing & handling events, and universal ways of deserialising the outer event schema.
Can more easily integrate work across platforms.

An example of an Azure Blob Storage event in CloudEvents format:
```json
{
	"specversion": "1.0",
	"type": "Microsoft.Storage.BlobCreated",
	"source": "<path-to-storage-account>",
	"id": "9aeb0fdf-c01e-0131-0922-9eb54906e209",
	"time": "2019-11-18T15:13:39.4589254Z",
	"subject": "blobServices/default/containers/{container}/blobs/{new-file}",
	"dataschema": "#",
	"data": {
		
	}
}
```