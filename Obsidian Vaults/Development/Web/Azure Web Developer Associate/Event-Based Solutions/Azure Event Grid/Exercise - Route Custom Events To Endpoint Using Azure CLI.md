#azure #az-204 #exercise #cli #json 

## Prerequisites
An Azure account with active subscription

## Start Cloud Shell
1. Log in to Azure Portal and open the Cloud Shell
2. After shell opens, select __Bash__ environment

## Create Resource Group
1. Set some variables for use in later commands
```shell
let rNum=$RANDOM*$RANDOM
myLocation=<region>
myTopicName="az204-egtopic-${rNum}"
mySiteName="az204-egsite-${rNum}"
mySiteUrl="https://${mySiteName}.azurewebsites.net"
myRG="az204-evgrid-rg"
```
2. Create a resource group for new resources
```shell
az group create --name $myRG --location $myLocation
```

## Enable An Event Grid Resource Provider
Register Event Grid resource provider using `provider register` command
```shell
az provider register --namespace Microsoft.EventGrid
```
It can take a few minutes to complete.
Can check status using command:
```shell
az provider show --namespace Microsoft.EventGrid --query "registrationState"
```

## Create A Custom Topic
Use the `eventgrid topic create` command.
Name must be unique as it is part of the DNS entry.
```shell
az eventgrid topic create --name $myTopicName \
	--location $myLocation \
	--resource-group $myRG
```

## Create A Message Endpoint
Need to create endpoint for event message before subscribing to custom topic.
Endpoint typically takes actions based on the event data.
Script below uses a pre-built web app that displays the event messages.
Deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.
It also generates a unique name for the site.

1. Create message endpoint - deployment may take a few minutes
```shell
az deployment group create --resource-group $myRG \
	--template-uri "https://raw.githubusercontent.com/Azure-Samples/azure-event-grid-viewer/main/azuredeploy.json" \
	--parameters siteName=$mySiteName hostingPlanName=viewerHost

echo "Your web app URL: ${mySiteUrl}"
```
2. In a new tab, navigate to site URL to ensure web app is running.

## Subscribe To A Custom Topic
Subscribe to an event grid topic to tell EG which events you want to track and where to send those events.
1. Use the `eventgrid event-subscription create` command:
```shell
endpoint="${mySuteUrl}/api/updates"
subId=$(az account show --subscription "" | jq -r '.id')

az eventgrid event-subscription create \
	--name az204ViewerSub --endpoint $endpoint
	--source-resource-id "/subscriptions/$subId/resourceGroups/az204-evgrid-rg/providers/Microsoft.EventGrid/topics/$myTopicName"
```
2. Navigate to web app again and notice subscription validation event has been sent to it.
	- Select eye icon to expand event data
	- EG sends validation event so the endpoint can verify that it wants to receive event data
	- The web app includes code to validate the subscription

## Send An Event To Your Custom Topic
Trigger an event to see how Event Grid distributes the message to your endpoint.
1. Retrieve URL and key for custom topic
```shell
topicEndpoint=$(az eventgrid topic show --name $myTopicName -g $myRG --query "endpoint" --output tsv)

key=$(az eventgrid topic key list --name $myTopicName -g $myRG --query "key1" --output tsv)
```
2. Create event data to send - typically an app or Azure service would send the data
```shell
event='[ {"id": "'"$RANDOM"'", "eventType": "recordInserted", "subject": "myapp/vehicles/motorcycles", "eventTime": "'`date +%Y-%m-%dT%H:%M:%S%z`'", "data":{ "make": "Contoso", "model": "Monster"},"dataVersion": "1.0"} ]'
```
3. Use `curl` to send the event to the topic
```shell
curl -X POST -H "aeg-sas-key: $key" -d "$event" $topicEndpoint
```
4. View the web app to see event that was just sent.
	- Select eye icon to expand event data
	- Event Grid sends validation event so endpoint can verify it wants to receive event data
	- Web app includes code to validate subscription

## Clean Up Resources
When you no longer need these resources, use the following command to delete the resource group and related resources.
```Shell
az group delete --name az204-evgrid-rg --no-wait
```