#azure #azure-wda #csharp #json #javascript 

# Create Triggers & Bindings
Triggers are what cause a function to run, or how it is invoked.
A function must have *exactly* one trigger.
Nearly always provided as the *payload* to the function.

Binding is a declarative way of connecting another resource to a function.
These are either as `input` or `output` bindings; or `both`.
Data *from* bindings are provided to functions through parameters.

Can mix and match bindings to suit your needs.
They are optional, and can have any number of them.

*Triggers* and *bindings* allow you to avoid hardcoding access to other services.
You receive values via parameters, and you send values by function return.

## Trigger & Binding Definitions
They are defined differently depending on the language.
See below table for examples.

| Language         | They are configured by...                    |
| ---------------- | -------------------------------------------- |
| C# class library | Decorating methods & params with attributes  |
| Java             | Decorating methods & params with annotations |
| JavaScript       | Updating function.js schema                  |
| PowerShell       | Updating function.js schema                  |
| Python           | Updating function.js schema                  |
| TypeScript       | Updating function.js schema                  | 

*Azure Portal* provides UI for adding bindings in ==Integration== tab for languages that rely on `function.js`.
Can also edit file directly in ==Code + test== tab of function.

In C# and Java, parameter determines data type for input data, some examples:
- `string` for text of a queue trigger
- `byte array` for a file read as binary
- `custom type` to deserialise to an object
They *do not* rely on `function.js`.
Can also use *Portal* for editing which is based on C# script, which uses `function.json` instead of attributes.

For dynamically-typed languages, use the `dataType` property in the `function.json` file:
```json
{
	"dataType": "binary",
	"type": "httpTrigger",
	"name": "req",
	"diretion": "in"
}
```
Other options for `dataType` are `string` and `stream`.

## Binding Direction
All triggers and bindings have a `direction` property in `function.json`.
For triggers, direction is *always* `in`.
Input and output bindings use `in` and `out` respectively.
Some support a special direction `inout` - you'll need the ==Advanced editor== via the ==Integrate== tab in *Azure Portal* for this.

When using attributes in a class library, direction is provided in an attribute constructor, or inferred from parameter type.

## Azure Functions Trigger & Binding Example
Suppose you want to write a new row to *Azure Table* storage whenever a new message appears in *Azure Queue* storage.
Here's a `function.json` for this scenario:
```json
{
	"bindings": [
		{
			"type", "queueTrigger",
			"direction": "in",
			"name": "order",
			"queueName": "myqueue-items",
			"connection": "QUEUE_CONN"
		},
		{
			"type": "table",
			"direction": "out",
			"name": "$return",
			"tableName": "outTable",
			"connection": "TABLE_CONN"
		}
	]
}
```

## C# Script Example
Continuing the same example [[#Azure Functions Trigger Binding Example|above]], here is the C# non-class library code that works with this `function.json` config:
```cs
#r "Newtonsoft.Json"

using Microsoft.Extensions.Logging;
using Newtonsoft.Json.Linq;

public static Person Run(JObject order, ILogger log)
{
	return new Person
	{
		PartitionKey = "Orders",
		RowKey = Guid.NewGuid().ToString(),
		Name = order["Name"].ToString(),
		MobileNumber = order["MobileNumber"].ToString()
	};
}
```

## JavaScript Example
Continuing the same example [[#Azure Functions Trigger Binding Example|above]], here is the JavaScript code that works with this `function.json` config:
```js
module.exports = function(context, order) {
	order.PartitionKey = "Orders",
	order.RowKey = generateRandomId(),

	context.done(null, order);
};

function generateRandomId() {
	return Math.random().toString(36).substring(2, 15) +
		Math.random().toString(36).substring(2, 15);
}
```

## C# Class Library
Continuing the same example [[#Azure Functions Trigger Binding Example|above]], here is the C# class library code that works with this `function.json` config:
```cs
public static class QueueTriggerTableOutput
{
	[FunctionName("QueueTriggerTableOutput")]
	[return: Table("outTable", Connection="TABLE_CONN")]
	public static Person Run(
		[QueueTrigger("myqueue-items", Connection="QUEUE_CONN")] JObject order,
		ILogger log)
	{
		return new Person
		{
			PartitionKey = "Orders",
			RowKey = Guid.NewGuid().ToString(),
			Name = order["Name"].ToString(),
			MobileNumber = order["MobileNumber"].ToString()
		};
	}
}
```

## Additional Resources
[Azure Blob storage bindings for Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob)
[Azure Cosmos DB bindings for Azure Functions 2.x](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2)
[Timer trigger for Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer)
[Azure Functions HTTP triggers and bindings](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook)