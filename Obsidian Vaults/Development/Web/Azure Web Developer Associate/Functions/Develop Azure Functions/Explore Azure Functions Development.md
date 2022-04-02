#azure #az-204 #json 

# Explore Azure Functions Development
A function contains two pieces:
1. Code - which can be written in a variety of languages
2. Config - the `function.json` file

Config file is generated automatically from annotations within the code.
For scripting languages, you must provide the config yourself.

The `function.json` file defines:
- Trigger
- Bindings
- Other config settings

Every function has a config file.
Every function has exactly *one* trigger.
The runtime uses the config to determine the events to monitor, as well as how to pass data into the function, and how to return it from the function.
Below is an example config file.

```json
{
	"disabled": false,
	"bindings": [
		// ... bindings go here
		{
			"type": "<bindingType>",
			"direction": "in",
			"name": "<paramName>"
			// ... might be more depending on binding type
		}
	]
}
```

The `bindings` property is where both the `trigger` and any number of `bindings` are set.
All binding types share a few common properties (below), but others have some unique settings.

| Property  | Types  | Comments                                                  |
| --------- | ------ | --------------------------------------------------------- |
| type      | string | Name of binding e.g. "queueTrigger"                       |
| direction | string | Indicates whether the data "in" or "out" bound            |
| name      | string | Name of bound variable within the function e.g. "myQueue" | 

## Function App
Provides an ==execution context== in which functions are run.
It is the ==unit== of deployment and management for functions.
It is comprised of one or more individual functions.
These are all managed, deployed, and scaled together.
They all share the same pricing plan, deployment method, and runtime version.
It is a way to organise and collectively manage functions.

## Folder Structure
The code for all functions in a function app is located in a root project folder.
It contains a host configuration file.
The `host.json` file contains runtime-specific config.
A `bin` folder contains packages and other lib files required by function.
Specific folders required by function depend on language:
- [C# Compiled (.csproj)](https://docs.microsoft.com/en-us/azure/azure-functions/functions-dotnet-class-library#functions-class-library-project)
- [C# script (.csx)](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-csharp#folder-structure)
- [F# script](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-fsharp#folder-structure)
- [Java](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-java#folder-structure)
- [JavaScript](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-node#folder-structure)
- [Python](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python#folder-structure)

## Local Development Environments
Allows you to use your favourite editor and dev tools.
Can write and test functions locally.
Can still connect to live *Azure* services.
Can debug functions locally using full *Functions* runtime.
The way in which you do this depends on your language and tooling preference.