#azure #az-204 

There are 3 ways to **connect** to your VMs; SSH, RDP, and Bastion.

**Secure Shell (SSH)**
- Protocol to establish a secure connection between client and server
- How you can remotely connect to Azure VM via terminal
- SSH happens in ==Port 22 via TCP==
- RSA Key Pairs are commonly used to authorise access

**Remote Desktop Protocol (RDP)**
- A proprietary protocol developed by Microsoft
- Provides a user with a GUI to connect to another computer over a network
- How you can remotely connect to Windows Server via Visual Desktop
- RDP happens on ==Port 3389 via TCP and UDP==

**Bastion**
- Azure Bastion is a service you deploy that lets you connect to a VM using your browser or Azure Portal
- Provides secure and seamless RDP/SSH connectivity to your VM over TLS
- A bastion is a hardened instance that is monitored
- Users connect to this VM which then establishes a connection to the target instance
- Sometimes known as a jump box since you have an extra security step