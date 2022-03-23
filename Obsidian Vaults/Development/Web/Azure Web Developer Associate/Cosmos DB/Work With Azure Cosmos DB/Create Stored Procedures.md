#azure #azure-wda #javascript 

# Create Stored Procedures
*Azure Cosmos DB* provides language-integrated, transactional execution of *JavaScript*.
This lets you write ==stored procedures==, ==triggers==, and ==functions==.
These need to be *registered* in order to be called.

## Writing Stored Procedures
Stored procs can create, read, query, and delete items inside a container.
They are registered per collection.
They can operate on any document or attachment present in that collection.

A simple stored proc that returns "Hello, World":
```js
var helloWorldStoredProc = {
	id: "helloWorld",
	serverScript: function() {
		var context = getContext();
		var response = context.getResponse();

		response.setBody("Hello, World");
	}
}
```
The `context` object provides access to all operations within *Cosmos DB*.
Also provides access to request and response objects.
In this case, can use the `response` object to set the body to be sent back to the client.

## Create An Item Using Stored Procedure
When creating an item via proc, it is inserted into the container and an ID for the new item is returned.
Creating an item is an async operation and depends on the callback functions.
The callback function has two parameters:
- The error object in case operation fails
- A return value

Inside callback, you can either handle exception or throw an error.
If callback not provided, and there is an error, the *Cosmos DB* runtime will throw an error.

Stored proc includes a parameter to set the description.
- When `true`, and description missing, stored proc will throw an exception
- Otherwise, proc continues to run regardless

Following example takes input named `documentToCreate`.
Parameter's value is body of document to be created in current collection.
Callback throws error if operation fails.
Otherwise, `id` of the created doc is set as response body.
```js
function createSampleDocument(documentToCreate) {
	var context = getContext();
	var collection = context.GetCollection();
	var accepted = collection.createDocument(
		collection.getSelfLink(),
		documentToCreate,
		function(error, documentCreated) {
			context.getResponse().setBody(documentCreated.Id)
		}
	);
	
	if (!accepted)
		return;
}
```

## Array As Input Parameters for Stored Procedures
When defining a stored proc, input params are always sent as `string` to the proc.
Even if you pass an array of strings, array is converted into a string and sent to proc.
To get the array values, you'll need to parse the string into an array, such as the example below:
```js
function sample(arr) {
	if (typeof arr === "string")
		arr = JSON.parse(arr);

	arr.forEach(function(a) {
		console.log(a);
	})
}
```

## Bounded Execution
All *Cosmos DB* operations must complete within a limited amount of time.
Stored procs have limited time with which to run on the server.
All collection functions return a boolean representing whether operation will complete or not.

## Transactions Within Stored Procedures
Can implement transactions on items within container by using a stored proc.
JS functions implement a continuation-based model to batch or resume execution.
Continuation value can by any value of choice, and apps can use it to resume a transaction from a new starting point.

Diagram below depicts how transaction continuation model can be used to repeat server-side function until it finishes processing workload:
![[Transactions In Stored Procs Diagram.png]]