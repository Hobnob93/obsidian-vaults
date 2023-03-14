#azure #az-204 

Container Groups are a collection of containers that get scheduled on the same host machine.
The containers in a container group share:
- Lifecycle
- Resource
- Local network
- Storage volumes

![[ACI - Container Groups Diagram.png]]

Container Groups are similar to a *Kubernetes pod*.
Multi-container groups **currently only support Linux** containers.

There are two ways to deploy a multi-container group:
- [[CodeCamp - ARM Templates|Resource Manager Template]]
	- When you need to deploy additional Azure service resources
- YAML File
	- When your deployment includes only container instances