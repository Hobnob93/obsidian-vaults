#azure #az-204 #json 

Local Settings File stores app settings and settings used by local development tools.
This file is called `local.settings.json`.
Should be at the root of the project folder.

`IsEncrypted`
- When true, all values are encrypted with a local machine key
`Values`
- Collection of app settings used when a project is running
`Host`
- Customise the Function's host process when you run projects locally
`ConnectionStrings`
- Used only by frameworks that typically get connection strings from `ConnectionStrings`

## Example Local Settings File
```json
{
	"IsEncrypted": false,
	"Values": {
		"FUNCTIONS_WORKER_RUNTIME": "<language worker>",
		"AzureWebJobsStorage": "<conn str>",
		"MyBindingConnection": "<binding conn str>",
		"AzureWebJobs.HttpExample.Disabled": "true"
	},
	"Host": {
		"LocalHttpPort": 7071,
		"CORS": "*",
		"CORSCredentials": false
	},
	"ConnectionStrings": {
		"SQLConnectionString": "<sqlclient conn str>"
	}
}
```