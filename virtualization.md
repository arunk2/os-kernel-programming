
Virtualization Technology
=========================
Virtualization is the means by which we create a virtual counterpart of an actual item, by software or hardware & software. 
The virtualized item could be another hardware, operating system (OS), storage device or network.

As defined above we have,

* **Hardware virtualization** for virtualizing hardware.
* **Desktop virtualization** for desktop, where in we use simple or cheap computers that are primarily designed to connect to the network for virtualizing the desktop. Typically many corporates use this ensure quick and easy infrastructure.
* **Software virtualization** like:
    * Operating System (OS) virtualization - where we host multiple OS on a different OS as an application running on it.
    * Application virtualization - where we ensure the availabilty of an individual applications in an environment separated from the underlying OS.
* **Memory virtualization** - like virtual memory, where multiple applications works such that it has contiguous working memory. But in actual it works on a single physical memory, which is shared.
* **Storage virtualization** - like Virtual File System, Virtual disk drive ensuring the abstraction of actual data storage.
* **Network virtualization** - like Virtual Private Network (VPN), which is a network protocol that replaces the actual wire or other physical media in a network with an abstract layer, allowing a private network to be created over the Internet.

---------------------------------------------

Hardware Virtualization
=========================
Hardware Virtualization is the technology of creation of a virtual machine that acts like a real computer. 
In short - it virtualizes hardware components on entirely different hardware. 
Software executed on these virtual machines is separated from the underlying hardware resources. 
For example, a computer that is running Microsoft Windows may host a virtual machine that looks like a computer with the Ubuntu Linux operating system.

In hardware virtualization we have
* **Host machine** - actual machine on which the virtualization takes place
* **Guest machine** - the virtual machine.

Hardware virtualization can be:
* **Full virtualization:** where a complete hardware is simulated.
* **Partial virtualization:** Some but not all of the target environment is simulated.
* **Para virtualization:** Here nothing is simulated. Guest programs need to be specifically modified to run in this environment. We can also call this as hardware-assisted virtualization. 
This technology is mainly introduced for efficiency of hardware virtualization. **Example:** Intel VT and AMD-V technologies

---------------------------------

Security Threats - Virtualization technology
============================================

In virtualization technology, we need a core component `hypervisor' for virtualization of various environment (guest OS) on host. Hypervisor or virtual machine monitor (VMM) is a software / fi rmware / hardware that creates and runs virtual machines. A computer on which a hypervisor is running one or more virtual machines is defined as a host machine and each virtual machine is called a guest machine. The hypervisor presents the guest operating systems with a virtual operating platform and manages the execution of the guest operating systems. Most of the hackers try to exploit the security hole in hypervisor. 

### Following are the popular security threats:
**Hyperjacking** - This involves subverting the existing hypervisor or inserting a rogue hypervisor. Since hypervisors run at the most privileged ring level on a processor, this would be hard or even impossible for any operating system running on the hypervisor to detect.

**VM Escape** - Virtual machine escape is an exploit in which the attacker runs code on a VM that allows an operating system running within it to break out and interact directly with the hypervisor. Such an exploit could give the attacker access to the host operating system and all other virtual machines (VMs) running on that host.

**VM Hopping** - Similar to VM Escape, VM Hopping allows an attacker to move from one virtual server to compromise other virtual servers on the same physical hardware.

**VM Theft** - This is the ability to steal a virtual machine le electronically, which can then be mounted and run elsewhere.

-------------------------------------------

Complexity of Hypervisors
=========================
In virtualization technology, we need a core component **'hypervisor'** for virtualization of various environment (guest OS) on host. 

Hypervisor or virtual machine monitor (VMM) is a software / rmware / hardware that creates and runs virtual machines. A computer on which a hypervisor is running one or more virtual machines is called as a host machine and each virtual machine is called a guest machine. 
The hypervisor presents the guest operating systems with a virtual operating platform and manages the execution of the guest operating systems. These hypervisors are complex units, which needs lot of support from current technology.

### For Xen Hypervisor and KVM Hypervisor - minimum System Requirements:
- Hardware virtualization support required (Intel-VT or AMD-V enabled)
- 64-bit x86 CPU
- 2 GB of memory
- 6 GB of local disk
- At least 1 NIC

### For VMware's Hypervisor (ESXi/ESX) - minimum System Requirements:
- Hardware virtualization support required (Intel-VT or AMD-V enabled)
- CPU: single socket, dual core
- Memory: 4GB
- Network: one network adapter, plus one for management interface
- Storage (SATA/SAS): one 80GB drive

## For more details: ##
- http://en.wikipedia.org/wiki/Virtualization
- http://www.esecurityplanet.com/network-security/virtualization-poses-security-risks-in-public-cloud.html
