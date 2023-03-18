#azure #az-204 #cli

`AzCopy` is a command-line utility for copying blobs or files to or from a storage account.
It's an executable that you need to download before you can use it.
You will also need correct level of authorisation:
- To download
	- Storage Blob Data Reader
- To upload
	- Storage Blob Data Contributor
	- Storage Blob Data Owner
You can gain access via either:
- Azure Active Directory (AD)
- Shared Access Signatures (SAS)

Use the `copy` command to either upload:
```shell
azcopy copy \
	'<path-to-file>' \
	'https://enterprise.blob.core.windows.net/<container>/<file>'
```
or download:
```shell
azcopy copy \
	'https://enterprise.blob.core.windows.net/<container>/<file>' \
	'<path-to-location>'
```