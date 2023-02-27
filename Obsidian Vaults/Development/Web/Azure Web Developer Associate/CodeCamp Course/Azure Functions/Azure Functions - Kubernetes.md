#azure #az-204 #cli

Kubernetes Event-driven Autoscaling (**KEDA**) allows you to setup autoscaling based on events from various cloud-native and third-party services

You can deploy any Azure function app to a Kubernetes cluster running KEDA.
```cli
func kubernetes deploy \
	--name <name-of-function-deployment> |
	--registry <container-registry-username
```

Kubernetes-based Functions provides the Functions runtime in a Docker container with event-driven scaling through KEDA.
KEDA can scale to 0 instances, and out to *n* instances.
It does this by exposing custom metrics for the Kubernetes autoscaler (*Horizontal Pod Autoscaler*).
Using Functions containers with KEDA makes it possible to replicate serverless function capabilities in any Kubernetes cluster.
These functions can also be deployed using Azure Kubernetes Services (AKS) virtual nodes feature for serverless infrastructure.