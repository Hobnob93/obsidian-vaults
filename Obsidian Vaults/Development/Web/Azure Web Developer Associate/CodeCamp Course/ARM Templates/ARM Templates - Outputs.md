#azure #az-204 #json #cli 

Outputs return values from deployed resources, so you can use them programmatically.

You can specify the type and value under outputs:
```json
{
	"outputs": {
		"resourceId": {
			"type": "string",
			"value": "[resourceId('Microsoft.Network/publicIpAddresses', parameters('publicIPAddresses_name'))]"
		}
	}
}
```

You can use the Azure API via CLI, PowerShell or SDK to fetch outputs:
```shell
az deployment group show \
	-g <resource-group-name> \
	-n <deployment-name> \
	--query properties.outputs.resourceId.value
```