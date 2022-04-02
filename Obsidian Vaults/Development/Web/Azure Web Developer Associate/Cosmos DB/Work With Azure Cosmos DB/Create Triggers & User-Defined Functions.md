#azure #az-204 #javascript 

# Create Triggers & User-Defined Functions
*Azure Cosmos DB* supports ==pre-triggers== and ==post-triggers==.
Pre-triggers executed *before* modifying a database item.
Post-triggers executed *after* modifying a database item.
They are *not* automatically executed; must be specified for each operation where you want them to be executed.
Need to register a trigger using the *Cosmos DB* SDK.

## Pre-Triggers
Following example shows how a pre-trigger is used to validate properties of an item being created.
It adds a timestamp property to a newly added item if it doesn't contain one.
```js
function validateToDoItemTimestamp() {
	var context = getContext();
	var request = context.getRequest();
	
	var itemToCreate = request.getBody();
	
	if (!("timestamp" in itemToCreate)) {
		var ts = new Date();
		itemToCreate["timestamp"] = ts.getTime();
	}

	request.setBody(itemToCreate);
}
```

They *cannot* have any input parameters.
The `request` object used to manipulate request message with associated operation.

When triggers are registered, you can specify operations that it can run with.
This trigger should be created with `TriggerOperation` value of `TriggerOperation.Create`.
This means using the trigger in a replace operation shown in following example is not permitted.

## Post-Triggers
Example below shows a post-trigger.
Trigger queries metadata item and updates it with details about newly created item.
```js
function updateMetadata() {
	var context = getContext();
	var container = context.getCollection();
	var response = context.getResponse();

	var createdItem = response.getBody();

	var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
	var accept = container.queryDocuments(
		container.getSelfLink(),
		filterQuery,
		updateMetadataCallback);
	if (!accept)
		throw 'Unable to update metadata; abort';

	function updateMetadataCallback(err, items, responseOptions) {
		if (err)
			throw new Error("Error: " + error.message);

		if (items.length != 1)
			throw 'Unable to find metadata document';

		var metadataItem = items[0];
		metadataItem.createdItems += 1;
		metadataItem.createdNames += " " + createdItem.id;
		var accept = container.replaceDocument(
			metadataItem._self,
			metadataItem,
			function(err, itemReplaced) {
				if (err)
					throw 'Unable to update metadata; abort';
			});
		if (!accept)
			throw 'Unable to update metadata; abort';

		return;
	}
}
```

One thing to note is the transactional execution of triggers.
Post-trigger runs as part of same transaction for the underlying item itself.
An exception during post-trigger will fail the whole transaction.
Anything committed will be rolled back and an exception returned.

## User-Defined Functions
The following creates a UDF to calculate income tax for various income brackets.
User-defined function would then be used inside a query.
For this example, there is a container called "Incomes" with the following properties:
```json
{
	"name": "User One",
	"country": "USA",
	"income": 70000
}
```

The following function definition created to calculate income tax for various brackets:
```js
function tax(income) {
	if (income == undefined)
		throw 'no input';

	if (income < 1000)
		return income * 0.1;
		
	if (income < 10000)
		return income * 0.2;

	return income * 0.4;
}
```