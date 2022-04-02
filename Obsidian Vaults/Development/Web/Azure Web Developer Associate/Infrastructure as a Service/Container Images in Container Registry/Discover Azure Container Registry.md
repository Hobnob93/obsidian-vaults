#azure #az-204 

# Discover Azure Container Registry
The *Azure Container Registry* (ACR) service builds container images in *Azure*.
Can be used with existing container development and deployment pipelines.
Can also be used with *Azure Container Registry Tasks*.
They can be built on demand, or as automated builds.

## Use Cases
Pull images from *Azure* container registry to various deployment targets:
- **Scalable orchestration systems**
	- Manage containerised applications across clusters of hosts
	- Includes Kubernetes, DC/OS. and Docker Swarm
- **Azure services**
	- Supports building and running apps at scale
	- Including *Azure Kubernetes Service* (AKS), *App Service*, *Batch*, *Service Fabric*, and others

Devs can push container registry as part of container development workflow.
E.g. container registry from CI and delivery tool such as *Azure Pipelines* or *Jenkins*.

Configure *ACR Tasks* to automatically rebuild app images when base images are updated.
Or automate image builds when changes committed to a repo.
Create multi-step tasks to automate building, testing, and patching multiple container images in parallel in the cloud.

## Azure Container Registry Service Tiers
Available in multiple service tiers.
They provide predictable pricing and options for aligning to capacity and usage patterns of private Docker registry.

- **Basic**
	- Cost-optimised for devs learning about *ACR*
	- Same programmatic capabilities as **Standard** and **Premium** (such as auth)
	- Included storage and image throughput are appropriate for lower usage scenarios
- **Standard**
	- Increased storage and image throughput
	- Should satisfy needs of most production scenarios
- **Premium**
	- Highest amount of storage, concurrent operations, and throughput
	- Allows for high-volume scenarios
	- Geo-replication for managing single registry across multiple regions
	- Content trust for image tag signing
	- Private link with private endpoints to restrict access to registry

## Supported Images & Artefacts
Each image is a read-only snapshot of a Docker-compatible container.
*ACR* can include both Windows and Linux images.
*ACR* stores content formats such as *Helm Charts* and *Open Container Initiative* (OCI).

## Automated Image Builds
Use *ACR Tasks* to streamline building, testing, pushing, and deploying images in *Azure*.
Configure build tasks to automate container OS and framework patching pipeline.
Build images automatically when team makes changes to source control.