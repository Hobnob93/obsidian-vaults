#azure #azure-wda 

# Explore Azure Container Instances
*Azure Container Instances* (ACI) is a solution for operating isolated containers.
This includes simple apps, task automation, and build jobs.

Some of the benefits of using *ACI*:
- **Fast start up**
	- *ACI* can start containers in seconds
	- No need to provision and manage VMs
- **Container access**
	- *ACI* enables exposing container groups directly with an IP address and a fully qualified domain name (FQDN)
- **Hypervisor-level security**
	- Isolate app as completely as it would be in a VM
- **Customer data**
	- *ACI* service stores minimum customer data required to ensure container groups running as expected
- **Custom sizes**
	- *ACI* provides optimum utilisation by allowing exact specs of CPU cores and memory
- **Persistent storage**
	- Mount *Azure Files* shares directly to container to retrieve and persist state
- **Linux and Windows**
	- Schedule both platform containers using the same API

[Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/) is recommended.

## Container Groups
Top level resource in *ACI* are container groups.
It is a collection of containers that get scheduled on the same host machine.
Containers in a group share a lifecycle, resources, local network, and storage volumes.
It's a similar concept to a ==pod== in Kubernetes.

A container group with multiple containers:
![[Container Group With Multiple Containers Diagram.png]]

This example container group:
- is scheduled on a single host machine
- is assigned a DNS name label
- exposes a single IP address, with one exposed port
- consists of two containers; one on port 80, the other port 5000
- includes two *Azure* file shares as volume mounts, each container mounts one of the shares locally

## Deployment
Two common ways to deploy multi-container groups:
1. [[Azure Resource Manager Templates|Resource Manager Template]]
	- Recommended when need to deploy additional *Azure* service resources
2. A YAML file
	- Recommended when deployment includes only container instances

## Resource Allocation
*ACI* allocates CPUs, memory, and optionally GPUs to a container group.
Adds resource requests of instances in the group.
E.g. if you create a container group with 2 instances, each needing 1 CPU; then the group has 2 CPUs allocated.

## Networking
Container groups share an IP address, and a port namespace on that address.
Must expose IP address from the container to enable external clients to reach the container.
Port mapping isn't supported due to sharing port namespace.
Containers within the same group can reach each other via localhost on ports they have been exposed on, even if those ports aren't exposed externally.

## Storage
Can specify external volumes to mount within a container group.
Can map those volumes into specific paths within individual containers in a group.

Support volumes include:
- *Azure* file share
- Secret
- Empty directory
- Cloned git repo

## Common Scenarios
Multi-container groups are useful where you want to divide a single functional task into a small number of container images.
These images can be delivered by different teams and have separate resource requirements.

Example usage could include:
- Container serving web app and container pulling latest content from source control
- App container and a logging container - latter collects logs and metrics output by main app and writes them to long-term storage
- App container and a monitoring container - latter periodically makes request to app to ensure it's running and responding correctly - raises alert if not
- Front-end container and back-end container - front end might be web app, back end might be service to retrieve data