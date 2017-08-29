
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


## For more details: ##
http://en.wikipedia.org/wiki/Virtualization
