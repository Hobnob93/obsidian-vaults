#azure #az-204 #json 

# Deploy Multi-Tiered Solutions
Using [[Explore Azure Resource Manager|Resource Manager]], you can create a template defining infrastructure and config of *Azure* solution.
Template allows you to repeatedly deploy your solution through its lifecycle.
Provides confidence resources are deployed in a consistent state.

When deploying template, *Resource Manager* (RM) converts template into REST API operations.

E.g. when *RM* receives a template with following definition:
```json
"resources": [
	{
		"type": "microsoft.Storage/storageAccounts",
		"apiVersion": "2019-04-01",
		"name": "mystorageaccount",
		"location": "westus",
		"sku": {
			"name": "Standard_LRS"
		},
		"kind": "StorageV2",
		"properties": {}
	}
]
```
It converts definition to following REST API operation, sent to `Microsoft.Storage` resource provider:
```http
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2019-04-01

REQUEST BODY
{
	"location": "westus",
	"sku": {
		"name": "Standard_LRS"
	},
	"kind": "StorageV2",
	"properties": {}
}
```
API Version is used as the API version of the REST operation.
By using same API version, you don't need to worry about breaking changes from newer versions.

Can deploy template using any of these options:
- Azure portal
- Azure CLI
- PowerShell
- REST API
- Button in GitHub repo
- Azure Cloud Shell

## Defining Multi-Tiered Templates
How you define templates and resource groups is up to you.
E.g. can deploy a three tier app through a single template to a single resource group:
![[Three Tier App Resource Group Diagram.png]]

Don't have to define entire infrastructure in single template.
Often makes sense to divide deployment requirements into a set of targeted, purpose-specific templates.
Can easily reuse templates for different solutions.
Create a master template linking all required templates to deploy a particular solution.
![[Three Tier App Deployment Diagram.png]]

Can deploy tiers into separate resource groups if you need separate lifecycles.
Resources can still be linked to other resources in other resource groups.

*RM* analyses dependencies to ensure resources created in correct order.
If one resource relies on value from another; you set a dependency.

Can use template for updates to the infrastructure.
E.g. can add resource to solution and add config rules for resources already deployed.
If template specifies creating a resource that already exists, *RM* performs update instead.
*RM* updates existing asset to same state as it would be if created new.

*RM* provides extensions for scenarios involving multiple operations.
E.g. installing software not in setup.
If using config management service, like *DSC*, *Chef*, or *Puppet*; can continue working with that service using ==extensions==.

Template becomes part of source code for the app.
Can check it in to source control and update as app evolves.
Template can be edited through any IDE.

## Share Templates
Can share a template within an organisation.
Can store template as resource type using [template specs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-specs).
Use role-based control to manage access to template spec.
Users with read access to template spec can deploy it, but not change the template.

Can safely share templates meeting organisation's standards.