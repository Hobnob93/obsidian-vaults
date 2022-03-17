#azure #azure-wda 

# Compare Azure Functions Hosting Options
When creating a *Function App*, you must choose a hosting plan.
Available hosting plans are: Consumption plan, Functions Premium Plan, or a Dedicated [[Examine Azure App Service Plans|App Service Plan]].
All plans are available on both Linux and Windows VMs.

The hosting plan dictates the following behaviours:
- How function app is scaled
- Resources available to each function app instance
- Support for advanced functionality, such as *Azure Virtual Network* connectivity

Here is a summary of the benefits for the 3 main types of hosting plans:
- `Consumption plan`
	- The default hosting plan
	- Scales automatically
	- Only pay for compute resources when functions are running
	- Frequency of incoming events my dynamically add or remove ==Functions host== instances
- `Functions Premium plan`
	- Automatically scales based on demand
	- Uses pre-warmed workers, which run apps without delay
	- runs on more powerful instances
	- Connects to virtual networks
- `App Service plan`
	- Uses regular app plan rates
	- Best for long-running scenarios where ==Durable Functions== can't be used

There are two other hosting options for ==control== and ==isolation==:
- `ASE` (App Service Environment)
	- *App Service* feature providing fully isolated and dedicated environments
	- Runs app securely and at high scale
- `Kubernetes`
	- Provides a fully isolated and dedicated environment
	- Runs on Kubernetes platform

## Always On
If you use *App Service* plan, you should enable `Always On` setting so the function runs correctly.
The function's runtime goes idle after a few minutes of inactivity, so only HTTP triggers will "wake up" functions.
Setting is *only* available on *App Service* plan.
On a Consumption plan, platform activates function apps automatically.

## Storage Account Requirements
A function app requires a general *Azure Storage* account; supporting *Azure Blob*, *Queue*, *Files*, and *Table* storage.
*Functions* relies on storage for managing triggers, and logging function executions.
Some storage accounts *do not* support queues and tables, such as blob-only accounts.

You can use the same storage account for application data.
However, for storage-intensive operations, you should use a separate storage account.