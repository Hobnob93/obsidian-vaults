#azure #azure-wda 

# Explore Azure Resource Manager
*Resource Manager* receives requests from any *Azure* tools, APIs, or SDKs.
Request is authenticated and authorised.
*Resource Manager* then sends request to *Azure* service, which takes the requested action.
Consistent results and capabilities through all different tools.

![[Role of Resource Manager.png]]

## Why Choose Azure Resource Manager Templates?
Consider the following advantages of using templates:
- **Declarative syntax**
	- Can create and deploy entire *Azure* infrastructure declaratively
	- E.g. can deploy network, storage, and resources along with VMs
- **Repeatable results**
	- Repeatedly deploy throughout dev lifecycle
	- Have confidence resources are deployed in consistent manner
	- Templates are idempotent; can deploy same template many times and get same resource types in same state
	- Can develop one template representing desired state, rather than developing lots of templates to represent updates
- **Orchestration**
	- No need to worry about complexities of ordering operations
	- *Resource Manager* orchestrates deployment of interdependent resources so they're created in the correct order
	- All resources deployed in parallel where possible
	- You deploy template through one command, rather than multiple imperative commands

## Template File
Within template, you can write template expressions extending capabilities of JSON.
Expressions make use of the [functions](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-functions) provided by *Resource Manager*.

Template has the following sections:
- [Parameters](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/parameters) 
	- Provides values during deployment allowing same template to be used with different environments
- [Variables](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/variables) 
	- Values reused within templates
	- Can be constructed from parameter values
- [User-defined functions](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/user-defined-functions)
	- Create customised functions that simplify your template
- [Resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/resource-declaration)
	- Specify resources to deploy
- [Outputs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/outputs)
	- Return values from deployed resources