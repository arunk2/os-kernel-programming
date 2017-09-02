OS - Micro kernel, Monolithic kernel, Modular kernel
====================================================

We all know that kernel is the core part of any OS. It is the set of code running in priviledged mode (kernel mode or Ring3 security level). Operating Systems can be classified based on the architechture of their kernel as

1. Monolithic kernel OS
2. Micro kernel OS
3. Modular kernel OS

### Monolithic kernel OS:
This is the old style of building kernel, where the whole OF kernel is a single large processes running entirely in a single address space. Every parts of a kernel like the Scheduler, File System, Memory Management, Networking Stacks, Device Drivers, etc., are loaded into memory at the time of OS booting and services are exposed through systemcalls.

**Example:** Unix, MS-DOS

### Micro kernel OS:
Leaving important parts like IPC(Inter process Communication), basic scheduler, basic memory handling, basic I/O primitives as microkernel, Rest of kernel is split into separate processes, known as servers and each of them run in their own space. Some run in kernel space and some run in user-space also. They co-ordinate through message passing.

**Example:** MINIX, Windows NT

### Hybrid/Modular kernel OS:
This is more like getting best of both micro and monolithic styles. Instead of loading the entire kernel into memory, kernel modules are loaded dynamically to memory on demand. Here, the kernel is compiled as multiple modules ready for loading and detaching from memory.

**Example:** Linux
