#azure #azure-wda #shell #csharp 

# Application Pattern - Async HTTP APIs
Addresses the problem of coordinating state of long-running operations with external clients.
Common way is to have an HTTP endpoint trigger the long-running action.
Then redirect client to a status endpoint which client polls to learn when operation complete.
![[Async HTTP APIs Diagram.png]]

*Durable Functions* provides *built-in* support for this pattern.
Almost entirely removes code you need to write to interact with long-running function executions.
After an instance starts, extension exposes HTTP APIs that query orchestrator function status.
Example below shows REST commands start an orchestrator and query its status - some protocol details removed for clarity.
```shell
> curl -X POST <func-orchestrator-endpoint> -H "Content-Length: 0" -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: <webhook-loc>

{"id": "durable-task-id", ...}

> curl <func-runtime-webhook-loc>/<durable-task-id> -i
HTTP/1.1 202 Accepted
Content-Type: application/json
Location: <durable-task-loc>

{"runtimeStatus":"Running","lastUpdatedTime":"<date-and-time>", ...}

> curl <func-runtime-webhook-loc>/<durable-task-id> -i
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: x

{"runtimeStatus":"Completed","lastUpdatedTime":"<date-and-time>", ...}
```

*Durable Functions* extension exposes built-in HTTP APIs that manage long-running orchestrations.
You can pattern yourself by using own function triggers and the orchestration client binding.

You can use `HttpStart` triggered function to start instances of orchestrator function using a client function.
```cs
public static class HttpStart
{
	[FunctionName("HttpStart")]
	public static async Task<HttpResponseMessage> Run(
		[HttpTrigger(AuthorizationLevel.Function, methods:"post", Route="Route")]
		HttpRequestMessage req,
		[DurableClient]
		IDurableClient starter,
		string functionName,
		ILogger log)
	{
		// Function input comes from request content
		var eventData = await req.Content.ReadAsAsync<object>();
		var instanceId = starter.StartNewAsync(functionName, eventData);

		log.LogInformation($"Started orchestration with ID = '{instanceId}'.");

		return starter.CreateCheckStatusResponse(req, instanceId);
	}
}
```

Function **must** include a `DurableClient` input binding.
Can use client to start and orchestration.
It can also help return HTTP response containing URLs for checking status of new orchestration.