#azure #az-204 

Package, deploy, and manage cloud applications using containers.
"Fully Managed Docker as a Service".

**Azure Container Instances** allow you to launch containers without need to worry about configuring or managing the underlying virtual machine.
Azure Container Instances are designed for isolate containers:
- Simple applications
- Task automation
- Build jobs

Containers can be provisioned *within seconds* where VMs can take several minutes.
Containers are billed *per second* where VMs are per hour (potential to save money).
Containers have *granular* custom sizing of vCPUs, memory, and GPUs where VMs are predetermined.

ACI can deploy both Windows and Linux containers.
Can *persist* storage with **Azure Files** for your ACI containers.
ACIs are accessed via a fully qualified domain name (FQDN) e.g. `customlabel.azureregion.azurecontainer.io`.

Azure provides *Quick-start images* to start launching example applications, but you can also source containers from:
- Azure Container Registry
- Docker Hub
- Privately hosted container registry