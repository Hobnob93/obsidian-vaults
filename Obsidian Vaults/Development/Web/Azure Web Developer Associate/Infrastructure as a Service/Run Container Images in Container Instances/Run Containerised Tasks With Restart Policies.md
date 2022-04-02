#azure #az-204 #shell 

# Run Containerised Tasks With Restart Policies
Ease and speed of deploying containers in *ACI* makes run-once tasks feasible.
Tasks such as build, test, or image rendering in a container instance.

Configurable restart policy can set if containers are stopped once processes are completed.
Container instances are billed by the second, you're charged for only compute resources used, while container executes your task.

## Container Restart Policy
When container group created, you can specify one of three restart policies:
- **Always**
	- Containers in group always restarted
	- This is the ==default==
- **Never**
	- Containers in group never restarted
	- Containers run once at most
- **OnFailure**
	- Containers only restarted when the process within container fails
	- Containers are run at least once

## Specify Restart Policy
You can use the following command to set the restart policy on a container:
```shell
az container create --resource-group <resource-group> --name <container-name>
	--image <container-image> --restart-policy <policy>
```

## Run To Completion
*ACI* starts container and stops when app, or script, exits.#
When *ACI* stops a container set to `Never` or `OnFailure`, the status of instance is set to ==Terminated==.