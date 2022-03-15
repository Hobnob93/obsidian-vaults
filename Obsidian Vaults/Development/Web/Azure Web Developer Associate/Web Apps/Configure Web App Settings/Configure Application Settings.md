#azure #azure-wda 

# Configure Application Settings
App settings are environment variables passed to the app.
For Linux and custom containers, *App Service* passes settings using the `--env` flag.
They can be accessed in app's management page and going to ==Application Settings==.

For ==ASP.NET== and ==ASP.NET Core== are the same as settings you'll find in `Web.config` or `appsettings.json` - the *App Service* settings simply overwrite the values contained in these files.
Production secrets are much safer if kept in *App Service* app settings.

App settings are always encrypted when stored (`encrypted-at-rest`).

## Adding and Editing Settings
Use the `New application setting` button to create new settings.
If using [[Explore Azure App Service Deployment Slots|deployment slots]], can specify if setting is swappable or not.
Can edit a setting using the `Edit` button on the right.
Don't forget to click `Update` when done, and to `Save` the changes on the ==Configuration== page.

## Editing Application Settings in Bulk
You can use the `Advanced` button to do this.
App settings have the following formatting:
```json
[
	{
		"name": "<key-1>",
		"value": "<value-1>",
		"slotSetting": false
	},
	{
		"name": "<key-2>",
		"value": "<value-2>",
		"slotSetting": true
	}
	...
]
```

## Configure Connection Strings
For non-ASP.NET stacks, better to use the app settings instead as connection strings require special formatting.
Connection strings are **always** encrypted when stored.

Adding or editing connection strings follow same principles as other app settings.
They can be tied to [[Explore Azure App Service Deployment Slots|deployment slots]].
An example of connection strings in JSON formatting for bulk adding or editing:
```json
[
	{
		"name": "name-1",
		"value": "conn-string-1",
		"type": "SQLServer",
		"slotSetting": false
	},
	{
		"name": "name-2",
		"value": "conn-string-2",
		"type": "PostgreSQL",
		"slotSetting": true
	}
]
```