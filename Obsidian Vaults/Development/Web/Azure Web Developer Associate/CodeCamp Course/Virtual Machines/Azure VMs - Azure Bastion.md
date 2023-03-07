#azure #az-204 

An **intermediate harden instance** you can use to connect to your target server via SSH or RDP.
It will provision a web-based RDP client or SSH terminal.

Some devices cannot run an RDP Client, such as Google Chromebook.
Azure Bastion is one of the only ways to allow such devices to connect.

When you create an Azure Bastion, you need to add a Subnet to your VNet called `AzureBastionSubnet`, with at least a size of `/27` (32 addresses).

### RDP
If you have a Windows Server which requires RDP, and you have Bastion on the same VNet.
When connecting using Bastion, enter your username and password as normal, and a new browser/tab will open connecting you to the VM with a GUI.

### SSH
If you have a Linux server you can SSH with Bastion.
Can use the SSH Private Key or Username and Password used when creating the VM.
With SSH, using the private key is recommended.
When connecting using Bastion, check "SSH Private Key from Local File" and use the stored private key (usually a `.pem` file).
Once connected, a new browser/tab will open connecting you to the VM via a shell window where you can give commands.