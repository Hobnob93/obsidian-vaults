#azure #azure-wda #csharp 

# Control Timing in Durable Functions
Create a *durable timer* by calling the `CreateTimer` method.
The method returns a `Task` that completes on a specified time and date.

## Timer Limitations
The *durable Task Framework* enqueues a message that only becomes visible at the time of when the timer expires.
When running on [[Compare Azure Functions Hosting Options|Consumption Plan]], newly visible timer message will ensure function app gets activated on an appropriate VM.

## Usage For Delay
Example below illustrates durable timer use for delaying execution.
Example is issuing a billing notification every 10 days.
```cs
[FunctionName("BillingIssuer")]
public static async Task Run(
	[OrchestrationTrigger]
	IDurableOrchestrationContext context)
{
	for (var = i; i < 10; i++)
	{
		var deadline = context.CurrentUtcDateTime.Add(TimeSpan.FromDays(1));
		await context.CreateTimer(deadline, ConacellationToken.None);
		await context.CallActivityAsync("SendBillingEvent");
	}
}
```

## Usage For Timeout
Example illustrates using durable timers to implement timeouts.
```cs
[FunctionName("TryGetQuote")]
public static async Task<bool> Run(
	[OrchestrationTrigger]
	IDurableOrchestrationContext context)
{
	var timeout = TimeSpan.FromSecnds(30);
	var deadline = context.CurrentUtcDateTime.Add(timeout);

	using var cts = new CancellationTokenSource();
	var activityTask = context.CallActivityAsync("GetQuote");
	var timeoutTask = context.CreateTimer(deadline, cts.Token);

	var winner = await Task.WhenAny(activityTask, timeoutTask);
	if (winner == activityTask)
	{
		// Success case
		cts.Cancel();
		return true;
	}
	else
	{
		// Timeout case
		return false;
	}
}
```

Ensure you `Cancel()` timeout task as otherwise orchestration will not "complete" while subtasks are still running.

The approach above won't cancel the queued activity on timeout, it just allows it to ignore the result and move on.