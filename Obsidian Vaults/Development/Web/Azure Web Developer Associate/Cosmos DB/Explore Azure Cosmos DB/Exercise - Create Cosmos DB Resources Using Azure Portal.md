#azure #az-204 #exercise #json 

# Exercise - Create Cosmos DB Resources Using Azure Portal
## Prerequisites
An *Azure* account with an active subscription.

## Create an Azure Cosmos DB Account
1. Log into *Azure Portal*
2. In navigation pane, select `+ Create a resource`
3. Search for **Azure Cosmos DB** and select `Create/Azure Cosmos DB`
4. On ==Select API== page, select `Create` under **Core (SQL) - Recommended**
5. In ==Create Azure Cosmos DB Account - Core (SQL)== page, enter basic settings:
	- `Suscription`: the subscription you want to use
	- `Resource Group`: select `Create new` then enter a name
	- `Account Name`: enter a *unique* name to identify account - name can only contain lowercase, numbers, and hyphen character between 3 and 31 chars
	- `Location`: use one that is closest
	- `Capacity mode`: select `Serverless`
6. Select `Review + create`
7. Review the settings and click `create`
8. Once done, select `Go to resource` to go to account page

## Add A Database & A Container
Can use Data Explorer in Portal to create a database and container
1. Select `Data Explorer` from nav pane, and select `New Container`
2. In ==Add container== page, enter settings for new container:
	- `Database ID`: select `Create new` and enter one
	- `Container ID`: enter one
	- `Partition key`: such as `/category`
3. Select `OK` when done

## Add Data To Database
1. In ==Data Explorer==, expand the `Database ID` and the `Container` within and select `New Item`
2. Add following structure to item on right side of ==Items== pane:
```json
{
	"id": "1",
	"category": "personal",
	"name": "groceries",
	"description": "Pick up apples and strawberries",
	"isComplete": false
}
```
3. Select `Save`
4. Keep doing this until you have all the data you want, making sure to use a *unique* ID each time

## Clean Up Resources
1. Select `Overview` on nav pane within ==Azure Cosmos DB Account== page
2. Select resource group you want to remove
3. Select `Delete` and follow directions