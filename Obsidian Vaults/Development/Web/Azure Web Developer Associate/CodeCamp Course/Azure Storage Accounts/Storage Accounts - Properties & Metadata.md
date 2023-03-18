#azure #az-204 #cli #json 

You can use the Azure CLI to retrieve properties and metadata for storage containers.

##### Getting Container Properties
Use the command `az storage container show` to fetch container properties:
```shell
az storage container show --account-name $storageAccountName \
	--name $containerName --account-key $accountKey
```
That command will return the following data:
```json
{
	"metadata": {},
	"name": "<container-name>",
	"properties": {
		"contentLength": 0,
		"etag": "\"0x8D9E1027FA92D9F\"",
		"hasImmutabilityPolicy": false,
		"hasLegalHold": false,
		"lastModified": "2022-01-26T19:31:49+00:00",
		"lease": {
			"duration": null,
			"state": "available",
			"status": "unlocked"
		},
		"publicAccess": null
	}
}
```

##### Update Container Metadata
The update command overwrites the existing container metadata.
Use the `az storage container metadata update` command to update metadata:
```shell
az storage container metadata update --account-name $accountName \
	--name $containerName --metadata creationType=AzureCli \
	--auth-mode key --account-key $accountKey
```
You will get a response like:
```json
{
	"etag": "\"0x8D9E1042167E273\"",
	"lastModified": "2022-01-26T19:43:30+00:00"
}
```

##### Show Container Metadata
Use the `az storage container metadata show` to retrieve metadata.
```shell
az storage container metadata show --account-name $accountName \
	--name $containerName --auth-mode key --account-key $accountKey
```
This will return the following metadata:
```json
{
	"creationType": "AzureCli"
}
```

##### Setting Blob Metadata
The updater command overwrites existing blob metadata.
Use the `az storage blob metadata update` command to update the metadata:
```shell
az storage blob metadata update --name "TestImage1.png" \
	--account-name $accountName --container-name $containerName \
	--metadata creationType=AzureCli --auth-mode key \
	--account-key $accountKey
```
This returns the following result:
```json
{
	"etag": "\"0x8D9E10A56B4AA4C\"",
	"lastModified": "2022-01-26T20:27:57+00:00"
}
```

##### Show Blob Metadata
use the `az storage blob metadata show` command to show a blob's metadata:
```shell
az storage blob metadata show --name "TestImage1.png" \
	--account-name $accountName --container-name $containerName \
	--auth-mode key --account-key $accountKey
```
This will return the following metadata:
```json
{
	"creationType": "AzureCli"
}
```