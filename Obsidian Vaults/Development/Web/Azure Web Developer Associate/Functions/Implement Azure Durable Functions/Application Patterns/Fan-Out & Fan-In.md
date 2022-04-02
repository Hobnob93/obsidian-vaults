#azure #az-204 #csharp 

# Application Pattern - Fan-Out & Fan-In
Execute multiple functions in parallel, then wait for all functions to finish.
Often, some aggregation work is done on the results from all functions.
![[Fan Out & Fan In Diagram.png]]

With normal functions, you can fan out by sending multiple messages to a queue.
To fan in, you'd track when queue-triggered functions end, then store function outputs.

In example below, fan-out is distributed to multiple instances of the `F2` function.
Work is tracked using dynamic list of tasks.
The `Task.WhenAll` .NET API or JavaScript `context.df.Task.all` API is called to wait for all functions to complete.
The `F2` function outputs are aggregated from the dynamic task list and passed to the `F3` function.

```cs
[FunctionName("FanOutFanIn")]
public static async Task Run(
	[OrchestrationTrigger]
	IDurableOrchestrationContext context)
{
	var parallelTasks = new List<Task<int>>();
	
	// Get a list of N work items to process in parallel
	var workBatch = await context.CallActivityAsync<object[]>("F1", null);
	for (var i = 0; i < workBatch.Length; i++)
	{
		var task = context.CallActivityAsync<int>("F2", workBatch[i]);
		parallelTasks.Add(task);
	}

	await Task.WhenAll(parallelTasks);

	// Aggregate all N outputs and send result to F3
	var sum = parallelTasks.Sum(t => t.Result);
	await context.CallActivitgyAsync("F3", sum);
}
```

Automatic checkpointing happens at the `await` or `yield` call on `Task.WhenAll` or `context.df.Task.all`.
Ensures that a potential midway crash or reboot doesn't require restarting an already completed task.