#azure #azure-wda #csharp 

# Application Pattern - Function Chaining
A sequence of functions executes in a specific order.
The output of one pattern is input of the next function.
![[Function Chaining Diagram.png]]

In the example below, `F1`, `F2`, `F3`, and `F4` are names of other functions in function app.
Can implement flow control using normal imperative coding constructs.
Code can use semantics like conditionals and loops.
Can also include error handling with `try`/`catch`/`finally` blocks.

```cs
[FunctionName("Chaining")]
public static async Task<object> Run(
	[OrchestrationTrigger]
	IDurableOrchestrationContext context)
{
	try
	{
		var x = await context.CallActivityAsync<object>("F1", null);
		var y = await context.CallActivityAsync<object>("F2", x);
		var z = await context.CallActivityAsync<object>("F3", y);
		return await context.CallActivityAsync<object>("F4", z);
	}
	catch (Exception ex)
	{
		// Error handling here
	}
}
```