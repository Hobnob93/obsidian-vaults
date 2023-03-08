#azure #az-204 #json 

An Azure resource you want to provision, such as a VM or database.
The following properties exist within the JSON:
- `type`
	- The type of the resource
	- Follows the format `{ResourceProvider}/ResourceType`
- `apiVersion`
	- Version of REST API to use for the resource
	- Each resource provider publishes its own API versions
- `name`
	- Name of the resource
- `location`
	- Region where the resource will be deployed
	- Most resources have a location property
- "Other Properties"
	- Can use to configure the specific resource type
	- Will be different depending on the resource type used

```json
{
	...
	"resources": [
		{
			"type": "Microsoft.Storage/storageAccounts",
			"apiVersion": "2019-04-01",
			"name": "{unique-name}",
			"location": "eastus",
			"sku": {
				"name": "Standard_LRS"
			},
			"kind": "StorageV2",
			"properties": {
				"supportsHttpsTrafficOnly": true
			}
		}
	]
	...
}
```