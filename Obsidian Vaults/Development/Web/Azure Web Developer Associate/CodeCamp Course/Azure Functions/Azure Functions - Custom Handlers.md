#azure #az-204 #json 

Lightweight web servers that receive events from the Functions host.
Can be written in any language that supports HTTP primitives.
Ideal for situations where you may need to:
- use a language not supported by existing Azure runtime e.g. Go, Rust, Ruby
- a runtime environment configured for a specific technology e.g. Deno, Ruby on Rails

Within the `functions.json` there is a JSON property called `customHandler` where you define executable path.
Can use triggers and input/output bindings via *extension bundles*.
```json
{
	"version": "2.0",
	"customHandler": {
		"description": {
			"defaultExecutablePath": "handler.exe"
		},
		"enableForwardingHttpRequests": true
	}
}
```

![[Azure Functions - Custom Handler Diagram.png]]

## Application Structure
To implement a custom handler, your functions app must have:
- A `host.json` file at the root of the app
- A `local.settings.json` file at the root of your app
- A `function.json` file for each function (inside a folder that matches the function name)
- A command, script, or executable, which runs a web server

## Azure Functions Runtime is Unreachable Error
Occurs when the Functions runtime can't start.
Most common reason is function app has lost access to its storage account.
Other reasons for the error:
- Storage account was deleted
- Storage account app settings were deleted
- Storage credentials were invalid
- Storage account is inaccessible
- Daily execution quota is full
- App is behind a firewall