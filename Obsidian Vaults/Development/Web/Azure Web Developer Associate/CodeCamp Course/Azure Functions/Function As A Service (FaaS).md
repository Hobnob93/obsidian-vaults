Allows devs to focus on writing pieces of code (functions).
Event-driven integration trigger based on event data or to emit event data.
Generally multiple functions orchestrated together to create a serverless app.
- Sometimes also known as **microservices**
Functions generally only run when needed.

FaaS is *not* serverless on its own.
FaaS is only serverless if its fully-managed and scales to zero.

Might have a container runtime configured for a given language within a virtual machine.
The functions sit within these containers.
See diagram below.

![[Function As A Service Diagram.png]]