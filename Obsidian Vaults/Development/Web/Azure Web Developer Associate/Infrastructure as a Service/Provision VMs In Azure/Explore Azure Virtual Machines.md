#azure #azure-wda 

# Explore Azure Virtual Machines
A VM gives the flexibility of virtualisation without having to buy and maintain physical hardware that it runs.
You till need to maintain the VM by performing tasks, such as:
- Configuring
- Patching
- Installing software that runs on it

*Azure* VMs can be used in various ways, such as:
- **Development and test**
	- They offer a quick and easy way to create a computer with specific config required to program and test an app
- **Applications in the cloud**
	- Demand for an app can fluctuate
	- Might make economic sense to run app on VM
	- You pay for extra VMs when you need them
	- The extra VMs are cleaned up when aren't needed
- **Extended data centre**
	- VMs in an *Azure* virtual network can easily be connected to organisation's network

## Design Considerations for Virtual Machine Creation
There are a multitude of design considerations when you build out an application infrastructure in *Azure*:
- **Availability**
	- *Azure* support s a single instance VM Service Level Agreement of 99.9%
	- Provided you deploy VM with premium storage for all disks
- **VM size**
	- Size of VM determined by workload