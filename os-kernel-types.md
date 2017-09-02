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

---------------------------------------------------------------

## Different OS - based on Purpose
Most of us know about existence of various OS (Operating Systems) like Linux, Windows 7/8, Mac OS. Apart from the fact that they are coming from different vendors, they are different and are built for different purposes. Lets  try to analyze it in this post. We can  be broadly categorize the OS as below:

## Single User and Single Task OS:
OS like MS-DOS allow single user to interact and run a single task @ given time. Mainly these Operating system are for Personal Computers (PC) and Handheld devices. The very old IBM mainframe machines (system/360) and its operating systems - OS/360, BOS/360, TOS/360 fall in this category.

## Single User and Multitasking OS:
Modern desktop/laptop OS like Windows xp/vista/7/8, Mac OS, Linux desktop distributions allows execution of more than one task concurrently. This is usually done by dividing the processor among different tasks. This division/split of time is also called time sharing. The processor switches rapidly between processes giving an illusion that they all run in parallel (in terms of milliseconds).

## Multi-user OS:
Server class OS like Linux, UNIX, and Windows Server distributions work in a network environment allow data and applications from single machine to be accessed by multiple users at the same time.

## Multiprocessing OS:
Most of the modern CPUs produced for consumer market from year 2000 have two or more processors/cores or at-least SMT(Simultaneous Multi-Threading) implementation at hardware level. Also, many server class application like web servers allow parallel processing i.e. it has many independent parts, which can run independently. Many Compiler are built to take advantage parallel processing @ hardware level, which can exploit the parallelism in a sequential code after various analysis/optimizations.
Each processor works on different parts of the same task, or, on two or more different tasks. Again modern OS Linux, UNIX and Windows 7/8 are examples of multiprocessing OS.

## Real Time OS:
Some time we need applications to respond to an event within a predetermined time. For such processes regular OS may not work properly. We need operating systems to control processes. Processing is done within a time constraint. We need such OS & apps in places like medical imaging system, industrial control systems etc.

## Embedded OS:
Some time we need processing specific to a device. For example: devices like microwaves, washing machines, traffic control systems have OS specific to those devices.
