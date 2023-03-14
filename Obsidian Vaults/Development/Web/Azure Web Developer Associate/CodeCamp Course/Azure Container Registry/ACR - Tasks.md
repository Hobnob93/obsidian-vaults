#azure #az-204 

ACR tasks allow you to automate OS and framework patching for your Docker containers.

For quick tasks you can push a single container image to a container registry on-demand, in Azure, without needing a local Docker Engine installation.
You're also able to create multi-step tasks.

You can trigger automated builds by:
- Source code updates
- Updates to a container's base image
- Timers on a schedule

Each ACR task has an associated source code context.
- The location of a set of source files used to build a container image or other artefact

Tasks can take advantage of run variables
- Reuse task definitions and standardise tags for images and artefact