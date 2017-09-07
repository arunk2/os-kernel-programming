System call in Linux - (x86 Arch implementation)
================================================

**System calls** are used by user programs in order get service from the operating system. Some of the popular system calls are we normally use are **open, read, write, close, wait, exec, fork, exit, and kill**. 
There are usually 100s of system call available in OS. For example, Linux has 300+ system calls.

### Why we need system call?
since, all the user program run only in 'user mode' it cannot access any resources. 
As we all know OS running in **kernel mode** can access a system's hardware directly and this designed so that the kernel can keep the system safe and secure from malicious programs. 
Of-course most of the user programs require access to system resources (example: to play a music, display video), but it cannot access them directly. 
Therefore it requests the **operating system for assistance**. Typically this is done through appropriate system call and executes in the kernel mode. 

## How System call works?
Every system call has a **number** associated with it. 
This number is passed to the kernel and that's how the kernel knows which system call was made. 
Another important aspect is that often user programs needs data/information from hardware it get them via **buffer accessible in user mode** sent as arguments to system calls. 

### What actually happens?
1. user program issues a system call, it is actually calling a library routine. 
2. The library routine issues a trap (software interrupt) to the operating system(eg. Linux OS) by executing **INT 0x80 assembly instruction (in x86 architecture)**. 
3. In x86 architecture specific implementation, it passes the system call number to the **kernel using the EAX register**. 
4. The arguments of the system call are also passed to the kernel using other registers (EBX, ECX, etc.). 
5. The kernel executes the system call and returns the result to the user program using a register. 


## How to access 'user buffer'?
There are type safe kernel APIs available for accessing user buffer.

### get_user() / put_user():

Used to get and put basic primitive values (such as an int, char, or long) from and to userspace. A pointer into userspace should never be simply dereferenced: data should be copied using these routines. Both return -EFAULT or 0.
These functions may sleep on a PAGE_FAULT and hence must always be called inside user context and with no interrupts disabled, or holding a spinlock.

**Usage:**

    get_user( x, ptr );
    put_user( x, ptr );


### copy_to_user()/copy_from_user():

They are used to copy an aritrary amount of data to and from userspace. Very similar to their primitive counterpart these functions may sleep on a PAGE_FAULT and hence must always be called inside user context and with no interrupts disabled, or holding a spinlock.

**Usage:**

    copy_to_user( to, from, n );
    copy_from_user( to, from, n );

-------------------------------------------------------

## Adding a new system call to Linux Kernel
Let us try to create a toy system call to do add operation, which takes 2 arguments and return their added value.

Following are the steps in adding a new system call to Linux Kernel:

1. Unzip and untar the latest Linux kernel source (https://www.kernel.org - currently 3.14 is the stable version) into /usr/src/ directory.
2. Under /usr/src/Linux-x.x.x/kernel/ directory, Create a new file 'add_syscall.c' to define your system call with the following content.

        #include <Linux/linkage.h>

        asmlinkage int sys_add_syscall (int arg1, int arg2) { 
         return(arg1 + arg2);
        }

3. In /usr/src/Linux-x.x.x/include/asm/unistd.h, define an index for the new system call. The index should be the number after the last system call defined in the list. Create new entry as below

        #define __NR_sys_add_syscall 351

4. Increment the system call count (since you have added a new system call). 

        #define __NR_syscalls 352

5. In /usr/src/Linux-x.x.x/arch/i386/kernel/entry.S, define a pointer to hold a reference to the new system call routine. (location/position should be same as the system call index defined in unistd.h).
    
        .long sys_myservice

6. Add the system call to Makefile in /usr/src/Linux-x.x.x/kernel/Makefile. Add object after the other kernel objects have been declared.

        obj-y += add_syscall.o

7. Build the kernel with this change from /usr/src/Linux-x.x.x using the following commands

        make xconfig
        make dep //make dependency list
        make bzImage //build kernel image
    
8. Boot the new kernel image by modifying the lilo loader (by editing /etc/lilo.conf)

## Testing the toy 'add_syscall'

1. Create a test.c file in home directory with the following content.

        #include <Linux/errno.h>
        #include<sys/syscall.h>
        #include <Linux/unistd.h>

        _syscall2(int, add_syscall, int, arg1, int, arg2);

        main() {
         printf ("Res = %d\n", add_syscall(1, 2));
        }

2. Compile and run the binary.

        Output: 3

If you get '3' as output, everything worked as expected and you have successfully created and added a system call to Linux kernel.
