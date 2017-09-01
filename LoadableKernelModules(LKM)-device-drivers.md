Loadable Kernel Modules and Device Drivers
==========================================
In the beginning almost all OS were implemented as a single huge kernel with all device drivers included as part of the kernel. If we think further this design make sense, as almost all device drivers require the hardware/resource access and these accesses are provided by being part of the kernel code running in kernel/supervisor mode. Otherwise such hardware/resource access can't be obtained.
From implementation point of view, writing them as part of kernel will be much easier. 
Because these drivers would have complete access to the data structures and other routines in the kernel 
and hence use them easily.

### Downside to this design:
It requires a rebuild of the kernel in order to include/remove device drivers. 
This design along with some poor coding practice by kernel developers may result in highly cohesive software component. 
This can make it more difficult to maintain and debug the code.

### Solution:
To have a solution for the above problems, the Linux kernel supports loadable device drivers / kernel modules. 
i.e. Device drivers can be added to or removed from memory at runtime, with some command-line tools (and without recompiling the entire kernel). 
Such drivers are still part of the kernel, but they are compiled separately and enabled only when loaded. 
Loadable device drivers, or modules, are generally loaded into memory using commands.

Most device drivers, and a lot of other kernel functionality under Linux, are implemented as modules. 
How to load, and unload modules?

### Typical commands:
- **insmod** : to load a module into kernel
- **rmmod** : to remove a module
- **modproble** : to detect any dependent module required and load it

--------------------------------------------

## Minimal - Loadable Kernel Module (LKM)

As discussed in previous posts, we know a kernel module can be added on the fly (while OS is still running) and hence the name “Loadable kernel modules”. They are special programs and have structures entirely different from user program. They don't have main functions but must have at-least 2 functions init_XXXXXX() and cleanup_XXXXXX() - here XXXXXX represent the module name.

### Example:
    int init_modulename (void)
    {
        /*initialition code*/
    }

    void cleanup_modulename (void)
    {
        /*cleanup code*/ 
    }


These functions will match the following LKM Utilities, while they are plugged into kernel:
- **insmod:** Insert an LKM into the kernel.
- **rmmod:** Remove an LKM from the kernel.

----------------------------------------------------------

## LKM Utilities

The following list of LKM commands (utilities) and their usage, Hope this is useful for someone.

| Tool | usage |
|------|-------|
| **insmod** | Insert a LKM into the kernel |
| **rmmod** | Remove a LKM from the kernel |
| **depmod** | Lists dependencies between LKMs.
| **ksyms** | Lists symbols that are exported by the kernel for use by given LKMs.
| **lsmod** | Lists currently loaded LKMs.
| **modinfo** | Display contents of .modinfo section in an LKM object file.
| **modprobe** | Loads given module after loading/unloads modules required for the given module. For example, if you must load A before loading B, 'modprobe' will automatically load A when you tell it to load B.|


-------------------------------------

## Linux Device Drivers - as a LKM
Most of the Linux Device drivers are available as LKM. Lets think a bit on this and justify the choice of it being LKM. We all know device drivers are set of API sub-routines interface to hardware. It mainly abstracts the implementation of hardware-specific details from a user program. Another important aspect is that every Device is a special file in all Unix like systems i.e. Typically a user/user-program can access the device via file name in /dev , e.g. /dev/dv1.
We have more than 70% of Linux kernel code specific to device drivers for thousands of devices. Only very few of these devices are needed at any point of time in running instance. We all know memory is costly and having all of them at once and having drivers of devices, which are useless is just a waste of memory. Hence, implementation of device drivers as LKM makes sense.

### Implementation Steps:
1. Understand the device characteristic and supported commands
2. Map device specific operations to unix file operation
3. Select the device name (user interface) Namespace (2-3 characters, /dev/dv1)
4. Select a major number and minor number (this step is optional)
5. Mapping the number to right device sub-routines
6. Implement file interface subroutines
7. Compile the device driver
8. Install the device driver module with loadable kernel module (LKM)


## More details:
- http://en.wikipedia.org/wiki/Loadable_kernel_module
- http://www.tldp.org/HOWTO/Module-HOWTO/x73.html
- http://www.freesoftwaremagazine.com/articles/drivers_linux
- http://oreilly.com/openbook/linuxdrive3/book/
