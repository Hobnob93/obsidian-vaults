#azure #az-204 #cli 

Azure Functions Core Tools lets you develop and test your functions on your local computer.
Uses the command prompt or terminal.

Run the command `func`, and it will begin running.
It allows you to do a whole host of things.

## Top-Level Commands
`func init`
- Creates a new Functions project in a specific language
`func new`
- Creates a new function in the current project based on a template
`func start`
- Starts local runtime host and loads function project in the current folder
`func run`
- Enables you to invoke a function directly
- Similar to running a function using the *Test* tab in the Portal
`func logs`
- Gets logs for Functions running in a Kubernetes cluster

## Command Groups
Contains their own set of subcommands
`func azure`
- Working with Azure resources, including publishing
`func durable`
- Working with Durable Functions
`func extensions`
- For installing and managing extensions
`func kubernetes`
- For working with Kubernetes and Azure Functions
`func settings`
- Manage environment settings for the local Functions host
`func templates`
- Listing available function templates