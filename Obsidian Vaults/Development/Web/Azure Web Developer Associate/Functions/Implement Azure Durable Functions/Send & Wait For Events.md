#azure #azure-wda #csharp 

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
	IDurableOrchestrationContext context
)
```