#azure #azure-wda 

# Explore Durable Functions App Patterns
It's an extension of functions.
Lets you define stateful workflows by writing ==orchestrator functions==.
Combines with stateful entities through ==entity functions==.
Uses the *Azure Functions* programming model.
The extension manages state, checkpoints, and restarts.

## Supported Languages
The following languages are supported:
- `C#`: both libraries and scripts
- `JavaScript`: supported only for version 2.x of *Azure Functions* runtime - requires version 1.7 or later of Durable Functions extension
- `Python`: requires 2.3.1 or later of Durable Functions extension
- `F#`: class libraries and scripts - only supported for version 1.x of *Azure Functions* runtime
- `PowerShell`: Supported only for version 3.x of *Azure Functions* runtime and PowerShell7 - required 2.x for bundle extensions

## Application Patterns
Primary use of *Durable Functions* is simplifying complex, stateful requirements in serverless applications.
The following sections describe typical application patterns that benefit from *Durable Functions*:
- [[Function Chaining]]
- [[Fan-Out & Fan-In]]
- [[Async HTTP APIs]]
- [[Monitor]]
- [[Human Interaction]]

## Additional Resources
Differences between *Durable Functions* 1.x and 2.x:
[Durable Functions version overview](https://docs.microsoft.com/en-us/azure/azure-functions/durable/durable-functions-versions)