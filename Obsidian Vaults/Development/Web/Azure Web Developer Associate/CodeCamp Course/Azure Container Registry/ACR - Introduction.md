#azure #az-204 

Create and maintain *Azure Container registries* to store and manage private Docker container images, and related artefacts.

ACR is a managed, private Docker registry service based on the open-source Docker Registry 2.0.

User ACRs with existing container development and deployment pipelines, use [[ACR - Tasks|ACR Tasks]] to build container images in Azure.

Pull images from an Azure container registry to various deployment targets:
- Kubernetes
- DC/OS
- Docker Swarm

Many Azure services have direct support to use ACR:
- Azure Kubernetes Service (AKS)
- Azure App Service
- Azure Batch
- Azure Service Fabric
- and more!

Developers can push to a container registry as part of a container deployment workflow with delivery tools such as:
- Azure Pipelines
- Jenkins

Many ways to work with ACR via Azure CLI:
- Azure PowerShell
- Azure Portal
- Azure SDK
- Docker Extension for VS Code