#azure #azure-wda #shell #json 

# Mount Azure File Share in ACI
By default, *ACI*s are stateless.
If container crashes or stops, all state is lost.
To persist state, you need to mount a volume from an external store.

## Limitations
- Can only mount *Azure Files* shares to Linux
- Volume mount requires Linux container run as *root*
- Volume mounts are limited to CIFS support

## Deploy Container & Mount Volume
Specify share and volume mount point when creating the container:
```shell
az container create --resource-group <resource-group> --name <container-name>
	--image <container-image> --dns-label-name <label-name>	--ports 80
	--azure-file-volume-account-name <aci-pers-strg-acct-name>
	--azure-file-volume-account-key <strg-key>
	--azure-file-volume-share-name <aci-pers-share-name>
	--azure-file-volume-mount-path /aci/logs/
```

## Mount Multiple Volumes
Must deploy using an [[Azure Resource Manager Templates|Azure Resource Manager template]], or YAML file.
Populate the `volumes` array in `properties` section of template.
```json
"volumes": [
	{
		"name": "myvolume1",
		"azureFile": {
			"shareName": "share1",
			"storageAccountName": "mystrgacct",
			"storageAccountKey": "<strg-key>"
		}
	},
	{
		"name": "myvolume2",
		"azureFile": {
			"shareName": "share2",
			"storageAccountName": "mystrgacct",
			"storageAccountKey": "<strg-key>"
		}
	}
]
```

For each container in group you'd like to mount the volumes, populate `volumeMounts` array in `properties` section of container definition.
```json
{
	"volumeMounts": [
		{
			"name": "myvolume1",
			"mountPath": "/mnt/share1/"
		},
		{
			"name": "myvolume2",
			"mountPath": "/mnt/share2/"
		}
	]
}
```