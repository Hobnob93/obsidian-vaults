#azure #az-204 #exercise #cli #json 

## Prerequisites
An Azure account with active subscription

## Start Cloud Shell
1. Log in to Azure Portal and open the Cloud Shell
2. After shell opens, select __Bash__ environment

## Create a Key Vault
1. Set some variables for the CLI commands to reduce retyping
	- Key Vault name needs to be globally unique, can use `$RANDOM` for a random string
```Shell
myKeyVault=az204vault-$RANDOM
myLocation=<region>
myResourceGroup=az204-vault-rg
```
2. Create a resource group
```Shell
az group create --name $myResourceGroup --location $myLocation
```
3. Create a Vault Key using the `az keyvault create` command
```Shell
az keyvault create --name $myKeyVault --resource-group $myResourceGroup --location myLocation
```

## Add and Retrieve a Secret
1. Create a secret
	- Add a password that could be used by an app
	- Password will be called `ExamplePassword` and will store `S0m3P455w0rd!`
```Shell
az keyvault secret set --vault-name $myKeyVault --name "ExamplePassword" --vaule "S0m3P455w0rd!"
```
2. Use the `show` command to retrieve the secret
```Shell
az keyvault secret show --name "ExamplePassword" --vault-name $myKeyVault
```
This command will produce the following JSON:
```json
"value": "S0m3P455w0rd"
```

## Clean Up Resources
When you no longer need these resources, use the following command to delete the resource group and associated Key Vault
```Shell
az group delete --name az204-vault-rg --no-wait
```