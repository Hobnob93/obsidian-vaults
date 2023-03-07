#azure #az-204 

Update Management allows you to manage and install OS updates and patches for both Windows and Linux VMs.
Can do this for VMs deployed to Azure, on-premises, or in other cloud providers.

When you launch an Azure VM, you can go to *Operations* and turn on *Guest + Host Updates*.
This installs the **Microsoft Monitoring Agent (MMA)** that will be used to monitor the instances.
**Azure Automations** is the underlying service that is installed on the agent.

Update Management will perform a scan for update compliance.
- Every 12 hours on a Windows VM by default
- Every 3 hours on a Linux VM by default
Can take between 30 minutes and 6 hours for dashboard to display updated data from managed computers.

#### Azure Automations
Contains features that can be enabled for servers, such as:
- Update Management
- Change Tracking and Inventory
- Start/Stop VMs during off-hours
These features have a dependency on a **Log Analytics** workspace, and therefore require linking the workspace with an Automation account.