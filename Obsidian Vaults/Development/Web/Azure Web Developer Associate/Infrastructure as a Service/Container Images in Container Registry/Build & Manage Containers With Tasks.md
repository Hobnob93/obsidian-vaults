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
- **Automatically triggered tasks**
	- Can enable one or more triggers to build an image:
		- Source code update
		- Base image update
		- Schedule
- **Multi-step task**
	- Extend single image build-and-push capability of *ACR Tasks*

Each *ACR Task* has associated source code context.
Location of a set of source files used to build a container image or other artefact.

## Quick Task
Provides an integrated development experience by offloading container image builds to *Azure*.
Can verify automated build definitions and catch potential problems prior to committing code.

The `az acr build` command takes a context (set of files), sends it to *ACR Tasks*, and pushes built image to registry when completed (by default).