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

But given the features/specifications of the hardware any one can write a driver for them. May be we will try to see how to write device drivers in following posts.


***Useful resource:***

http://lwn.net/Kernel/LDD3/
