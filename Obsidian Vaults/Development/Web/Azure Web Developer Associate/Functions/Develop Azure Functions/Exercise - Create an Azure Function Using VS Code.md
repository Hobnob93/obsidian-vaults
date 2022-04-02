#azure #az-204 #exercise 

# Exercise - Create an Azure Function Using VS Code
## Prerequisites
1. An azure account or active subscription ([Free](https://azure.com/free))
2. [Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local#install-the-azure-functions-core-tools) version 3.x
3. [Visual Studio Code](https://code.visualstudio.com/) on a supported platform
4. [.NET Core 3.1](https://dotnet.microsoft.com/download/dotnet/3.1) for the steps below
5. The [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) for VS Code
6. The [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) for VS Code

## Create Local Project
1. Choose *Azure* icon in activity bar, then in ==Azure: Functions== area choose `Create new project...`
2. Choose directory from project workspace and choose `Select`
3. Provide the following for prompts:
	- `Language`: C#
	- `.NET Runtime`: .NET Core 3.1
	- `Template for Function`: HTTP Trigger
	- `Function name`: HttpExample
	- `Namespace`: My.Functions
	- `Auth Level`: Anonymous - enables anyone to call endpoint
	- `How to open`: Add to workspace
4. VS Code will generate *Azure Functions* project with an HTTP Trigger

## Run Function Locally
VS Code integrates with *Azure Functions Core Tools* to let you run and test locally.
1. Press `F5` to start up project
	- Output from *Core Tools* is displayed in ==Terminal==
	- App starts in the ==Terminal==
	- Here you can see the ==URL endpoint== of the HTTP-triggered function
2. Go to ==Azure: Functions== area and right click `HttpExample` and choose `Execute Function Now...`
3. In ==Enter request body== type a message like `{ "name": "Azure" }`
	- Press enter to send it
	- Notification should be raised in VS Code when received by function
	- Info about function execution should show in ==Terminal==
4. Press `Ctrl + C` to stop *Core Tools* and disconnect debugger

## Sign In to Azure for Publishing
You *must* be signed in to *Azure* in order to publish:
1. Choose *Azure* icon in activity bar, go to ==Azure: Functions== area, choose `Sign in to Azure...`
2. When prompted, choose *Azure account* and sign in with credentials
3. Once signed in, close browser window and you should see login details in side bar

## Publish Project to Azure
1. Choose *Azure* icon in activity bar, then ==Azure: Functions== area, choose `Deploy to Function App...`
2. Provide following pieces of info:
	- `Function App in Azure`: Create new Function App (don't choose advanced option)
	- `Globally Unique Name for Function App`: Needs to be a valid URL path - is validated to ensure is unique
	- `Runtime stack`: Same choice as when making the function
	- `Location for new resources`: Choose region near you for optimal performance
	- `Subscription`: Choose subscription to use (not shown if you only have the one)
3. The following *Azure* resources are created in subscription
	- Resource group; a logical container for related resources
	- Standard Azure Storage account; maintains state and info about projects
	- Consumption plan; defines underlying cost of serverless function app
	- A function app; the environment for executing function code
	- Application Insights instance; tracks usage of serverless function

## Run the Azure Function
1. In ==Azure: Functions== area, expand your subscription, right click `HttpExample` and choose `Execute Function Now...`
2. Enter request body as you did before and press enter
3. Notification should be raised in VS Code once *Azure* returns a response

## Clean Up Resources
Use following steps to delete function app and related resources to avoid any further costs:
1. In VS Code, press `F1` to open command palette & search for `Functions: Open in portal`
2. Choose app from list and press Enter
3. In ==Overview== tab, select named link next to ==Resource Group==
4. In ==Resource Group== page, review list of included resources and verify what is to be deleted
5. Select `Delete resource group` and follow instructions