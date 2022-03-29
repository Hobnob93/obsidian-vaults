#azure #azure-wda #shell 

# Set Correct Deployment Mode#
Can set if deployment is either ==incremental== update or ==complete== update.
This determines how *RM* handles existing resources in resource group that ==aren't== in the template.
The `default` is ==incremental==.

For either mode, *RM* tries to create all resources specified in template.
If resource exists, and settings for it not changed, then no operation taken.
If resource properties have changed, that resource is updated with new values.

## Complete Mode
*RM* **deletes** resources in resource group not defined in template.

If template includes resource not deployed due to [[Explore Conditional Deployment|condition]] being false, result depends on which API version you use to deploy.
If version is earlier than 2019-05-10; resource **is not** deleted.
If later version; resource **is** deleted.

Caution when using this mode with `copy loops`.
Any resources not specified in template after resolving copy loop are deleted.

## Incremental Mode
*RM* leaves **unchanged** resources that exist in resource group but not in template.

When redeploying an existing resource in incremental, outcome is slightly different.
Specify all properties for resource, not just the ones being updated.
A common misunderstanding is thinking unspecified properties are left unchanged.
If you **don't** specify certain properties, *RM* interprets the update as overwriting those values.

## Set Deployment Mode
**PowerShell**
```shell
New-AzResourceGroupDeployment 
	-Mode Complete 
	-Name ExampleDeployment 
	-ResourceGroupName ExampleResourceGroup 
	-TemplateFile c:\MyTemplates\storage.json
```

**Azure CLI**
```shell
az deployment group create
	--mode Complete
	--name ExampleDeployment
	--resource-group ExampleResourceGroup
	--template-file storage.json
```