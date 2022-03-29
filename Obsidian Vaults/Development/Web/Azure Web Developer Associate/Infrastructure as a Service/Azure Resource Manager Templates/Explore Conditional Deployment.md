#azure #azure-wda #json 

# Explore Conditional Deployment
Allows you to optionally deploy a resource in a template.
Use the `condition` element to specify whether resource is deployed.
Value for condition resolves to `true` or `false`.
Value can only be applied to the whole resource.

## New or Existing Resource
Can use conditionals to use an existing resource or create a new one.
Example below shows how to use condition to deploy new storage account or use an existing one.
Contains parameter `newOrExisting` which is used as condition in `resources` section.
```json
{
	"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
	"contentVersion": "1.0.0.0",
	"parameters": {
		"storageAccountName": {
			"type": "string"
		},
		"location": {
			"type": "string",
			"defaultValue": "[resourceGroup().location]"
		},
		"newOrExisting": {
			"type": "string",
			"defaultValue": "new",
			"allowedValues": [
				"new",
				"existing"
			]
		}
	},
	"functions": [],
	"resources": [
		{
			"condition": "[equals(parameters('newOrExisting'), 'new')]",
			"type": "Microsoft.Storage/storageAccounts",
			"apiVersion": "2019-06-01",
			"name": "[parameters('storageAccountName')]",
			"location": "[parameters('location')]",
			"sku": {
				"name": "Standard_LRS",
				"tier": "Standard"
			},
			"kind": "StorageV2",
			"properties": {
				"accessTier": "Hot"
			}
		}
	]
}
```

## Runtime Functions
If you use a `reference` or `list` function with a resource that is conditionally deployed, function is evaluated even if resource isn't deployed.
You get an error if function refers to a resource that doesn't exist.

Use `if` function to make sure function only evaluated for conditions when resource is deployed.

You set resource as dependent on conditional resource exactly as you would any other resource.
When conditional resource isn't deployed, *RM* automatically removes it from required dependencies.