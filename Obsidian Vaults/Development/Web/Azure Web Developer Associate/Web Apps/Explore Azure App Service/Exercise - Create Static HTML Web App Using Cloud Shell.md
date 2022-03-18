#azure #azure-wda #exercise #shell #json

# Create Static HTML Web App Using Cloud Shell
You will need an *Azure* account with an active subscription in order to fulfil this exercise.

## Log In to Azure & Download Sample App
1. Login to [Azure Portal](https://portal.azure.com/) and open *Cloud Shell*
2. When shell opens, select *Bash* environment
3. Using the shell, create a directory and navigate to it
	```shell
	mkdir htmlapp
	
	cd htmlapp
	```
4. Run `git clone` to clone the sample app into directory just created
	```shell
	git clone https://github.com/Azure-Samples/html-docs-hello-world.git
	```

## Create the Web App
1. Need to run `az webapp up`, which may take a few minutes
	```shell
	cd html-docs-hello-world

	az webapp up --location <myLocation> --name <myAppName> --html
	```
	
	Once done you will receive the following info (abbreviated) - make note of the `resourceGroup` value required for [[#Clean Up Resources]]
	```json
	{
		"app_url": "https://<myAppName>.azurewebsites.net",
		"location": "westeurope",
		"name": "<app_name>",
		"os": "Windows",
		"resourceGroup": "<resource_group_name>",
		"serverfarm": "appsvc_asp_Windows_westeurope",
		"sku": "FREE",
		"src_path": "/home/<username>/demoHTML/html-docs-hello-world"
	}
	```
2. Navigate to `http://<myAppName>.azurewebsites.net` to verify the app is running

## Update & Redeploy App
1. After making changes to the app's code, you can redeploy using the `az webapp up` command - ensure same values as before for `<myLocation>` and `<myAppName>`
	```shell
	az webapp up --location <myLocation> --name <myAppname> --html
	```
2. Once completed, navigate to the `azurewebsites` address as before to confirm changes are present

## Clean Up Resources
You can delete the resource group using `az group delete` command:
```shell
az group delete --name <resource_group> --no-wait
```