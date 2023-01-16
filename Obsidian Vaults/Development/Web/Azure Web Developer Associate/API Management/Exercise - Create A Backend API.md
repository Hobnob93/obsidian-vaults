#azure #az-204 #exercise #cli 

## Prerequisites
An Azure account with active subscription

## Start Cloud Shell
1. Log in to Azure Portal and open the Cloud Shell
2. After shell opens, select __Bash__ environment

## Create An API management Instance
1. Set some variables for use with later commands
```shell
myApiName=az204-apim-$RANDOM
myLocation=<region>
myEmail=<email>
myRG=az204-apim-rg
```
2. Create a resource group
```shell
az group create --name $myRG --location $myLocation
```
3. Create an APIM instance using the `apim create` command. The `--sku-name Consumption` option is used to speed up process for the walkthrough
```shell
az apim create -n $myApiName --location $myLocation \
	--publisher-email $myEmail --resource-group $myRG \
	--publisher-name AZ204-APIM-Exercise \
	--sku-name Consumption
```

## Import A Backend API
1. In Azure Portal, search for and select `API Management services`
2. On `API Management` screen, select API Management instance created above
3. Select `APIs` in the navigation pane
4. Select `OpenAPI` from the list and select `Full` in the pop-up
5. Use the values from the table below to fill out the form
| Setting               | Value                                               |
| --------------------- | --------------------------------------------------- |
| OpenAPI Specification | https://conferenceapi.azurewebsites.net?format=json |
| Display Name          | Demo Conference API                                 |
| Name                  | demo-conference-api                                 |
| Description           | Automatically populated                             |
| API URL suffix        | conference                                          |
6. Select `Create`

## Configure the Backend Settings
The API is created, but need to specify a backend
1. Select `Settings` in the blade to the right and enter `https://conferenceapi.azurewebsites.net/` in the `Web service URL` field
2. Deselect the `Subscription required` checkbox
3. Select `Save`

## Test the API
1. Select `Test`
2. Select `GetSpeakers`
	- The page shows `Query pamraeters` and `Headers`, if any.
	- The `Ocp-Apim-Subscription-Key` is filled in automatically for the subscription key associated with this API
3. Select `Send`
	- Backend responds with `200 OK` and some data

## Clean Up Resources
When you no longer need these resources, use the following command to delete the resource group and related resources.
```shell
az group delete --name az204-apim-rg --no-wait
```