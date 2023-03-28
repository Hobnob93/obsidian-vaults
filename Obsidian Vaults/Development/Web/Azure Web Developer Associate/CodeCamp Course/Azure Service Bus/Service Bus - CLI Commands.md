#azure #az-204 #cli 

Azure CLI has a few commands for Azure Service Bus.
- `az servicebus georecovery-alias`
- `az servicebus migration`
- `az servicebus namespace`
- `az servicebus queue`
- `az servicebus topic`

Service Bus does not have CLI commands to send messages to a queue or topic.
- Azure Queue Storage does
- To send messages you need to use the SDK

#### Create Service Bus Namespace
```shell
az servicebus namespace create \
	--resource-group ContosoRG \
	--name ContosoBusNS \
	--location eastus
```

#### Create Service Bus Queue
```shell
az servicebus queue create \
	--resource-group ContosoRG \
	--namespace-name ContosoBusNS \
	--name ContosoOrdersQueue
```

#### Create Authorisation Rule
```shell
az servicebus namespace authorization-rule keys list \
	--resource-group ContosoRG \
	--namespace-name ContosoBusNS \
	--name RootManageSharedAccessKey \
	--query primaryConnectionString \
	--output tsv
```