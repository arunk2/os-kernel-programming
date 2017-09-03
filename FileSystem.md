Filesystem Basics
=================
FS is a part of OS, whose purpose is to store and retrieve information (data) from any storage medium. 
Without a FS, information on storage medium is meaningless or just a single piece of huge data.

Lets discuss this in detail. Any storage device (Hard disk, CD, DVD, Flash, RAID, Tape) comes with a device driver(DD). 
DD are the lowest level of programmable abstraction available for any program wanting to use the device. 
We also know that every device is available as file to OS (like Linux OS). 
Hence, the abstraction of reading entire data from storage device as a single piece of data. 
Every part of device is accessed through LBA (logical block address), which gives the single piece of huge data.

Writing DD, utilizing features (following the specification) of device is not related to FS. 
It is called device driver development. We will discuss on this sometime later. 

FS provides abstract programmable layer, which encapsulates all the direct DD communication (and devices). 
It logically groups information/data stored in device into multiple items. We typically call these individual items as files. 
There are also special type of files called as directories typically used to group other files into a hierarchy structure of files. 
Individual files are identified by a fully qualified path (like '/usr/home/file1.txt')

Precisely a FS is the set of programs(executable instances) which logically divides a storage device into many files. 
It gives an API for other programs, which is independent of the device for manipulating files. 
We normally refer these APIs as filesystem system calls. We have different kinds of FS. 
Each of them differ in the way of logical grouping and structure to provide the abstraction of multiple files. 

It is curious to ask why there are multiple FS, knowing the fact that it is more than 4 decades since first FS for Unix based systems were introduced. 
Ideally the best FS should have been found and used by every OS for every device. But it is not. Why?

Lets answer this, the argument goes as below.
It is logical to have -

1. Different FS for different type of storage devices.

   We have FS like 
   - ext(2,3,4), FAT, FAT32, NTFS, XFS, Journaling FS for Disk based devices
   - UDF for optical discs like CDs, DVDs, Blu-Ray
   - JFFS, YAFFS, UBIFS, F2FS, LogFS for flash based devices 
   - Linear Tape FS for Tape devices

2. Different FS for different requirements/usage (upper layers using FS).

   We have FS like
   - differnt databases like DB2, Oracle, MySQL uses - Transactional based FS
   - Network based FS like NFS
   - Shared disk FS like GFS, Hadoop

-------------------------------

Earlier we discussed about what a File system was and why we need different type of file systems. 
Let us discuss various key components of FS and implementation of them. 

As discussed earlier FS gives abstraction to other programs to store and retrieve data on a storage device (through APIs or FS System calls). Let us see how the call from user API goes and fetches data from storage system.

### User Space:
1. User application uses FS through APIs (like fopen, fread, fwrite). 
2. These are not actual system calls, but are simple library calls (available as part of **libc.so** for every user programs). 
3. These lib functions save the current context (stack, execution register details - through assembly instructions) 
4. Pack the arguments along with corresponding system call no
5. After they raise a trap (software interrupt) by calling trap instruction (direct assembly instruction). 

### Kernel Space:
6. Interrupt handler observes a system call request and switches to kernel mode
7. calls the appropriate system call with packed arguments
8. System call implementation will check for legality of the arguments (typically validity of the buffer being passed for read/write operations is checked)
9. Makes call to the VFS system through (vop_open, vop_read, vop_write)
10. VFS simply calls the corresponding FS's **ufs_open, ufs_read, ufs_write** calls. 
11. These methods actually implement the underlying FS for mapping in and out of device through device drivers of the system.
12. This layer keeps the implementation of mapping a file name (like '/usr/test/file1.txt') into some index number (called as inode number) 
13. All the related blocks, where data for the given file is stored. 
14. Once the blocks are identified (which are nothing but LBA - Logical Block Address), they call device drivers with corresponding operation open/read/write for given LBA.
15. The device drivers actually checks for buffer validity and initiates the corresponding operation on the given LBA and suspends. 
16. Device controller, part of every device maps the LBA to the actual location of device and does the requested operation and uses the DMI controller to move the requested data in/out of device and memory location.
17. Once the operation is completed - buffer is loaded by the DMI mechanism and it awakes the suspended thread and returns 'return code' back to the user application after handling and raising respective error messages at each level.

Real FS are normally implemented with Virtual memory subsystem, which adds additional layer in the translation process and gives flexibility of **memory mapping, shared memory, security and uniform address space** for every process.
