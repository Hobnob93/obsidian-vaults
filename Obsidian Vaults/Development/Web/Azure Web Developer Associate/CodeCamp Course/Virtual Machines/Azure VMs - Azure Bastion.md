#azure #az-204 

An **intermediate harden instance** you can use to connect to your target server via SSH or RDP.
It will provision a web-based RDP client or SSH terminal.

Some devices cannot run an RDP Client, such as Google Chromebook.
Azure Bastion is one of the only ways to allow such devices to connect.

When you create an Azure Bastion, you need to add a Subnet to your VNet called `AzureBastionSubnet`, with at least a size of `/27` (32 addresses).

### RDP
If you have a Windows Server which requires RDP, and you have Bastion on the same VNet.
Select `Connect Using Azure Bastion`, enter your username and password as normal, and a new browser/tab will open connecting you to the VM.