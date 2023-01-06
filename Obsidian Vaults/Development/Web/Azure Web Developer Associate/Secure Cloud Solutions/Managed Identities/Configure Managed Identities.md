#azure #az-204 #cli 

## System-Assigned Managed Identity Role Requirements
To create, or enable, a VM with system-assigned identity, your account needs the ==Virtual Machine Contributor== role assignment.
No additional Azure AD directory role assignments are required.

## Enable System-Assigned Identity During Creation of an Azure Virtual Machine
The following creates a VM with a system-assigned identity (`--assign-identity`) with a specified role and scope.
You'll also need the admin user name and password account for VM sign-in.
```Shell
az vm create --resource-group myResourceGroup \
	--name myVM --image win2016datacenter \
	--generate-ssh-keys \
	--assign-identity \
	--role contributor \
	--scope mySubscription \
	--admin-username azureuser \
	--admin-password P455w0rd!
```

## Enable System-Assigned Identity on Existing Azure Virtual Machine
Use the `identity assign` command to assign identity to existing VM:
```Shell
az vm identity assign -g myResourceGroup -n myVM
```

## Create A User-Assigned Identity
Need to use the `identity create` command, specifying resource group where identity will be created, and the name of the identity:
```Shell
az identity create -g myResourceGroup -n myUserAssignedIdentity
```

## Assign a User-Assigned Identity During Creation of an Azure Virtual Machine
Create a VM associated with new user-assigned identity by doing the following:
```Shell
az vm create --resource-group myResourceGroup \
	--name myVM --image UbuntuLTS \
	--assign-identity myUserAssignedIdentity \
	--role <ROLE> \
	--scope mySubscription \
	--admin-username azureuser \
	--admin-password P455w0rd!
```

## Assign A User-Assigned Identity to Existing Azure Virtual Machine
Need to use the `identity assign` command to do this:
```Shell
az vm identity assign -g myResourceGroup -n myVM \
	--identities myUserAssignedIdentity
```
