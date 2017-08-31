Device Drivers
=================
**What are device drivers?**

Device drivers are simply programs which executes in kernel mode (unrestricted mode) interacting directly with hardware of the corresponding device. They mainly do all the talking/interaction with raw hardware as part OS.

**Why we need them?**

Every device is/can be unique with different functionality. To access and exploit all the features of the device it is important we need to know
-Devices capabilities?
-How to program to access capabilities?
Device drivers are the answers to the questions above.

**Who writes them?**

Usually developers @ device manufacturer writes them.
It is logical that they know everything about device. Also, it is common to involve device driver developers in design of device features.

But given the features/specifications of the hardware any one can write a driver for them. May be we will try to see how to write device drivers in following sections.


## Device driver - File Operations structure

An important structure in any device driver is the  **file_operations**.  It holds the  pointers to functions defined by the driver implementation to perform various operations on the device.
Each field of the structure corresponds to the address of some function defined by the driver to handle a requested operation. As discussed earlier we have device being accessed like files and hence  all the operations of files are to be implemented.

Following is an example of creating device specific implemetation for standard file operations open, close, read, write.

**Example:**

     struct file_operations fops = {
       read: device_read,
       write: device_write,
       open: device_open,
       release: device_release
     };

    /* Actual methods for device operations */
    int init_module(void) {
      //Initialization code
    }
    
    void cleanup_module(void) {
      //Cleanup code
    }
    
    static int device_open(struct inode *, struct file *) {
      //open operations - dont forgret to return the file descriptior for future use
    }
    
    static int device_release(struct inode *, struct file *) {
      //Close operations implementation
    }
    
    static ssize_t device_read(struct file *, char *, size_t, loff_t *) {
      //Read operation implementation
    }
    
    static ssize_t device_write(struct file *, const char *, size_t, loff_t *) {
      //Write operation implementation
    }


We can have other function implementations as well. The entire list of the file_operation is given below:

    struct file_operations {
       struct module *owner;
       loff_t (*llseek) (struct file *, loff_t, int);
       ssize_t (*read) (struct file *, char *, size_t, loff_t *);
       ssize_t (*write) (struct file *, const char *, size_t, loff_t *);
       int (*readdir) (struct file *, void *, filldir_t);
       unsigned int (*poll) (struct file *, struct poll_table_struct *);
       int (*ioctl) (struct inode *, struct file *, unsigned int, unsigned long);
       int (*mmap) (struct file *, struct vm_area_struct *);
       int (*open) (struct inode *, struct file *);
       int (*flush) (struct file *);
       int (*release) (struct inode *, struct file *);
       int (*fsync) (struct file *, struct dentry *, int datasync);
       int (*fasync) (int, struct file *, int);
       int (*lock) (struct file *, int, struct file_lock *);
      ssize_t (*readv) (struct file *, const struct iovec *, unsigned long,
          loff_t *);
      ssize_t (*writev) (struct file *, const struct iovec *, unsigned long,
          loff_t *);
    };









## Useful resource:
- http://lwn.net/Kernel/LDD3/
- http://lwn.net/images/pdf/LDD3/ch03.pdf
