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
	- Determined by expected workload
	- Determines factors such as processing power, memory, and storage capacity
- **VM limits**
	- Subscription has default quota limits
	- Can impact deployment of many VMs for your project
	- Current limit on a per subscription basis is 20 VMs per region
- **VM image**
	- Can either use your own image, or can use one of the images in *Azure Marketplace*
	- Can get a list of images in marketplace by using `az vm ikmage list` command
- **VM disks**
	- Two components that make up this area
	- The types of disks; determines performance level
	- The storage account type; contains the disks
	- *Azure* provides two types of disks:
		1. **Standard disks**: backed by HDDs & delivers cost-effective storage while being performant. Ideal for cost effective and test workload
		2. **Premium disks**: backed by SSD, high-performance, low-latency disks. Perfect for VMs running production workload
	- There are two options for disk storage:
		1. **Managed disks**: newer and recommended. Specify disk size (up to 4TB), and *Azure* will create and manage disk and storage. No limits to worry about
		2. **Unmanaged disks**: You're responsible for storage accounts holding virtual hard disks (VHDs). You pay for amount of space you use. A single account has a fixed rate limit of 20,000 I/O operations per second. You need to scale out with more disks; need more storage accounts to do this. Gets complicated.

## Virtual Machine Extensions
Windows VMs have extensions which give VM additional capabilities through post deployment config and automated tasks.
Common tasks can be accomplished using extensions:
 - **Run custom scripts**: Custom Script Extension helps you configure workloads on VM by running script when VM is provisioned
 - **Deploy and manage configs**: the PowerShell Desired State (DSC) Extension helps you set up DSC on a VM to manage configs and environments
 - **Collect diagnostics data**: Azure Diagnostics Extension helps configure VM to collect diagnostics data used to monitor health of application

For Linux VMs, *Azure* supports [cloud-init](https://cloud-init.io/) across most Linux distributions.
Works with all major automation tooling like *Ansible*, *Chef*, *SaltStack*, and *Puppet*.