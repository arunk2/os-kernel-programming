Important Kernel routines
=========================
For most of the kernel hackers or device driver programmers, lets try to list some of the mostly used kernel routines, 
their need and usage.

## printk():
Used mainly for debugging, error tracking purpose. You may get them in syslogs/console depending on configuration.

**Usage:**

    printk(KERN_INFO "Hello value = %d\n", i);

we have other flags from highest to lowest:

    KERN_EMERG  high priority  low number
    KERN_ALERT
    KERN_CRIT
    KERN_ERR
    KERN_WARNING
    KERN_NOTICE
    KERN_INFO
    KERN_DEBUG  low priority  hi number


## get_user() / put_user():

Used to get and put basic primitive values (such as an int, char, or long) from and to userspace. A pointer into userspace should never be simply dereferenced: data should be copied using these routines. Both return -EFAULT or 0.
These functions may sleep on a PAGE_FAULT and hence must always be called inside user context and with no interrupts disabled, or holding a spinlock.

**Usage:**

    get_user( x, ptr );
    put_user( x, ptr );


## copy_to_user()/copy_from_user():

They are used to copy an aritrary amount of data to and from userspace. Very similar to their primitive counterpart these functions may sleep on a PAGE_FAULT and hence must always be called inside user context and with no interrupts disabled, or holding a spinlock.

**Usage:**

    copy_to_user( to, from, n );
    copy_from_user( to, from, n );


## kmalloc()/kfree():

Very similar to malloc() and free() routines in user program (for allocation in userspace), we have these routines to dynamically request pointer-aligned chunks of memory. kmalloc() takes an extra flag giving more details about the memory chunk to be allocated.

- **GFP_KERNEL:** Most reliable way to allocate memory. The request may sleep and swap to free memory hence it is only allowed in user context (not in interrupt context).
- **GFP_ATOMIC:** This call will never sleep, hence can be called in interrupt context. Less reliable than GFP_KERNEL. Out-of-memory error handling must be done to avoid any kernel panics.


### More Details:

http://www.ibm.com/developerworks/linux/library/l-kernel-memory-access/index.html
http://linuxforthenew.blogspot.in/2013/01/why-doshould-we-use-copyfromuser-or.html

