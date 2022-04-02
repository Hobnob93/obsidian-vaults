#azure #az-204 #csharp 

# Send & Wait For Events
Orchestrator functions have the ability to wait and listen for external events.
Useful for handling human interaction or other external triggers.

## Wait For Events
The `WaitForExternalEvent` method of orchestration trigger binding allows for async wait and listen for external event.
Listening orchestrator declares `name` of event and `shape of the data` it expects to receive.

Example below listens for a specific single event and takes action when received.
```cs
[FunctionName("BudgetApproval")]
public static async Task Run(
	[OrchestrationTrigger]
	IDurableOrchestrationContext context)
{
	var approved = await context.WaitForExternalEvent<bool>("Approval");
	if (approved)
	{
		// Approval granted - do something
	}
	else
	{
		// Approval denied - do something else
	}
}
```

## Send Events
The `RaiseEventAsync` method of orchestration client binding sends event that a `WaitForExternalEvent` waits for.
The `RaiseEventAsync` method takes `eventName` and `eventData` as parameters.
Event data **must** be JSON-serialisable.

Example below is of queue-triggered function that sends "Approval" event to orchestrator function instance.
The `instance ID` comes from body of the queue message.
```cs
[FunctionName("ApprovalQueueProcessor")]
public static async Task Run(
	[QueueTrigger("approval-queue")]
	string instanceId,
	[DurableClient]
	IDurableOrchestrationClient client)
{
	await client.RaiseEventAsync(instanceId, "Approval", true);
}
```

Internally, `RaiseEventAsync` enqueues a message that orchestrator function waits for.
If instance is not waiting on specified `event name`, event message added to in-memory queue.
If instance later begins listening for that `event name`, it will check queue for event messages.