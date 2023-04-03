#azure #az-204 

It's a Platform as a Service (PaaS).
Quickly deploy and manage Web apps on Azure without worrying about the underlying infrastructure.

Azure App Service is an HTTP-based service for hosting web apps, REST APIs, and mobile back ends.
You can choose your programming language and either a Windows or Linux environment.
It's the**Heroku** equivalent for Azure.

Azure App Service takes care of the following underlying structure:
- Security patches for OS and languages
- Load balancing
- Autoscaling
- Automated manager

Azure App Service makes it easy to implement common integrations and features such as:
- Azure DevOps (For deployments)
- GitHub integration
- Docker Hub integration
- Package management
- Easy to setup staging environments
- Custom domains
- Attaching TLS/SSL Certificates

You pay based on an Azure App Service plan:
- **Shared Tier**
	- Free, Standard (Linux not supported)
- **Dedicated Tier**
	- Basic, Standard, Premium, PremiumV2, PremiumV3
- **Isolated Tier**
	- Specific tier for [[Azure App Services - App Service Environment (ASE)|ASE]]

Azure App Services can also run docker [[ACI - Introduction|single or multi-containers]].