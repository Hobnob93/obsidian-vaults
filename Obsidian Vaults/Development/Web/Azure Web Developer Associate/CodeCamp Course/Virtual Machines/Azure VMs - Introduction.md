#azure #az-204 

Azure Virtual Machines (VMs) are a highly configurable server.
Virtualisation lets you run a server *without* having to buy and maintain hardware.
VMs *do* still require maintenance at a *software level*, though:
- Applying OS system patches
- Installing and configuring packages

The size of the VM is determined by the *Image*.
- Image defines combination of vCPUs, Memory, and Storage Capacity
Current limit on a per subscription basis is 20 VMs per region.
Azure VMs are billed at an hourly rate.
Single instance VMs have an availability of 99.9% (when all storage disks are *premium*).
Two instances deployed in an Availability Set will give 99.95% availability.
Can attach multiple Managed Disk to your Azure VMs.

## Virtual Machine Components
Many networking components make up a VM.
All these components will be placed in a resource group when the VM is *launched*.
The components are:
- **Network Security Group (NSG)**
	- Attached to the NIC
	- Virtual firewall with rules around ports and protocols
- **Network Interface (NIC)**
	- Device that can handle IP protocols and network communication
- **Virtual Machine Instance**
	- The actual running server
- **Public IP Address**
	- The address used to publicly access a VM
- **Virtual Network (VNet)**
	- The network where your VM will reside