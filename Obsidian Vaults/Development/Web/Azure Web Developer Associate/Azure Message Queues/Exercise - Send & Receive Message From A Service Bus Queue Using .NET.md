#azure #az-204 #cli #csharp 

## Prerequisites
An Azure account with active subscription.
Visual Studio Code on a supported platform.
The C# extension for VS Code.

## Start Cloud Shell
1. Log in to Azure Portal and open the Cloud Shell
2. After shell opens, select __Bash__ environment

## Create Azure Resources
1. Create some variables
```shell
myLocation=<region>
myNameSpaceName=az204svcbus$RANDOM
myRG=az204-svcbus-rg
```
2. Create resource group to hold Azure resources
```shell
az group create --name $myRG --location $myLocation
```
3. Create Service Bus messaging namespace
```shell
az servicebus namespace create --resource-group $myRG \
	--name $myNameSpaceName --location $myLocation
```
4. Create a Service Bus queue
```shell
az servicebus queue create --resource-group $myRG \
	--namespace-name $myNameSpaceName --name az204-queue
```

## Retrieve Connection String For Service Bus Namespace
1. Open portal and navigate to `az204-svcbus-rg` resource group
2. Select `az204svcbus` resource just created
3. Select `Shared access policies` in __Settings__ section
4. Select `RootManageSharedAccessKey` policy
5. Copy `primary Connection String` from dialog box

## Create Console App To Send Messages To The Queue
1. Open a local terminal and create a directory for `az204svcbus` then launch VS Code
```shell
code .
```
2. Open terminal in VS Code and run the following
```shell
dotnet new console
dotnet add package Azure.Messaging.ServiceBus
```
3. In `Program.cs` add these usings
```csharp
using System.Threading.Tasks;
using Azure.Messaging.ServiceBus;
```
4. Add the following to the `Program` class
```csharp
static string connectionString = "<Value from Step 5 previously>";
static string queueName = "az204=queue";

// Client that owns connection used to create sends & receivers
static ServiceBusClient client;

// Sender used to publish messages to the queue
static ServiceBusSender sender;

// Number of messages to be sent to the qeueue
private const int numOfMessages = 3;
```
5. Replace the `Main()` method with the following `async Task Main()` method
```csharp
// Create clients used for sending & processing messages
client = new ServiceBusClient(connectionString);
sender = client.CreateSender(queueName);

// Create a batch
using ServiceBusMessageBatch msgBatch = await sender.CreateMessageBatchAsync();

for (var i = 0; i <= numOfMessages; i++)
{
	if (!msgBatch.TryAddMessage(new ServiceBusMessage($"Message {i}")))
	{
		throw new Exception($"Exception {i} has occurred.");
	}
}

try
{
	// Use producer client to send batch of messages to queue
	await sender.SendMessagesAsync(msgBatch);
	Console.WriteLine($"A batch of {numOfMessages} messages was sent");
}
finally
{
	await sender.DisposeAsync();
	await client.DisposeAsync();
}

Console.WriteLine("Press any key to end application");
Console.ReadKey();
```
6. Run program and wait for batch sent message to appear
7. Log into portal and go to Service Bus namespace & select the queue and notice:
	- __Active__ message count is now 3
	- __Current size__ of queue increments each time a message is added
	- __Messages chart__ in the __Metrics__ section shows three incoming messages for queue

## Console Project To Receive Messages From The Queue
1. In the `Program` class add the following statics
```csharp
static string connectionString = "<Value from Step 5 previously>";
static string queueName = "az204=queue";

// Client that owns connection used to create sends & receivers
static ServiceBusClient client;

// Processor that reads and processes messages from the queue
static ServiceBusProcessor processor;
```
2. Add the following methods to `Program` to handle messages and errors
```csharp
static async Task MessageHandler(ProcessMessageEventArgs args)
{
	string body = args.Message.Body.ToString();
	Console.WriteLine($"Received: {body}");

	// Complete message to delete from queue
	await args.CompleteMessageAsync(args.Message);
}

static Task ErrorHandler(ProcessErrorEventArgs args)
{
	Console.WriteLine(args.Exception.ToString());
	return Task.CompletedTask;
}
```
3. Replace the `Main()` method with the following `async Task Main()` method
```csharp
client = new ServiceBusClient(connectionString);
processor = client.CreateProcessor(queueName, new ServiceBusProcessorOptions());

try
{
	processor.ProcessMessageAsync += MessageHandler;
	processor.ProcessErrorAsync += Errorhandler;

	// Start processing
	await processor.StartProcessingAsync();

	Console.WriteLine("Wait a while and press any key to end processing");
	Console.ReadKey();

	// Stop processing
	Console.WriteLine("\nStopping the receiver...");
	await processor.StopProcessingAsync();
	Console.WriteLine("Stopped receiving messages");
}
finally
{
	await processor.DisposeAsync();
	await client.DisposeAsync();
}
```
4. Build and run the application - you should see the received messages
5. Check portal again, and notice the __Active Message Count__ value is now 0.

## Clean Up Resources
When you no longer need these resources, use the following command to delete the resource group and related resources.
```Shell
az group delete --name az204-svcbus-rg --no-wait
```