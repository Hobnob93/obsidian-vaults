#azure #az-204 #json 

Template variables are used to simplify ARM templates.
You transform parameters and resource properties using functions, then store the results in variables.
```json
{
	"variables": {
		"storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
	}
}
```

To call a variable, use the `variable` function.
```json
{
	"resources": [
		{
			"type": "Microsoft.Storage/storageAccounts",
			"name": "[variables('storageName')]"
		}
	]
}
```

You can use nested JSON to have nested variables to essentially create objects and scope.
Scoping/Nesting variables based on environment:
```json
{
	"variables": {
		"environmentSettings": {
			"test": {
				"instanceSize": "Small",
				"instanceCount": 1
			},
			"prod": {
				"instanceSize": "Large",
				"instanceCount": 4
			}
		}
	}
}
```
Use parameters to then choose the environment:
```json
{
	"parameters": {
		"environmentName": {
			"type": "string",
			"allowedValues": [
				"test",
				"prod"
			]
		}
	}
}
```
Referencing nested variables:
```json
{
	"envInstanceSize": "[variables('environmentSettings')[parameters('environmentName')].instanceSize]"
}
```