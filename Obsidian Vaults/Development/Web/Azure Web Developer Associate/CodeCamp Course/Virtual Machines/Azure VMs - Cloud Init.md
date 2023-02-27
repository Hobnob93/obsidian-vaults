#azure #az-204 

**Cloud-init** is the industry standard multi-distribution method for cross-platform cloud instance initialisation.
Supported across all major public cloud providers, provisioning systems for private cloud infrastructure, and bare-metal installations.

**What is Cloud Instance Initialisation?**
The process of preparing an instance with config data for operating system and runtime environment.
Cloud instances are initialised from a disk image and instance data:
- Meta-data
- User-data
- Vendor-data

**User Data** is a script that you want to run when an instance first boots up e.g. install Apache web-server.

Azure VMs support Cloud-init across most Linux Distros that support it.

![[Azure VMs - Cloud Init Diagram.png]]