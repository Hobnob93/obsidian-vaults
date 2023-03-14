#azure #az-204 #cli 

Deployment is the action of pushing changes or updates from a local environment or repository into a remote environment.

Azure App Service provides many ways to deploy your applications:
- Run from package
- Deploy ZIP or WAR (uses Kudu)
- Deploy via FTP
- Deploy via cloud sync (Dropbox or OneDrive)
- Deploy continuously (GitHub, BitBucket, and Azure Repos) uses Kudu and Azure Pipelines
- Deploy using a custom container CI/CD pipeline (Deploy for Docker Hub, or [[ACR - Introduction|Azure Container Registry]])
- Deploy from a local Git (Kudu build server)
- Deploy using GitHub Actions
- Deploy using GitHub Actions containers
- Deploy with template ([[ARM Templates - Infrastructure As Code (IaC)|ARM Templates]])

#### Run From a Package
When files in the package are *not* copied to `wwwroot` directory.
Instead, the ZIP package itself gets *mounted* directly as the **read-only** `wwwroot` directory.

All other deployment methods in App Service have deployments to the following directories:
- **Windows**
	- `D:\home\site\wwwroot`
- **Linux**
	- `/home/site/wwwroot`

Since the same directory is used by app at runtime, it's possible for deployment to fail because of file lock conflicts.
App can behave unexpectedly as a result if some of the files are not yet updated.
This is why packaging a file and running it directly can be a good option.

#### ZIP and WAR Deployment
Uses the same Kudu service that powers continuous integration-based deployments.
Kudu is the engine behind git deployments in Azure App Service.
It's an open-source project that can also be run outside of Azure.

Kudu supports the following functionality for ZIP file deployment (but can support other types of deployment):
- Deletion of files left over from a previous deployment
- Option to turn on the default build process, which includes package restore
- Deployment customisation, including running deployment scripts
- Deployment logs
- A file size limit of 2048MB (2GB)

You can deploy using:
- Azure CLI
- Azure API via REST (cURL)
- Azure Portal
```shell
# Azure CLI
az webapp deployment source config-zip --resource-group <rg-name> \
	--name <app-name> --src <zip-file-path>

#cURL
curl -X POST -u <deployment_user> --data-binary @"<zip-file-path>" \
	https://<app-name>.scm.azurewebsites.net/api/zipdeploy

#Azure PowerShell
Publish-AzWebApp -ResourceGroupName <rg-name> -Name <app-name> \
	-ArchivePath <zip-file-path>
```

#### FTP Deployment
Not a great way to deploy, as it is very old-school, but it's an option.
You can use File Transfer Protocol (FTP) to upload your files.
You will need your own FTP client.
You simply drag and drop your files into the FTP client with the correct FTPS endpoint set.
Will need FTP credentials in order to do this.

#### Cloud Sync Deployment
Can use Dropbox or OneDrive to deploy using a cloud sync.
Dropbox is a third-party storage service.
OneDrive is Microsoft's cloud storage service.

You can go to Deployment Centre and configure for Dropbox or OneDrive.
When you turn on Sync it will create a folder in your cloud drive:
- **OneDrive**
	- `Apps\Azure Web Apps`
- **Dropbox**
	- `Apps\Azure`

This will sync with your `/home/site/wwwroot` directory, so you just update the files in the cloud folder.