#azure #az-204 

Normal functions are *stateless*.
Durable Functions are *stateful*.
It's a serverless compute extension of Azure Functions.

The extension introduces two types of functions:
1. **Orchestrator function**
	- Define stateful workflows
	- Implicitly representing state via control flow
2. **Entity function**
	- Manage state of an entity
	- Explicitly representing state

They define workflows in code.
- No JSON schemas or designers are needed
They can other functions synchronously or asynchronously.
- Output from called functions can be saved to local variables
They automatically checkpoint their progress whenever the function awaits.
- Local state is never lost if the process recycles or the VM reboots

## Supported Languages & Installation
To use durable functions, you need to install a library specific to your language into the root of your app project.
Supported languages are:
- C#
	- both precompiled class libraries and C# script
- JavaScript
	- only for version 2.x or later of Azure Functions runtime
	- requires 1.7.0 or later of the Durable Functions extension
- Python
	- requires 2.3.1 or later of the Durable Functions extension
- F#
	- precompiled class libraries and F# script
	- F# script only supported for version 1.x of Azure Functions runtime
- PowerShell
	- supported only for version 3.x of Azure Functions runtime
	- PowerShell 7 requires 2.x of the bundle extensions