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
