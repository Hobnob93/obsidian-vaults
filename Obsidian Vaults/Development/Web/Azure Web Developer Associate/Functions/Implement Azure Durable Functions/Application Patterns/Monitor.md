#azure #azure-wda #csharp 

# Application Pattern - Monitor
Refers to a flexible, recurring process in a workflow.
Polling until specific conditions are met, as an example.
Can use regular timer trigger to address basic scenario, but its interval is static and managing instances becomes complex.
Can use *Durable Functions* to create flexible recurrence intervals, manage task lifetimes, and create multiple monitor processes from a single orchestration.
![[Monitor Diagram.png]]

See below for code that creates multiple monitors that observe arbitrary endpoints.
Monitors can end execution when a condition is met, or another function can use the orchestration client to terminate monitors.
Can change monitor's `wait` interval based on specific condition, such as ==exponential backoff==.
```cs
[FunctionName("MonitorJobStatus")]
public static async Task Run(
	[OrchestrationTrigger]
	IDurableOrchestrationContext context)
{
	var jobId = context.GetInput<int>();
	var pollingInterval = GetPollingInterval();
	var expiryTime = GetExpiryTime();

	while (context.CurrentUtcDateTime < expiryTime)
	{
		var jobStatus = 
			await context.CallActivityAsync<string>("GetJobStatus", jobId);
		if (jobStatus == "Completed")
		{
			// Perform an action when a condition is met
			await context.CallActivityAsync("SendAlert", machineId);
			break;
		}

		// Orchestration sleeps until this time
		var nextCheck = context.CurrentUtcDateTime.AddSeconds(pollingInterval);
		await context.CreateTimer(nextCheck, CancellationToken.None);
	}

	// Perform work here, or let orchestration end
}
```