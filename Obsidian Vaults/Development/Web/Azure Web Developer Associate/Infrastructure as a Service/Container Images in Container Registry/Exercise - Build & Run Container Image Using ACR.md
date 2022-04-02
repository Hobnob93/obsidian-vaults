#azure #az-204 #exercise #shell

# Exercise - Build & Run Container Image Using ACR
## Prerequisites
An *Azure* account with an active subscription.

## Log In to Azure & Start Cloud Shell
1. Log in to *Azure Portal*
2. Open *Cloud Shell*
3. Select the `Bash` environment

## Create Azure Container Registry
1. Create a resource group for the registry
```shell
az group --name <resource-group> --location <my-loc>
```
2. Create basic container registry - name must be unique within *Azure*
```shell
az acr create --resource-group <resource-group> --name <container-name> --sku Basic
```

## Build & Publish Image From Dockerfile
1. Navigate to desired local directory and use command below for sample Dockerfile
```shell
echo FROM mcr.microsoft.com/hello-world > Dockerfile
```
2. Build the image and push it to registry when built
```shell
az acr build --image sample/hello-world:v1 --registry <container-name>
	--file Dockerfile .
```

## Verify Results
1. List repositories in registry
```shell
az acr repository list --name <container-name> --output table
```
2. List the tags on sample/hello-world repository
```shell
az acr repository show-tags --name <container-name>
	--repository sample/hello-world --output table
```

## Run Image in ACR
Run sample/hello-world:v1 container image from container registry
```shell
az acr run --registry <container-name> 
	--cmd '$Registry/sample/hello-world:v1' /dev/null
```

## Clean Up Resources
Remove the resource group created as part of this exercise to clean up all resources.
```shell
az group delete --name <resource-group> --no-wait
```