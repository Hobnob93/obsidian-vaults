#azure #az-204 

Can launch either Windows or Linux services on Azure VMs.

### Windows
- Need a Windows license (or your Windows account)
- Can bring your own license via *Hybrid License*
- Set a username and password, primarily used for RDP access
- Have to use much larger instances to run Windows due to the higher memory usage
	- At least a B2, which is more expensive than a B1
- It's a full desktop environment

### Linux
- Most versions require no type of license, unless it's for extra support
- Can set either a username and password OR create an SSH key-pair
- Can utilise smaller VM sizes as you're not running a full desktop experience
- Unix and Linux based systems are traditionally terminal-based environments