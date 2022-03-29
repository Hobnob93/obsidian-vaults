#azure #azure-wda #exercise #json #shell 

# Exercise - Create & Deploy Azure Resource Manager Templates
## Prerequisites
- An *Azure* account with active subscription
- VSCode or another IDE with *Azure Resource Manager Tools* installed
- *Azure CLI* installed locally

## Create an Azure Resource Manager Template
1. Create and open file named `azuredeploy.json`
2. If using VSCode, can use `arm!` autocomplete snippet for the following json:
```json
{
	"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
	"contentVersion": "1.0.0.0",
	"paramters": {},
	"functions": [],
	"variables": {},
	"resources": [],
	"outputs": {}
}
```

## Add Azure Resource to Template
Change the `resources` array to look like this:
```json
"resources": [
	{
		"name": "storageaccount1",
		"type": "Microsoft.Storage/storageAccounts",
		"apiVersion": "2019-06-01",
		"tags": {
			"displayName": "storageaccount1"
		},
		"location": "[resourceGroup().location]",
		"kind": "StorageV2",
		"sku": {
			"name": "Premium_LRS",
			"tier": "Premium"
		}
	}
]
```

## Add Parameters to Template
Use a parameter to specify storage account name.

The `parameters` block should be changed to this:
```json
"paramters": {
	"storageAccountName": {
		"type": "string",
		"metadata": {
			"description": "Storage Account Name"
		},
		"minLength": 3,
		"maxLength": 24
	}
}
```

Change the `resources::name` property from [[#Add Azure Resource to Template|above]] to be:
```json
"name": "[parameters('storageAccountName')]",
```

## Create a Parameter File
Allows you to store environment-specific values and pass these values in as a group at deployment time.
1. Create and open file `azuredeploy.parameters.json` file
2. Ensure file looks as follows:
```json
{
	"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
	"contentVersion": "1.0.0.0",
	"paramters": {
		"storageAccountName": {
			"value": "az204storageacctarm"
		}
	}
}
```

## Deploy Template
1. Connect to *Azure* by using the `az login` command
2. Create resource group to contain new resource:
```shell
az group create --name resource-group --location my-loc
```
3. Deploy the template using the following command - progress will be shown in the terminal
```shell
az deployment group create --resource-group resource-group
	--template-file azuredeploy.json --parameters azuredeploy.parameters.json
```
4. Verify deployment using the command:
```shell
az storage account show --resource-group resource-group --name storage-acct
```

## Clean Up Resources
Clean up all *Azure* resources using the following command:
```shell
az group delete --name resource-group --no-wait
```