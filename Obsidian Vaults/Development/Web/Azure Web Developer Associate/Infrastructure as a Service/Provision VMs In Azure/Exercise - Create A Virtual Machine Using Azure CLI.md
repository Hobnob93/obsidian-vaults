#azure #azure-wda #exercise #shell #cli

# Exercise - Create A Virtual Machine Using Azure CLI
## Prerequisites
An *Azure* account with an active subscription.

## Log In To Azure & Start Cloud Shell
1. Log in to *Azure Portal* and open Cloud Shell
2. Once shell opens, select the ==Bash== environment.

## Create Resource Group & Virtual Machine
1. Create resource group
```shell
az group create --location <my-loc> --name <resource-group>
```
2. Create a VM using the below command
```shell
az vm create --resource-group <resource-group> --name <vm-name> --image UbuntuLTS
	--generate-ssh-keys --admin-username azureuser
```

## Install Web Server
1. By default, only SSH connections are opened when creating Linux VM. Use command below to open the TCP port 80 for use with NGINX web server
```shell
az vm open-port --port 80 --resource-group <resource-group> --name <vm-name>
```
2. Connect to VM using SSH like the example below
```shell
ssh azureuser@<publicIPAddress>
```
3. Install the NGINX web server to see the server in action - update package sources and install latest
```shell
sudo apt-get -y update
sude apt-get -y install nginx
```
4. When done, type `exit` to leave the SSH session

## View Web Server In Action
Use a web browser to view the default NGINX welcome page.
Use public IP address of VM as the web address.

## Clean Up Azure Resources
Can safely delete resource group using command below:
```shell
az group delete --name <resource-group> --no-wait
```