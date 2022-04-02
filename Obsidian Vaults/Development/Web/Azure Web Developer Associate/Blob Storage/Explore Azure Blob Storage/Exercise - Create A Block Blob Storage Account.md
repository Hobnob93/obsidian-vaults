#azure #az-204 #exercise #shell 

# Exercise - Create A Block Blob Storage Account
Lets you create block blobs with premium performance.
Optimised for workloads with high transaction rates or require fast access time.

## Prerequisites
An Azure Account with an active subscription.

## Create Account in Azure Portal
To create a block blob storage account in *Azure Portal*:
1. Select `All Services` => `Storage` category => `Storage Accounts`
2. Under ==Storage Accounts== select `Create`
3. In ==Subscription== field, select subscription in which to create account
4. In ==Resource Group==, select `Create new` and enter name for resource group
5. In ==Storage account name== field, enter name for account following these guidelines:
	- Name must be unique across *Azure*
	- Name must be between 3 and 24 chars
	- Nam can only include numbers and lowercase letters
6. In ==Location== field, select location for storage account or use default
7. For the final settings, configure the following:
	- `Performance`: Premium
	- `Permium Account Type`: Block Blobs
	- `Replication`: [[Azure Storage Redundancy Options#Redundancy in the Primary Region|LRS]]
8. Click `Review + create` to review storage account settings
9. Select `Create`

## Create Account by Using Azure Cloud Shell
1. Login to *Azure Portal* and open *Cloud Shell*
2. Create new Resource Group with command:
```shell
az group create --name <resource-group-name> --location <my-loc>
```
3. Create block blob storage account with following command:
```shell
az storage account create --resource-group <resource-group-name> --name 
	<storage-acct-name> --location <my-loc> --kind BlockBlobStorage 
	--sku Premium_LRS
```

## Clean Up Resources
Run the following command to delete the resource group and associated resources
```shell
az group delete --name <resource-group-name> --no-wait
```