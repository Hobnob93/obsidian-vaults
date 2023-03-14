#azure #az-204 #cli 

Azure Containers are *stateless by default*!
When container crashes or stops, all state is lost.
To persist state you need to mount an external volume.

You can mount the following external volumes:
- Azure Files (file share)
- Secret volume
- Empty directory
- Cloud git repo

To mount a file volume, you need to do this via PowerShell or CLI and specify the details to mount the drive.
```shell
az container create \
	--resource-group exampro-resource-group \
	--name my-app \
	--image exampro/web-app \
	--location eastus
	--ports 80 \
	--ip-address Public \
	--azure-file-volume-account-name $STRG_ACCNT_NAME \
	--azure-file-volume-account-key $STRG_KEY \
	--azure-file-volume-share-name my-fileshare \
	--azure-file-volume-mount-path /aci/logs/
```