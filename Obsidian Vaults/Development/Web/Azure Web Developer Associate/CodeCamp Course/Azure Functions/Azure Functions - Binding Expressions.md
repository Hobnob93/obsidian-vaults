#azure #az-204 #json 

In the `function.json` file, and in function parameters and code, you can use *binding expressions* that resolve to values from various sources.

*Most* expressions are identified by wrapping them in curly braces.
- e.g. `container/{queueTrigger}`

Types of binding expressions
- App settings (usus `% %` instead of `{ }`)
- Trigger file name
- Trigger metadata
- JSON payloads
- New GUID
- Current date and time

## App Settings Example
Want to change config based on environment.
```json
{
	"bindings": [
		{
			"name": "order",
			"type": "queueTrigger",
			"direction": "in",
			"queueName": "%input_queue_name%",
			"connection": "STORAGE_CONN"
		}
	]
}
```

## Trigger Filename Example
Change path of file name, works for both in and out directions.
```json
{
	"bindings": [
		{
			"name": "image",
			"type": "blobTrigger",
			"path": "sample-images/{filename}",
			"direction": "in",
			"connection": "STORAGE_CONN"
		}
	]
}
```

## Trigger Metadata Example
Many triggers provide additional metadata values.
These can be used as input parameters in C# or F#, or properties on the `context.bindings` object in JavaScript.
E.g. Azure Queue storage trigger supports the following properties:
- QueueTrigger
- DequeueCount
- ExpirationTime
- Id
- InsertionTime
- NextVisibleTime
- PopReceipt

JSON below uses QueueTrigger metadata.
```json
{
	"bindings": [
		{
			"name": "myQueueItem",
			"type": "queueTrigger",
			"queueName": "myqueue-items",
			"connectionn": "STORAGE_CONN"
		},
		{
			"name": "myInputBlob",
			"type": "blob",
			"path": "samples-workitems/{queueTrigger}",
			"direction": "in",
			"connection": "STORAGE_CONN"
		}
	]
}
```

## JSON Payloads Example
When a trigger payload is JSON, you can refer to its properties in configuration for other bindings in the same function, and in function code.
E.g. webhook function that receives a blob name in JSON:
	`{ "BlobName": "HelloWorld.txt" }`

If some properties in your JSON payload are objects with properties, you can use the `.` notation to refer to them.
```json
{
	"bindings": [
		{
			"name": "info",
			"type": "httpTrigger",
			"direction": "in",
			"webHookType": "genericJson"
		},
		{
			"name": "blobContents",
			"type": "blob",
			"direction": "in",
			"path": "strings/{BlobName}",
			"connection": "STORAGE_CONN"
		},
		{
			"name": "res",
			"type": "http",
			"direction": "out"
		}
	]
}
```

## New GUID Example
Produces a globally unique identifier in its place.
```json
{
	"type": "blob",
	"name": "blobOutput",
	"direction": "out",
	"path": "my-output-container/{rand-guid}.txt"
}
```

## Current Date & Time Example
Produces the current date and time in the format: `YYYY-MM-ddTHH:mm:ssZ`
```json
{
	"type": "blob",
	"name": "blobOutput",
	"direction": "out",
	"path": "my-output-container/{DateTime}.txt"
}
```