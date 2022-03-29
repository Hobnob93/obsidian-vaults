#azure #azure-wda #exercise #shell 

# Exercise - Deploy Container Instance Using Azure CLI
## Prerequisites
An *Azure* account with an active subscription

## Log In to Azure & Create Resource Group
1. Log in to *Azure Portal*
2. Select *Cloud Shell*
3. Choose the `Bash` environment
4. Create new resource group with following command
```shell
az group create --name <resource-group> --location <my-loc>
```

## Create A Container
Provide a name, a Docker image, and resource group.
Expose container to Internet by specifying DNS name label.
1. Create a DNS name to expose container - must be unique
```shell
DNS_NAME_LABEL=aci-example-$random
```
2. Start a container instance
```shell
az container create --resource-group <resource-group> --name <container-name>
	--image mcr.microsoft.com/azuredocs/aci-helloworld
	--ports 80 --dns-name-label $DNS_NAME_LABEL
	--location <my-loc>
```

## Verify Container is Running
When container creation completes, check its status.
```shell
az container show --resource-group <resource-group> --name <container-name>
	--query "{FROM:ipAddress.fqdn,ProvisioningState:provisioningState}"
	--out table
```
You should see table containing container's FQDN.

## Clean Up Resources
Remove the resource group to clean up all resources used.
```shell
az group delete --name <resource-group> --no-wait
```