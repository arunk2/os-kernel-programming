Compile & Boot a Linux Kernel
=============================
It becomes absolutely necessary for a Kernel Hacker to compile various kernel sources and boot them for either taking traces or testing a modification for a kernel module. Although there are lot of blogs talk about this compile and booting, I found the following resource more useful (http://www.wikihow.com/Compile-the-Linux-Kernel). I will explain the overview for the whole process, for detailed steps one can follow the above link.

> Assumption: Logged-in user has root privileges

## Steps:
1. Get the kernel image you want to work with (http://www.kernel.org)
2. Extract to /usr/src directory and compile (make) from there
3. Configure kernel per your need. (from the menu options). This is done with command (make menuconfig)
4. Compile Kernel and install it (make && make modules_install && make install)
5. Change the boot loader to point the new compiled version

## For more details:
http://www.wikihow.com/Compile-the-Linux-Kernel
