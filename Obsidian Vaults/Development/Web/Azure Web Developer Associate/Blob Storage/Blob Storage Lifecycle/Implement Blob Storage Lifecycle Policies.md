#azure #az-204 #json #shell 

# Implement Blob Storage Lifecycle Policies
You can add, edit, or remove a policy through any of these methods:
- Azure Portal
- Azure PowerShell
- Azure CLI
- REST APIs

## Azure Portal
Two ways; List View and Code View

### Azure Portal List View
1. Sign in to Azure Portal
2. Select `All resources` and select your storage account
3. Under ==Data Management== select `Lifecycle management` to view or change rules
4. Select ==List view== tab
5. Select `Add rule` and fill out ==Action set== form fields
6. Select `Filter set` to add optional filter
7. Select `Browse` to specify container and folder by which to filter
8. Select `Review + add` to review policy settings
9. Select `Add` to add the new policy

### Azure Portal Code View
1. Follow the first few steps in the [[#Azure Portal List View|List view]]
2. Select ==Code view== tab
3. Json below is example of policy that moves a block blob with name prefix "log" to cool tier if been more than 30 days since modified
```json
{
	"rules": [
		{
			"enabled": true,
			"name": "move-to-cool",
			"type": "Lifecycle",
			"definition": {
				"actions": {
					"baseBlob": {
						"tierToCool": {
							"daysAfterModificationGreaterThan": 30
						}
					}
				},
				"filters": {
					"blobTypes": [
						"blockBlob"
					],
					"prefixMatch": [
						"sample-container/log"
					]
				}
			}
		}
	]	
}
```
4. Select `Save`

## Azure CLI
To add lifecycle management policy with Azure CLI, write policy to JSON file, then call command below.
A lifecycle policy must be read or written in full - partial updates are not supported.
```shell
az storage account management-policy create --account-name <storage-acct-name> 
	--policy @<policy-json> --resource-group <resource-group>
```