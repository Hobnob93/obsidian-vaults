#azure #az-204 #ci #deployment

# Deploy to App Service
Every deployment has unique requirements, making implementing an efficient pipeline difficult.
*App Service* supports ==automated== and ==manual== deployment.

## Automated Deployment
Also known as ==Continuous Integration==.
A process used to push new code changes in a fast and repetitive pattern with minimal impact on end users.

The following source options available:
- `Azure Devops`
	- Can push code to DevOps, build the code in the cloud, run tests, generate release, and finally push code to *Azure Web App*
- `GitHub`
	- Can connect GitHub repository to Azure for automated deployment
	- Any changes to a production branch will be automatically deployed
- `BitBucket`
	- Can connect BitBucket repository to Azure for automated deployment
	- Any changes to a production branch will be automatically deployed

## Manual Deployment
There are a few options to push code to Azure:
- `Git`
	- *App Service* web apps have a *Git* URL that you can add as remote repository
	- Pushing to remote repo will deploy the app
- `CLI`
	- `webapp up` is a feature of the `az` cmd that packages app and deploys it
	- Can create a new web app for you if you haven't already created one
- `Zip deploy`
	- Use `curl` or similar HTTP utility to send a ZIP of app files
- `FTP/S`
	- FTP or FTPS a traditional way of pushing code to many hosting environments

## Use Deployment Slots
Available when using a `Standard` app tier or better.
Allows for swapping of staging & production slots when deploying changes.
Makes updates seamless for the end users as it warms up necessary workers to match required scale, eliminating downtime.

[[Explore Azure App Service Deployment Slots]]