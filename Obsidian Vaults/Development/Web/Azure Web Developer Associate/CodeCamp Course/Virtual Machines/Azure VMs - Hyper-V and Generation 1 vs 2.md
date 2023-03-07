#azure #az-204 

Hyper-V is Microsoft's hardware virtualisation product.
Lets you create and run a software version of a computer, called a *virtual machine*.
Each virtual machine acts like a complete computer, running an operating system and programs.
Hyper-V VMs are packaged into Virtual Hard Disk formats VHD or VHDX files.

There are two generations of Hyper-V VMs:
- **Generation 1**
	- Supports most guest operating systems
- **Generation 2**
	- Supports most 64-bit versions of Windows
	- Supports more current versions of Linux and FreeBSD operating systems

Azure has Generation 1 and Generation 2 VMs which are similar but **NOT** exactly the same as Hyper-V Generations.

The most important difference between Azure Gen 1 and Gen 2:
- **Generation 1**
	- ==Bios-based== architecture
- **Generation 2**
	- ==UEFI-based== boot architecture (improved boot and installation times)
	- Secure Boot verifies boot loader is signed and trusted by authority
	- Larger boot volume up to 64TB