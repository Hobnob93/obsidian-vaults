#azure #az-204 #json 

# Explore Task Hubs
In Durable Functions, it is a logical container for durable storage resources.
used for Orchestration and Entities.
An Orchestrator, Activity, or Entity function can only interact with each other when they belong to the *same task hub*.

If multiple function apps share a storage account, each app *must* be configured with a separate task hub name.
A storage account can contain multiple task hubs.
This restriction generally applies to other storage providers as well.

## Azure Storage Resources
A task hub in *Azure Storage* consists of the following resources:
- One or more control queues
- One work-item queue
- One history table
- One instances table
- One storage container with one or more lease blobs
- A storage container with large message payloads, if applicable

All resources created automatically on configured *Azure Storage* account when functions are run or are scheduled to run.

## Task Hub Names
Task hubs are identified by a name that conforms to these rules:
- Contains only alphanumeric characters
- Starts with a letter
- Minimum length of 3 characters
- Maximum length of 45 characters

Task hub name is declared in the `host.json` file, as in the following example:
```json
{
	"version": "2.0",
	"extensions": {
		"durableTask": {
			"hubName": "MyTaskHub"
		}
	}
}
```

Name differentiates one hub from another when there are multiple in a shared storage account.
The names need to be unique if multiple function apps sharing a shared storage account, or apps will compete with each other for messages.
This could lead to undefined behaviour, including "stuck" orchestrators in `pending` or `running` states.