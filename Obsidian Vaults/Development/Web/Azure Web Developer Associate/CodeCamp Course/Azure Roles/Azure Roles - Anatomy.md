#azure #az-204 #json 

You're able to fetch an Azure Role using PowerShell or the CLI.
Azure Role document syntax of the property names will change whether it's Azure PowerShell or Azure CLI.

The properties returned are as follows:
- `Name` (or `RoleName` in CLI)
	- The display name of the role
- `Id`
	- A generated ID for the role
- `IsCustom`
	- Indicates whether the role is custom created
- `Description`
	- The description of the role
- `Actions`
	- An array of strings
	- Specifies management operations that the role allows to be performed
- `NotActions`
	- An array of strings
	- Specifies operations the role *does not* allow to be performed
- `DataActions`
	- Array of strings
	- Specifies operations role is allowed to perform to your data
- `NotDataActions`
	- Array of strings
	- Specifies operations role *is not* allowed to perform
- `AssignableScopes`
	- Array of strings
	- Specifies scopes the role is available for assignment
	- You an only define one management group in the scopes of a custom role

Example as JSON:
```json
{
	"Name": "Virtual Machine Operator",
	"Id": "<guid>",
	"IsCustom": true,
	"Description": "Can monitor and restart VMs",
	"Actions": [
		"Microsoft.Storage/*/read",
		"Microsoft.Network/*/read",
		"Microsoft.Compute/*/read",
		"Microsoft.Compute/virtualMachines/start/action",
		"Microsoft.Compute/virtualMachines/restart/action",
		"Microsoft.Authorization/*/read",
		"Microsoft.ResourceHealth/availabilityStatuses/read",
		"Microsoft.Resources/subscriptions/resourceGroups/read",
		"Microsoft.Insights/alertRules/*",
		"Microsoft.Insights/diagnosticSettings/*",
		"Microsoft.Support/*"
	],
	"NotActions": [],
	"DataActions": [],
	"NotDataActions": [],
	"AssignableScopes": [
		"/subscriptions/{subscriptionId1}",
		"/subscriptions/{subscriptionId2}",
		"/providers/Microsoft.Management/managementGroups/{groupId1}"
	]
}
```