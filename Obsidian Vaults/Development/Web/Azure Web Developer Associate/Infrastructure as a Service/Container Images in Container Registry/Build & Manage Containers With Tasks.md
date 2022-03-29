#azure #azure-wda 

# Build & Manage Containers With Tasks
*ACR Tasks* is a suite of features within *ACR*.
Provides cloud-based container image building for *Windows*, *Linux*, and *Azure Resource Manager*.
Can automate OS and framework patching for Docker containers.

## Task Scenarios
*ACR* supports several scenarios to build and maintain container images and other artefacts:
- **[[#Quick Task]]**
	- Build & push single container image to a container registry on-demand
	- Without needing local Docker Engine installation
- **[[#Automatically Triggers Tasks]]**
	- Can enable one or more triggers to build an image:
		- Source code update
		- Base image update
		- Schedule
- **[[#Multi-Step Tasks]]**
	- Extend single image build-and-push capability of *ACR Tasks*

Each *ACR Task* has associated source code context.
Location of a set of source files used to build a container image or other artefact.

## Quick Task
Provides an integrated development experience by offloading container image builds to *Azure*.
Can verify automated build definitions and catch potential problems prior to committing code.

The `az acr build` command takes a context (set of files), sends it to *ACR Tasks*, and pushes built image to registry when completed (by default).

## Automatically Triggers Tasks
### Trigger Task on Source Code Update
Upon code committed, or PR completed, to either public or private repo, a container image can be built automatically.
Can use command `az acr task create` to config a build task specifying a Git repo, and optionally a branch and/or [[Explore Elements of a Dockerfile|Dockerfile]].

### Trigger on Base Image Update
Can set up an *ACR* task to track a dependency on a base image when it builds an app image.
When an update to base image is pushed to registry, or base image is updated in a public repo, *ACR Tasks* automatically builds any app images based on it.

### Schedule a Task
Can set up one or more time triggers when you create or update the task.
Useful for running container workloads on a defined schedule.
Useful for running maintenance operations or tests on images pushed regularly to registry.

## Multi-Step Tasks
Defined in a YAML file.
Specifies individual build and push operations for container images or other artefacts.
Defines execution of one or more containers.
Each step using container as its execution environment.
E.g. can create multi-step task automating the following:
1. Build web app image
2. Run web app container
3. Build web app test image
4. Run web app test container; performs tests against running app container
5. If tests pass, build Helm Char archive package
6. Perform a `Helm upgrade` using the new chart archive package